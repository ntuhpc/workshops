# NTUHPC HPC Compute: Build Guide
This guide introduces how to build software for NTUHPC's HPC Compute cluster.
Generally, built software artifacts are reside in `/scratch/apps` and can be
exposed to a system using an [modulefile](https://lmod.readthedocs.io/en/latest/015_writing_modules.html) in `/scratch/apps/modulefiles`.

## Build Dependencies
When do build dependencies occur? Generally they occur when programs are linked to libraries built with a specific environment (eg. compiler / MPI):
- **Compiler Dependency**
    If `libA` is built with `compilerC` (e.g., GCC 9.3.0), then `libA` _depends_ on that exact compiler ABI/version. Any program linking to `libA` must be built with the same compiler to ensure ABI compatibility.
- **MPI stack dependency:**  
    Software built with an MPI library depends on that exact MPI implementation and version (and its underlying compiler). This means if `libD` is built with `MPIx` on `compilerC`, it requires both the matching MPI and compiler environment at runtime.

## Install Prefix
Where should I install my software under `/scratch/apps`?
- **No Dependency** `/scratch/apps/<NAME>/<VERSION>`
- **Compiler Dependency** `/scratch/apps/<compilerName>-<version>/<pkgName>/<pkgVersion>/`
- **MPI Dependency** `/scratch/apps/<compilerName>-<version>/<mpiName>-<version>/<pkgName>/<pkgVersion>/`

## Modulefile
Where should I install my modulefiles under `/scratch/apps/modulefiles`?
- **No Dependency** `/scratch/apps/modulefiles/Core/<name>/<version>.lua`
- **Compiler Dependency** ``/scratch/apps/modulefiles/Compilers/<compilerName>/<version>/<pkgName>/<pkgVersion>.lua`
- **MPI Dependency** `/scratch/apps/modulefiles/MPI/<compilerName>/<compilerVersion>/<mpiName>/<mpiVersion>/<pkgName>/<pkgVersion>.lua`
