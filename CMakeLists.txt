cmake_minimum_required(VERSION 3.20.0)
project(sudoku VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)

if(POLICY CMP0167)
  cmake_policy(SET CMP0167 NEW)
endif()

find_package(Qt6 REQUIRED COMPONENTS Core Widgets)
find_package(Boost REQUIRED COMPONENTS functional)

add_library(sudokusolver STATIC
  src/main_window.cpp
  src/sudoku_solver_logic.cpp
  src/window_keyboard_detect.cpp
  include/main_window.h
  include/sudoku_solver_logic.h
  include/window_keyboard_detect.h
)

target_include_directories(sudokusolver PUBLIC include)

target_link_libraries(sudokusolver
  Qt::Core
  Qt::Widgets
)

add_executable(sudoku src/main.cpp)
target_link_libraries(sudoku sudokusolver)

target_compile_features(sudokusolver PRIVATE cxx_std_17)
target_compile_features(sudoku PRIVATE cxx_std_17)
