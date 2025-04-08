cmake_minimum_required(VERSION 3.10)
# SET(CMAKE_CXX_COMPILER "C:/msys64/ucrt64/bin/g++.exe")
# SET(CMAKE_C_COMPILER "C:/msys64/ucrt64/bin/gcc.exe")
# SET(CMAKE_MAKE_PROGRAM "C:/msys64/usr/bin/make")
# set(CMAKE_C_COMPILER_WORKS 1)
# set(CMAKE_CXX_COMPILER_WORKS 1)

project(DICProject)

# set(OpenCV_ROOT "${VCPKG_INSTALLED_DIR}/x64-windows/share/opencv4")
find_package(OpenCV REQUIRED)
# find_package(fftw3 CONFIG REQUIRED)
# find_package(Ceres CONFIG REQUIRED)

# Set files
SET(ncorr_src ../src/ncorr.cpp ../src/Strain2D.cpp ../src/Disp2D.cpp ../src/Data2D.cpp ../src/ROI2D.cpp ../src/Image2D.cpp ../src/Array2D.cpp)
SET(ncorr_h ../include/ncorr.h ../include/Strain2D.h ../include/Disp2D.h ../include/Data2D.h ../include/ROI2D.h ../include/Image2D.h ../include/Array2D.h)

# Set include directory
INCLUDE_DIRECTORIES(./include)

# Add library
ADD_LIBRARY(ncorr STATIC ${ncorr_src} ${ncorr_h})

# Set C++11 support
set_property(TARGET ncorr PROPERTY CXX_STANDARD 11)
set_property(TARGET ncorr PROPERTY CXX_STANDARD_REQUIRED ON)

# # Set -03 optimization
# INCLUDE(CheckCXXCompilerFlag)
# CHECK_CXX_COMPILER_FLAG("-O3" COMPILER_SUPPORTS_O3)
# if (COMPILER_SUPPORTS_O3)
# 	SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
# endif()

# include_directories(${OpenCV_INCLUDE_DIRS})
# add_executable(DICProjec1t ${ncorr_src})
add_executable(DICProject ncorr_test.cpp)

message(STATUS "OpenCV libraries: ${OpenCV_LIBS}")

target_link_libraries(DICProject ncorr)
target_link_libraries(DICProject ${OpenCV_LIBS})
# target_link_libraries(DICProject PUBLIC fftw3::fftw3)
# target_link_libraries(DICProject PUBLIC SuiteSparse::amd SuiteSparse::btf SuiteSparse::klu SuiteSparse::ldl)