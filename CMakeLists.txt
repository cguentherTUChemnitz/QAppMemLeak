
cmake_minimum_required (VERSION 2.8)

project(QApplicationMemLeak)



if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  # using Clang
  #disable currently unavoidable warnings
  #enable all warning and error flags
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -Wextra")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  # using GCC
  #enable all warning and error flags
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -Wextra")
endif()

option(USE_ADDRESS_SANITZER "build application with activated address sanitizer" ON) # OFF is the default
if(USE_ADDRESS_SANITZER)
  set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -fsanitize=address -fno-omit-frame-pointer")
  set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -fsanitize=address")
  set(ENV{ASAN_SYMBOLIZER_PATH} /usr/bin/llvm-symbolizer) #for clang
  set(ENV{ASAN_OPTIONS} symbolize=1) #for g++
endif(USE_ADDRESS_SANITZER)


# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)
# Find the Qt libraries
find_package(Qt5Core REQUIRED)
find_package(Qt5Widgets REQUIRED)
ADD_DEFINITIONS(${QT_DEFINITIONS})



add_executable(qappMemLeak main.cpp)

qt5_use_modules(qappMemLeak Core Widgets)