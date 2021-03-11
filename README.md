# Use Open3D as a CMake External Project

This is one of the two CMake examples showing how to use Open3D in your CMake
project:

* [Find Pre-Installed Open3D Package in CMake](https://github.com/intel-isl/open3d-cmake-find-package)
* [Use Open3D as a CMake External Project](https://github.com/intel-isl/open3d-cmake-external-project)

For more details, check out the [Open3D repo](https://github.com/intel-isl/Open3D) and
[Open3D docs](http://www.open3d.org/docs/release/cpp_project.html).

## Ubuntu 18.04+

```bash
# Install minimal Open3D compilation dependencies. For the full list, checkout:
# https://github.com/intel-isl/Open3D/blob/master/util/install_deps_ubuntu.sh
sudo apt-get --yes install xorg-dev libglu1-mesa-dev

# Compile your example project with Open3D.
git clone https://github.com/intel-isl/open3d-cmake-external-project.git
cd open3d-cmake-external-project
mkdir build
cd build
cmake ..
make -j$(nproc)
./Draw
```

## macOS

```bash
git clone https://github.com/intel-isl/open3d-cmake-external-project.git
cd open3d-cmake-external-project
mkdir build
cd build
cmake ..
make -j$(nproc)
./Draw
```

## Windows 10

```batch
git clone https://github.com/intel-isl/open3d-cmake-external-project.git
cd open3d-cmake-external-project
mkdir build
cd build
cmake -G "Visual Studio 16 2019 Win64" -A x64 ..
cmake --build . --config Release
Release\Draw
```
