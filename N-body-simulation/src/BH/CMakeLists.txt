cmake_minimum_required(VERSION 3.18)

project(BarnesHut LANGUAGES CXX CUDA)

# Standard C++
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CUDA_STANDARD 14)

# Abilita separable compilation per device linking
set(CMAKE_CUDA_SEPARABLE_COMPILATION ON)

# Imposta architetture CUDA specifiche (sm_80 = Ampere)
set(CMAKE_CUDA_ARCHITECTURES 80)

# Trova OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# Trova OMP
find_package(OpenMP REQUIRED)

# Aggiungi i file sorgente
file(GLOB SOURCES
    *.cpp
    *.h
    *.cu
    *.cuh
)

# Crea l'eseguibile
add_executable(BarnesHut ${SOURCES})

# Abilita ottimizzazioni -O3 per tutti i linguaggi
target_compile_options(BarnesHut PRIVATE
    $<$<COMPILE_LANGUAGE:CXX>:-O3>
    $<$<COMPILE_LANGUAGE:CUDA>:-O3>
)

# Link a OpenCV e CUDA
target_link_libraries(BarnesHut PRIVATE ${OpenCV_LIBS} cuda cudart OpenMP::OpenMP_CXX)
