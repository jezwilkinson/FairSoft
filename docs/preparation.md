## I. Preparation

### I.1. Install the [prerequisites](prerequisites.md).

### I.2. Clone the repo

If you are running on NFS, please take note the [Filesystem requirements](https://spack.readthedocs.io/en/latest/basic_usage.html#filesystem-requirements) of spack on the ``flock`` requirements of spack and possible workarounds. Also, compiling ROOT with X11 support will install font-related packages which require ``$HOME/.cache/fontconfig/`` to support locking.

First, check out the repository for Spack from Git (`--depth 2` is recommended to significantly reduce the download size)
```
git clone --depth 2 --branch tags/v1.0.0 https://github.com/spack/spack
```

By default, Spack will place its recipe repository in your home directory when it first runs. If you want the recipes to be kept in another location (such as shared network storage) or need to modify them, you should manually check out the `spack-packages` repository as well:

```
git clone -c feature.manyFiles=true https://github.com/spack/spack-packages.git
```


### I.3. Run the first-time Spack setup

Enter the `spack` directory, and run `share/spack/setup-env.sh` to intialise the environment:
```
cd spack
. share/spack/setup-env.sh
```
If you separately checked out the `spack-packages` repository, you should now set it as Spack's default repo location (use the full path, not a relative path):
```
spack repo set --destination /path/to/spack-packages builtin
```

### I.4. Activate Spack in your current shell

Only needed in new shells where you have not just performed the previous steps.

```
source /path/to/spack/share/spack/setup-env.sh
```

Verify that the `spack` command works and lists the correct FairSoft package [repository](https://spack.readthedocs.io/en/latest/repositories.html).

```
$ spack list fairsoft-bundle
fairsoft-bundle
==> 1 packages
```
