cmake_minimum_required(VERSION 3.15)
project(test_package LANGUAGES CXX)

find_package(geotrans REQUIRED dtcc ccs CONFIG)

add_executable(${PROJECT_NAME} test_package.cpp)
target_link_libraries(${PROJECT_NAME} PRIVATE geotrans::dtcc geotrans::ccs)
