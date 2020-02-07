cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
SET(CMAKE_CUDA_COMPILER /usr/local/cuda-9.0/bin/nvcc)
SET(CMAKE_CUDA_COMPILER_ENV_VAR /usr/local/cuda-9.0/bin/nvcc)
project(CUDA_Test_Clion LANGUAGES CXX CUDA)
project(cuda_base CXX CUDA)

if ($ENV{CLION_IDE})
    include_directories("/usr/local/cuda-9.0/include")
endif ()

set(CMAKE_CXX_STANDARD 11)
add_library(cuda_base
        cudaMain.cu cudaMain.h
        vecAdd.cu vecAdd.h
        dummy.cpp cudaHeaders.h)
target_compile_features(cuda_base PUBLIC cxx_std_11)
set_target_properties( cuda_base
        PROPERTIES CUDA_SEPARABLE_COMPILATION ON
        )


set(CMAKE_CUDA_FLAGS "${CMAKE_CUDA_FLAGS} -gencode=arch=compute_62,code=sm_62")

add_executable(CUDA_Test_Clion
        main.cpp
        )

set_target_properties(
        CUDA_Test_Clion
        PROPERTIES
            CUDA_SEPARABLE_COMPILATION ON
    )
target_link_libraries(CUDA_Test_Clion cuda_base)
