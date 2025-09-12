cmake_minimum_required(VERSION 3.18)

project(DirectSum LANGUAGES CXX CUDA)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CUDA_STANDARD 14)

# Imposta architetture CUDA specifiche (sm_80 = Ampere)
set(CMAKE_CUDA_ARCHITECTURES 80)

# Trova OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# Trova OMP
find_package(OpenMP REQUIRED)

# Add source files
file(GLOB SOURCES *.h *.cu)

# Add the executable
add_executable(DirectSum ${SOURCES})

# Abilita ottimizzazioni -O3 per tutti i linguaggi
target_compile_options(DirectSum PRIVATE
    $<$<COMPILE_LANGUAGE:CXX>:-O3>
    $<$<COMPILE_LANGUAGE:CUDA>:-O3>
)

# Link GLFW and OpenGL libraries
target_link_libraries(DirectSum PRIVATE ${OpenCV_LIBS} OpenMP::OpenMP_CXX)