# project-root/CMakeLists.txt

cmake_minimum_required(VERSION 3.5)
set(CMAKE_GENERATOR "MinGW Makefiles")
project(gray-scott-sim)
# include_directories(C:/Users/Reynaud/Desktop/gray-scott-sim/acutest-master)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 配置构建类型
set(CMAKE_CONFIGURATION_TYPES Debug Release RelWithDebInfo MinSizeRel)
if("${CMAKE_BUILD_TYPE}" STREQUAL "")
    set(CMAKE_BUILD_TYPE $ENV{CMAKE_BUILD_TYPE})
    if("${CMAKE_BUILD_TYPE}" STREQUAL "")
        set(CMAKE_BUILD_TYPE "Release")
    endif()
endif()

# 设置输出目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

# 设置编译器标志
if ("${CMAKE_C_COMPILER_ID}" STREQUAL "Clang" OR "${CMAKE_C_COMPILER_ID}" STREQUAL "GNU")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall /W4")
elseif ("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC")
    # Specify proper C runtime library:
    set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} /MTd")
    set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} /MT")
    set(CMAKE_C_FLAGS_RELWITHDEBINFO "${CMAKE_C_FLAGS_RELEASE} /MT")
    set(CMAKE_C_FLAGS_MINSIZEREL "${CMAKE_C_FLAGS_RELEASE} /MT")
endif()

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang" OR "${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall /W4")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    # Specify proper C runtime library:
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")
    set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "${CMAKE_CXX_FLAGS_RELEASE} /MT")
    set(CMAKE_CXX_FLAGS_MINSIZEREL "${CMAKE_CXX_FLAGS_RELEASE} /MT")
endif()

# if(MINGW)
#     set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")  # 或者使用 -std=c++14
# endif()

# Add the source files
# add_subdirectory(lib)  # Move this line up
add_subdirectory(tests)  # Move this line up

# Add the main executable
add_executable(main_target main.cpp)

# Enable Testing
enable_testing()

# Add testing executable 
add_executable(tests_exec gs_test1.cpp)

# Include the headers folder
target_include_directories(main_target PRIVATE include)

# Link the gray_scott_lib library
target_link_libraries(main_target PRIVATE gs)

# 添加 include 文件夹
include_directories(include)
