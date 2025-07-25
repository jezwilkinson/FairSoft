## II. Installation

### II.1. Define a [spack environment](https://spack.readthedocs.io/en/latest/environments.html) for a FairSoft release

Create a fresh Spack environment for the FairSoft installation:
```
spack env create fairsoft-env
```
`fairsoft-env` can be any name you choose. 

You can also use one of the pre-defined environments from the `env/` folder in the FairSoft repository:

```
spack env create may25 /path/to/FairSoft/env/may25/sim/spack.yaml
```
This will let you skip the "`spack add` step below.


### II.2. Activate the Spack environment

In order to work with the previously defined environment, it needs to be activated in any given shell instance using the commands `spack env activate` or `spacktivate`:

```
spacktivate fairsoft-env
```

To check that the environment is properly loaded:
```
$ spack env status
==> In environment fairsoft-env
```

You may also activate an environment with `-p`, which generates a prefix to your prompt as long as the environment is active:

```
$ spacktivate -p fairsoft-env
[fairsoft-env] $
```

To deactive the active environment, run
```
spack env deactivate
```
or
```
despacktivate
```

### II.3. Compile and install the packages defined in the active [spack environment](https://spack.readthedocs.io/en/latest/environments.html)

First, activate your environment:
```
spacktivate -p fairsoft
```

FairSoft is listed in Spack as a "bundle package" named `fairsoft-bundle`, with its dependency versions pinned to specific combinations that are known to work well together. Release versions are numbered in "YYYY-MM" CalVer format (i.e. the "May25" release in the FairSoft repo is `fairsoft-bundle@2025-05` in Spack).

To see the list of available versions in the recipe, run `spack info fairsoft-bundle`:

```
BundlePackage:   fairsoft-bundle

Description:
    Bundle package providing default environment for FAIR software

Homepage: https://github.com/FairRootGroup/FairSoft

Preferred version:
    2025-05

Safe versions:
    2025-05

Deprecated versions:
    None

Variants:
    build_system [bundle]        bundle
        Build systems supported by the package
    graphics [false]             false, true
        Enable graphical support in ROOT
    mt [false]                   false, true
        Enable multithreading for GEANT4

Build Dependencies:
    faircmakemodules  fftw  geant3  geant4  geant4-vmc  openblas  pythia8  root  vgm  vmc

Link Dependencies:
    faircmakemodules  fftw  geant3  geant4  geant4-vmc  openblas  pythia8  root  vgm  vmc

Run Dependencies:
    fairsoft-config

Licenses:
    None
```

To add the May25 (2025-05) release of `fairsoft-bundle` to your environment's specification (spec), use `spack add`:
```
[fairsoft-env] $ spack add fairsoft-bundle@2025-05 fairroot
==> Adding fairsoft-bundle@2025-05 to environment fairsoft-env
```

You can remove packages from an existing spec with `spack remove [packagename]`.

The listed variants can also be customised by adding them to the end of the `spack add` command, with `+[variant]` to enable and `~[variant]` to disable:

```
[fairsoft-env] $ spack add fairsoft-bundle@2025-05 ~mt +graphics fairroot +sim +examples
==> Adding fairsoft-bundle@2025-05 to environment fairsoft-env
```

Then run `spack install` to concretize the dependency tree and install all of the defined packages in one shot:

```
[fairsoft-env] $ spack install
```
This step usually takes a while - time for a coffee break ☕.

### II.4. Verify the installation

To see your defined spec, and the full list of installed dependencies and their versions, use `spack find`:
```
[fairsoft-env] $ spack find
==> In environment fairsoft-env
==> 1 root specs
-- no arch / no compilers ---------------------------------------
[+] fairsoft-bundle@2025-05

-- linux-ubuntu24.04-skylake / %c,cxx,fortran=gcc@13.3.0 --------
geant3@4-4  hepmc3@3.3.0  openblas@0.3.29  root@6.36.00

-- linux-ubuntu24.04-skylake / %c,cxx=gcc@13.3.0 ----------------
berkeley-db@18.1.40  davix@0.8.10   geant4-vmc@6-7-p1  intel-tbb@2022.0.0   libtiff@4.7.0  nghttp2@1.65.0        pcre@8.45      unuran@1.8.1  xerces-c@3.3.0  zstd@1.5.7
clhep@2.4.7.1        expat@2.7.1    gettext@0.23.1     libffi@3.4.8         lz4@1.10.0     ninja@1.12.1          python@3.13.2  vc@1.4.5      xrootd@5.6.9
cmake@3.31.6         fcgi@2.4.4     hepmc@2.06.11      libjpeg-turbo@3.0.4  m4@1.4.19      nlohmann-json@3.11.3  re2c@3.1       vgm@5-3-1     xxhash@0.8.3
curl@8.11.1          geant4@11.3.2  hwloc@2.11.1       libpng@1.6.47        ncurses@6.5    openssl@3.4.1         rsync@3.4.1    vmc@2-1       zlib-ng@2.2.4

-- linux-ubuntu24.04-skylake / %c,fortran=gcc@13.3.0 ------------
fftw@3.3.10

-- linux-ubuntu24.04-skylake / %c=gcc@13.3.0 --------------------
automake@1.16.5  findutils@4.10.0  giflib@5.2.2  json-c@0.18    libiconv@1.18      libsigsegv@2.14  nasm@2.16.03  pkgconf@2.3.0  rngstreams@1.0.1  util-linux-uuid@2.41  xz@5.6.3
bzip2@1.0.8      freetype@2.13.2   gmake@4.4.1   libbsd@0.12.2  libmd@1.1.0        libtool@2.4.7    perl@5.40.0   popt@1.19      sqlite@3.46.0     xproto@7.0.31
diffutils@3.10   gdbm@1.23         gsl@2.8       libice@1.1.2   libpciaccess@0.17  libxml2@2.13.5   pigz@2.8      readline@8.2   tar@1.35          xtrans@1.6.0

-- linux-ubuntu24.04-skylake / %cxx=gcc@13.3.0 ------------------
pythia8@8.313  rapidjson@1.2.0-2024-08-16

-- linux-ubuntu24.04-skylake / no compilers ---------------------
autoconf@2.72                       fairsoft-bundle@2025-05  g4emlow@8.6.1     g4nudexlib@1.0           g4radioactivedecay@6.1.2  g4urrpt@1.1         glibc@2.39
ca-certificates-mozilla@2025-02-25  fairsoft-config@master   g4ensdfstate@3.0  g4particlexs@4.1         g4realsurface@2.2         gcc@13.3.0          util-macros@1.20.1
compiler-wrapper@1.0                g4abla@3.3               g4incl@1.2        g4photonevaporation@6.1  g4saiddata@2.0            gcc-runtime@13.3.0
faircmakemodules@1.0.0              g4channeling@1.0         g4ndl@4.7.1       g4pii@1.3                g4tendl@1.4               geant4-data@11.3.0
==> 101 installed packages
==> 0 concretized packages to be installed (show with `spack find -c`)
```
