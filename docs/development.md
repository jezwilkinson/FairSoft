## IV. Development

### IV.1. Classic "cmake -> make -> make install" workflow (FairRoot and/or Experiment)

```
[fairsoft-env] $ export SIMPATH=<path of your choice>
[fairsoft-env] $ spack view --dependencies true [-e fairroot] symlink -i $SIMPATH fairroot [cmake]
```

The above will create a directory structure at the path of your choice that can be used as
* $SIMPATH - with `-e fairroot`, or
* $SIMPATH and $FAIRROOTPATH - without `-e fairroot`.

If you need a newer CMake version than your system provides, add `cmake` at the end of the `spack view` command which will make a recent version available at `$SIMPATH/bin/cmake`.

A $SIMPATH created as shown above may be removed by a simple `rm -rf $SIMPATH`. This will **not** uninstall the packages themselves and you may recreate the view without recompilation.

### IV.2. Spack dev-build (single-package)

A package can be built in development mode - without checking it out from repository. In this case the code will be taken from local directory SOURCE_PATH.
The following command will run a development build of FairRoot with dependencies equivalent to the May25 environment.

```
spack dev-build -j JOBS -d SOURCE_PATH fairroot@18.8.2+sim+examples ^fairsoft-bundle@2025-05
```
