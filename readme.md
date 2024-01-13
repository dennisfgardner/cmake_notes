# CMake Notes

A good reference is [Modern CMake for C++ by Rafal Swidzinski](https://www.packtpub.com/product/modern-cmake-for-c/9781801070058)

CMake version 3.15 and newer is considered modern CMake.

The CMake executables:

- cmake
- ctest
- cpack
- cmake-gui
- ccmake (console gui)

For a list of system generators: `cmake --help`
For a bunch of system information: `cmake -system-information [file]`

## Bare Minimum Example

Bare minimum `CMakeLists.txt`

```cmake
cmake_minimum_required(VERSION 3.20)
project(Hello)
add_executable(hello_program hello_world.cpp)
```

```bash
cmake -S . -B build
cmake --build build
./build/hello_program
```

## More Details on CMake Stages

There are three stages to CMake:

- configuration and generation
  - `cmake [options] -S <src_dir> -B <build_dir>`
  - will make the build dir if it does not already exist
  - stores information in CMakeCache.txt
  - `-D <var>=<value>` to define variable, e.g., `-D CMAKE_BUILD_TYPE=Release`
  - `-L` to list cache variables
  - `-LH` to list description of the variables
  - `LHA` to also list advanced variables
  - `--log-level=VERBOSE` or `--log-level=DEBUG` or `--log-level=TRACE` and others
  - `cmake --trace` for major debugging
  - `cmake -U <glob_expr>` to remove variables
- build
  - `cmake --build <build_dir> [options]`
  - `--config Debug` or `--config Release` or others
  - `--parallel <N>` or `-j <N>` for N parallel jobs
  - `--verbose` or `-v`
  - `--target <target_name1>` or `-t <target_name2>`
  - `--target clean` to remove all artifacts from build dir
  - `--clean-first` to rm all artifacts first, then build
- installation
  - `cmake --install <build_dir> [options]`
  - `--prefix` for installation prefix
  - `--config Debug` or `--config Release` or others
  - `--verbose` or `-v`
