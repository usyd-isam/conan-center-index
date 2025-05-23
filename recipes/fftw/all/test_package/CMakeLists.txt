cmake_minimum_required(VERSION 3.15)
project(test_package LANGUAGES C)

option(ENABLE_DOUBLE_PRECISION "Enable FFTW single precision" ON)
option(ENABLE_SINGLE_PRECISION "Enable FFTW single precision" OFF)
option(ENABLE_LONG_DOUBLE_PRECISION "Enable FFTW single precision" OFF)
option(ENABLE_QUAD_PRECISION "Enable FFTW quad precision" OFF)

find_package(FFTW3 REQUIRED CONFIG)

add_executable(${PROJECT_NAME} test_package.c)
target_link_libraries(${PROJECT_NAME}
  $<$<BOOL:${ENABLE_DOUBLE_PRECISION}>:FFTW3::fftw3>
  $<$<BOOL:${ENABLE_SINGLE_PRECISION}>:FFTW3::fftw3f>
  $<$<BOOL:${ENABLE_LONG_DOUBLE_PRECISION}>:FFTW3::fftw3l>
  $<$<BOOL:${ENABLE_QUAD_PRECISION}>:FFTW3::fftw3q>)

target_compile_options(${PROJECT_NAME} PRIVATE
    $<$<BOOL:${ENABLE_SINGLE_PRECISION}>:-DENABLE_SINGLE_PRECISION=1>
    $<$<BOOL:${ENABLE_LONG_DOUBLE_PRECISION}>:-DENABLE_LONG_DOUBLE_PRECISION=1>
    $<$<BOOL:${ENABLE_QUAD_PRECISION}>:-DENABLE_QUAD_PRECISION=1>)
