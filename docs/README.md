## Spack based FairSoft

### Preface

The Spack-based FairSoft distribution is currently in an EXPERIMENTAL state. FairSoft releases are available via the `fairsoft-bundle` package, starting from the May25 release. In the mid-term future we plan to retire the CMake-based "Legacy" FairSoft and fully switch to the Spack-based one. The installation has been tested across multiple operating systems and architectures (Ubuntu 24.04, AlmaLinux 9, Mac OSX (x86 and ARM)).

### Introduction

This new FairSoft distribution modernizes and reorganizes the framework installation.
All needed packages, including the FairRoot package itself,
are now installed using [Spack](https://spack.readthedocs.io/en/latest/).

The packages are installed by Spack automatically using package [recipes](https://spack-tutorial.readthedocs.io/en/latest/tutorial_packaging.html), stored in the corresponding folders of the [packages](https://github.com/spack/spack-packages/tree/develop/repos/spack_repo/builtin/packages) directory of the `spack-packages` repository. The [recipe](https://spack-tutorial.readthedocs.io/en/latest/tutorial_packaging.html)
lists the dependencies of the given package and describes its installation procedure. A collection of packages that form the software framework is called a [spack environment](https://spack.readthedocs.io/en/latest/environments.html)  - examples of such are located in the [env](./env) directories.

In the process of installing of a package, Spack creates its list of dependencies,
forming a so-called installation tree. It is possible to install different packages/versions with [Spack](https://spack.readthedocs.io/en/latest/). Since they share a common installation tree, Spack reuses already available software when installing new packages.


### Table of Contents
* [I. Preparation](preparation.md) (download the package)
* [II. Installation](installation.md) (install packages in environment)
* [III. Execution](execution.md) (using the framework)
* [IV. Development](development.md)
* [V. Troubleshooting](troubleshooting.md)
* [VI. Advanced topics](advanced.md)

#### Appendix:
* [Structure of this repo](structure.md)