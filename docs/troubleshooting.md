# Troubleshooting

Table of Contents
* [General](#general)
* [g++: internal compiler error: Killed (program cc1plus)](#g-internal-compiler-error-killed-program-cc1plus)
* [Building DDS fails with external (non-spack) non-system compiler](#building-dds-fails-with-external-non-spack-non-system-compiler)
* [Warning: Failed to initialize repository](#warning-failed-to-initialize-repository)


## General

The command `spack clean` can be used to clean up Spack's working space. By default without any options, `spack clean` will remove temporary staged builds from failed installations.

On occasion when compilers or package specs are updated with new patches, Spack will fail to concretise new versions. This can usually be resolved using `spack clean --all` to remove Spack's long-term caches, staged builds, and cached downloads.


## g++: internal compiler error: Killed (program cc1plus)

If you get errors with "compiler error: Killed", then this most likely means issues of the compiler / system. In most cases, this will be related to not having enough RAM for a parallel build. In order to limit the number of compilation threads running in parallel, use the `-j` switch:

```bash
$ spack install -j4
```

where `4` is the number of parallel build jobs. We recommend 2 GB of system RAM per such job.

