# On Ubuntu 18.04, get the latest CMake from https://apt.kitware.com/.
cmake_minimum_required(VERSION 3.18)
set(CMAKE_CXX_STANDARD 14)
project(Open3DCMakeExternalProject LANGUAGES C CXX)

option(GLIBCXX_USE_CXX11_ABI   "Set -D_GLIBCXX_USE_CXX11_ABI=1"       OFF)
option(STATIC_WINDOWS_RUNTIME  "Use static (MT/MTd) Windows runtime"  ON )

if(NOT CMAKE_BUILD_TYPE)
    message(STATUS "No CMAKE_BUILD_TYPE specified, default to Release.")
    set(CMAKE_BUILD_TYPE "Release")
endif()

# Option 1: Use ExternalProject_Add, as shown in this CMake example.
# Option 2: Install Open3D first and use find_package, see
#           http://www.open3d.org/docs/release/cpp_project.html for details.
include(ExternalProject)
ExternalProject_Add(
    external_open3d
    PREFIX open3d
    GIT_REPOSITORY https://github.com/intel-isl/Open3D.git
    GIT_TAG master
    GIT_SHALLOW ON
    UPDATE_COMMAND ""
    # Check out https://github.com/intel-isl/Open3D/blob/master/CMakeLists.txt
    # For the full list of available options.
    CMAKE_ARGS
        -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
        -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
        -DCMAKE_C_COMPILER=${CMAKE_C_COMPILER}
        -DCMAKE_CXX_COMPILER=${CMAKE_CXX_COMPILER}
        -DGLIBCXX_USE_CXX11_ABI=${GLIBCXX_USE_CXX11_ABI}
        -DSTATIC_WINDOWS_RUNTIME=${STATIC_WINDOWS_RUNTIME}
        -DBUILD_SHARED_LIBS=ON
        -DBUILD_PYTHON_MODULE=OFF
        -DBUILD_EXAMPLES=OFF
)
ExternalProject_Get_Property(external_open3d INSTALL_DIR)
set(OPEN3D_INCLUDE_DIRS ${INSTALL_DIR}/include ${INSTALL_DIR}/include/open3d/3rdparty)
set(OPEN3D_LIB_DIR ${INSTALL_DIR}/lib)

add_executable(Draw Draw.cpp)
add_dependencies(Draw external_open3d)
target_include_directories(Draw PRIVATE ${OPEN3D_INCLUDE_DIRS})
target_link_directories(Draw PRIVATE ${OPEN3D_LIB_DIR})
target_link_libraries(Draw PRIVATE Open3D)
target_compile_definitions(Draw PRIVATE _GLIBCXX_USE_CXX11_ABI=$<BOOL:${GLIBCXX_USE_CXX11_ABI}>)
