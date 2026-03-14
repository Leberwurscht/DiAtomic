cmake_minimum_required(VERSION 3.18...3.26)
project(${SKBUILD_PROJECT_NAME} LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find Python and pybind11
set(PYBIND11_FINDPYTHON ON)
find_package(pybind11 CONFIG REQUIRED)

# First extension: identify
pybind11_add_module(identify MODULE diatomic/identify.cpp)
set_target_properties(identify PROPERTIES 
    OUTPUT_NAME "identify"
    LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/diatomic
)

# Second extension: wavenumbers
pybind11_add_module(wavenumbers MODULE diatomic/wavenumbers.cpp)
set_target_properties(wavenumbers PROPERTIES 
    OUTPUT_NAME "wavenumbers"
    LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/diatomic
)

# Install targets
install(TARGETS identify wavenumbers LIBRARY DESTINATION diatomic)
