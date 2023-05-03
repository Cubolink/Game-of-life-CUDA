cmake_minimum_required(VERSION 3.23)
project(Game_of_life_CUDA C CXX CUDA)

set(CMAKE_CXX_STANDARD 14)

if((MSCV) OR (CMAKE_CXX_COMPILER_ID STREQUAL "MSVC"))
    link_directories(
            lib/freeglut-3.0.0MSVC/x64
            lib/glew
            lib/gtest
    )
endif()

include_directories(
        "${PROJECT_SOURCE_DIR}/CudaLife/include"
        "${PROJECT_SOURCE_DIR}/CudaLifeTests/include"
        "${PROJECT_SOURCE_DIR}/include"
        ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES}
)

add_executable(tests
        "${PROJECT_SOURCE_DIR}/CudaLife/src/CudaLife.cu"
        "${PROJECT_SOURCE_DIR}/CudaLifeTests/src/BenchmarkTests.cpp"
        "${PROJECT_SOURCE_DIR}/CudaLifeTests/src/CpuLifeTests.cpp"
        "${PROJECT_SOURCE_DIR}/CudaLifeTests/src/GpuLifeTests.cpp"
        "${PROJECT_SOURCE_DIR}/CudaLifeTests/src/main.cpp "
        )

add_executable(gui
        "${PROJECT_SOURCE_DIR}/CudaLife/src/CudaLife.cu"
        "${PROJECT_SOURCE_DIR}/CudaLifeGui/src/main.cpp"
)

target_link_libraries(gui
        "freeglut.lib"
        "glew32.lib"
        "gtest.lib"
        "gtestd.lib"
)

target_link_libraries(tests
        "freeglut.lib"
        "glew32.lib"
        "gtest.lib"
        "gtestd.lib"
        )