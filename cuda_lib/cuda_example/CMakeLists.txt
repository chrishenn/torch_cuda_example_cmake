cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

# Create project
SET(PROJECT_NAME example_cuda)
SET(CMAKE_C_COMPILER gcc)
SET(CMAKE_CXX_COMPILER g++)
SET(CMAKE_CUDA_COMPILER nvcc)
project(${PROJECT_NAME} LANGUAGES CUDA CXX)

# LIBTORCH
FIND_PACKAGE( Torch REQUIRED )

# Source files
file(GLOB INTERNAL_SOURCE ${PROJECT_SOURCE_DIR}/*.cpp )
file(GLOB CUDA_SOURCE ${PROJECT_SOURCE_DIR}/*.cu)
file(GLOB INTERNAL_HEADERS ${PROJECT_SOURCE_DIR}/*.h )

# Define our library target
add_library(${PROJECT_NAME} SHARED ${INTERNAL_SOURCE} ${INTERNAL_HEADERS} ${CUDA_SOURCE} )
target_link_libraries(${PROJECT_NAME} "${TORCH_LIBRARIES}")