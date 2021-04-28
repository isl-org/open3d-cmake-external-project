# Use Open3D as a CMake External Project

This is one of the two CMake examples showing how to use Open3D in your CMake
project:

* [Find Pre-Installed Open3D Package in CMake](https://github.com/intel-isl/open3d-cmake-find-package)
* [Use Open3D as a CMake External Project](https://github.com/intel-isl/open3d-cmake-external-project)

For more details, check out the [Open3D repo](https://github.com/intel-isl/Open3D) and
[Open3D docs](http://www.open3d.org/docs/release/cpp_project.html).

## Step 1: Install Open3D dependencies

On Ubuntu:

```bash
# Install minimal Open3D compilation dependencies. For the full list, checkout:
# https://github.com/intel-isl/Open3D/blob/master/util/install_deps_ubuntu.sh
sudo apt-get --yes install xorg-dev libglu1-mesa-dev
```

On macOS/Windows:

```bash
# Skip this step
```

## Step 2: Use Open3D in this example project

You can specify the number of parallel jobs to speed up compilation.

On Ubuntu/macOS:

```bash
git clone https://github.com/intel-isl/open3d-cmake-external-project.git
cd open3d-cmake-external-project
mkdir build
cd build
cmake ..
cmake --build . --config Release --parallel 12
./Draw
```

On Windows:

```batch
git clone https://github.com/intel-isl/open3d-cmake-external-project.git
cd open3d-cmake-external-project
mkdir build
cd build
cmake ..
cmake --build . --config Release --parallel 12
Release\Draw
```
