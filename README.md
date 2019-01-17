# libxml2-cmake

LibXml2 with a CMake-based build system.

**This repo is still a work in progress: use only if you are fully aware of what you are doing.**

## Installation

The project can be download and installed as any CMake project, for example on `*nix` systems
the library can be installed in the `<prefix>` directory with the following commands:
~~~
git clone https://github.com/robotology-dependencies/libxml2-cmake-buildsystem
cd libxml2-cmake
cmake -DCMAKE_INSTALL_PREFIX=<prefix> ..
cmake --build . --target INSTALL
~~~

Once you installed the library, it should be possible to find it using the [`FindLibXml2.cmake`](https://cmake.org/cmake/help/latest/module/FindLibXml2.html) module available in CMake.
If you specified a non-standard `<prefix>`, you may need to also add `<prefix>` to [`CMAKE_PREFIX_PATH`](https://cmake.org/cmake/help/latest/variable/CMAKE_PREFIX_PATH.html).

For more details on how to configure, compile and install a CMake project, see [CGold section on Generate native tool files](https://cgold.readthedocs.io/en/latest/first-step/generate-native-tool.html).
Note that the repo does not contain a copy of the libxml2 source code, that is instead downloaded during the CMake configuration using the [CMake's FetchContent module](https://cmake.org/cmake/help/v3.13/module/FetchContent.html).

## Options
This CMake-based build system for libxml2 aims to support all the options supported by the autotools-based
official build system of libxml2.

Configure command line option such as:
~~~
./configure --with-ftp
~~~
are converted to CMake command line options such as:
~~~
cmake -DLIBXML2_WITH_FTP:BOOL=ON ..
~~~

The additional prefix was added to avoid conflicts when this project is included in bigger CMake projects using
the `add_subdirectory` CMake command.

### Without options
autotools options such as:
~~~
./configure --without-ftp
~~~
are supported by setting to `OFF` the corresponding CMake options such as:
~~~
cmake -DLIBXML2_WITH_FTP:BOOL=OFF ..
~~~

### Shared and static libraries
`--build-shared` and `--build-static` autotools options are not directly supported, but instead you can set the `BUILD_SHARED_LIBS` option to
`ON` if you want to compile shared libraries, or `OFF` if you want to compiled static libraries. See
[CGold section on Shared + Static](https://cgold.readthedocs.io/en/latest/tutorials/libraries/static-shared.html) for more info on this.
