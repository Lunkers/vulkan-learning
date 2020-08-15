cmake_minimum_required(VERSION 3.11)
project(vulkan_learning VERSION 1.0 DESCRIPTION "simple project for learning vulkan" LANGUAGES CXX)


set (CMAKE_CXX_STANDARD 11)
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

add_executable(vulkanLearning src/main.cpp src/math.cpp )

find_package(Vulkan REQUIRED)
if(Vulkan_FOUND)
    message(STATUS "Vulkan found!")
    include_directories(${Vulkan_INCLUDE_DIR})
    target_include_directories(vulkanLearning PUBLIC ${Vulkan_INCLUDE_DIRS})
endif(Vulkan_FOUND)

find_package(glfw3 3.2 REQUIRED)
if(glfw3_FOUND)
    message(STATUS "GLFW found!")
    include_directories(vulkanLearning ${GLFW_INCLDUE_DIRS})
else()
    message(STATUS "could not find GLFW!")
endif(glfw3_FOUND)

target_include_directories(vulkanLearning PUBLIC external)
target_compile_features(vulkanLearning PUBLIC cxx_std_11)
target_link_libraries(vulkanLearning PUBLIC ${Vulkan_LIBRARY} glfw)

