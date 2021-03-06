cmake_minimum_required(VERSION 3.0)
project(ANTLRBase)

# Ensure tool dependencies.
include(ExternalProject) # Required to download and build external projects (i.e. ANTLR)
find_package(Git REQUIRED) # Need git to download ANTLR through ExternalProject
find_package(Java COMPONENTS Runtime REQUIRED) # Need java to run ANTLR, but only the runtime

# Set C++ standards.
set(CMAKE_CXX_STANDARD 11)

# Grab ANTLR.
include("${CMAKE_SOURCE_DIR}/cmake/get_antlr.cmake")

# Set up paths and info to generate ANTLR sources with.
set(GRAMMAR_NAME "generator")
set(ANTLR_NAMESPACE "generator")

# Generate sources.
include("${CMAKE_SOURCE_DIR}/cmake/antlr_generate.cmake")

# Build src
add_subdirectory("${CMAKE_SOURCE_DIR}/src")
