# Build Instructions

This is a C++ project built using [CMake](https://cmake.org/).  Building it should just be a matter of installing
dependencies (Qt 6, spdlog, Boost) and then using CMake to compile it.

Please add more detailed instructions here if you have success building it on your platform!

## Linux

1. Install dependencies.
   - Ubuntu:
    ```
    sudo apt install \
        build-essential \
        cmake \
        git \
        libboost-all-dev \
        libspdlog-dev \
        ninja-build \
        qt6-base-dev \
        qt6-svg-dev
    ```
   - Fedora:
    ```
    sudo dnf install \
        boost-devel \
        boost-static \
        cmake \
        gcc-c++ \
        ninja-build \
        qt6-qtbase-devel \
        qt6-qtsvg-devel \
        spdlog-devel
    ```
   
2. Create a `build` directory inside the repository and run cmake in it:
   ```
   cd xenoprobes/
   cmake -B build -DCMAKE_BUILD_TYPE=Release -G Ninja
   ```
3. Build it:
   ```
   cmake --build build/
   ```
4. After it's finished building, the command line tool will be in `build/src/xenoprobes/` and the GUI
   will be in `build/src/xenoprobes_gui/`.
5. Optionally, cd into `build/` and run `cpack -G DEB` to build a `.deb` package or `cpack -G RPM` to build an `.rpm`.

### Windows

1. Install dependencies:
   - [Visual Studio](https://visualstudio.microsoft.com/)
   - [CMake 3.31.6](https://github.com/Kitware/CMake/releases/download/v3.31.6/cmake-3.31.6-windows-x86_64.msi) (**note**: CMake 4.0.0 will not work, you need 3)
   - [vcpkg](https://learn.microsoft.com/en-us/vcpkg/get_started/get-started?pivots=shell-powershell)
     - Make sure you set your `VCPKG_ROOT` environment variable to the location where you clone vcpkg, and add `%VCPKG_ROOT%` to your `PATH` environment variable.
   - [git](https://git-scm.com/downloads)

2. Open a developer console, `cd` to the `xenoprobes` project directory, and use `vcpkg` to install dependencies.
   Note that it will take several hours and a few hundred GB of disk space to build all of them.  Some packages also
   require very long path names to build, and you will need to point it at a very short path that it can use
   to build them.  After installation is complete, you can delete this path.
   ```
   cd xenoprobes/
   vcpkg install --x-buildtrees-root=C:\v\
   ```
3. Now you can create a build directory and use CMake to build it, then CPack to create an installer executable.
   ```
   mkdir build
   cd build
   cmake .. -DCMAKE_BUILD_TYPE=Release
   cmake --build . --config Release
   cpack
   ```
