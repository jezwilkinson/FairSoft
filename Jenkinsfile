#!groovy

def jobMatrix(String node_type, String ctestcmd, List specs, Closure callback) {
  def nodes = [:]
  for (spec in specs) {
    def label = spec.os
    def jobsh = "job_${label}.sh"
    def title = "build/${label}"
    def container = ""
    if (node_type == 'macos') {
      node_type = label
    } else {
      container = spec.container
    }
    nodes[title] = {
      node(node_type) {
        githubNotify(context: title, description: 'Building ...', status: 'PENDING')
        try {
          checkout scm

          if (node_type == 'slurm') {
            sh """
              echo '#! /bin/bash' > ${jobsh}
              echo 'echo "*** Job started at: \$(date -R)"' >> ${jobsh}
              echo 'echo "*** Job ID: \$SLURM_JOB_ID"' >> ${jobsh}
              echo "source <(sed -e '/^#/d' -e '/^export/!s/^.*=/export &/' /etc/environment)" >> ${jobsh}
              echo "export LABEL=${label}" >> ${jobsh}
              echo "${env.SINGULARITY_CONTAINER_ROOT}/run_container ${container} ${ctestcmd}" >> ${jobsh}
            """
            sh "cat ${jobsh}"
          }

          callback.call(spec, label, jobsh)

          githubNotify(context: title, description: 'Success', status: 'SUCCESS')
        } catch (e) {
          githubNotify(context: title, description: 'Error', status: 'ERROR')
          throw e
        }
      }
    }
  }
  return nodes
}

pipeline {
  agent none
  stages {
    stage('Run CI Matrix') {
      steps{
        script {
          def ctestcmd = "ctest -VV -S FairSoft_test.cmake"
          def linux_jobs = jobMatrix('slurm', ctestcmd, [
            [os: 'Fedora30', container: 'fedora.30.sif'],
            [os: 'Ubuntu-18.04-LTS', container: 'ubuntu.18.04.sif'],
            [os: 'Debian8', container: 'debian.8.sif'],
          ]) { spec, label, jobsh ->
            sh """
              echo "*** Submitting at: \$(date -R)"
              srun -p main -c 64 -n 1 -t 300 --job-name="alfaci-${label}" bash ${jobsh}
            """
          }
          def macos_jobs = jobMatrix('macos', ctestcmd, [
            [os: 'macOS10.14'],
          ]) { spec, label, jobsh ->
            sh """
              export LABEL=${label}
              ${ctestcmd}
            """
          }
          parallel(linux_jobs + macos_jobs)
        }
      }
    }
  }
}

