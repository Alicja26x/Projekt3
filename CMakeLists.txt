cmake_minimum_required(VERSION 3.14)

if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE "${CMAKE_SOURCE_DIR}/external/vcpkg/scripts/buildsystems/vcpkg.cmake"
        CACHE STRING "Vcpkg toolchain file")
endif()

set(VCPKG_INSTALLED_DIR "${CMAKE_SOURCE_DIR}/vcpkg_installed")

set(CMAKE_PREFIX_PATH "${CMAKE_SOURCE_DIR}/vcpkg_installed/x64-windows/share")

set(PYTHON_EXECUTABLE "${CMAKE_SOURCE_DIR}/envs/projekt3_env/python.exe" CACHE FILEPATH "Python interpreter")

project(signals)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)



find_package(pybind11 REQUIRED)
add_subdirectory(external/matplotplusplus)

find_package(fftw3 REQUIRED)
find_package(libpng REQUIRED)
find_package(jpeg REQUIRED)
find_package(lapack REQUIRED)
find_package(liblzma REQUIRED)
find_package(nodesoup REQUIRED)
find_package(openblas REQUIRED)
find_package(tiff REQUIRED)
find_package(libjpeg-turbo REQUIRED)
find_package(zlib REQUIRED)

include_directories(${CMAKE_SOURCE_DIR}/src)

pybind11_add_module(signals
    src/binding.cpp
    src/main.cpp
)


set_target_properties(signals PROPERTIES
    PREFIX "" 
    SUFFIX ".pyd"  
)
target_link_libraries(signals PRIVATE matplot)


