## Structure of this repo

Releases are defined as a Spack environment in the directory [`env/<release>/<variant>.yaml`](env/).

`docs/` contains additional documentation pages, the relevant ones for the user should all be linked from this top-level page.

`legacy/` contains the former shell script based FairSoft before we switched to Spack - it is no longer updated, but remains for reference.

`test/` contains mainly integration test related files used by the FairSoft Continuous Integration checks. Normal users can ignore them.

CMake/CTest-related files are mainly for internal use and running the FairSoft Continuous Integration checks. Normal users can ignore them.
