cmake_minimum_required(VERSION 3.18)

project(Cpp2main)

include(FetchContent)

FetchContent_Declare(
    cppfront
    GIT_REPOSITORY https://github.com/hsutter/cppfront.git
    GIT_TAG 5b100f62aa18b4af6306aa24385c2369d75e0c36 # 2022-09-22
)

FetchContent_MakeAvailable(cppfront)

add_executable(cppfront "${cppfront_SOURCE_DIR}/source/cppfront.cpp")
target_include_directories(cppfront PUBLIC "${cppfront_SOURCE_DIR}/source")
set_target_properties(cppfront PROPERTIES CXX_STANDARD 20 CXX_STANDARD_REQUIRED True)

add_custom_command(OUTPUT main.cpp
    DEPENDS cppfront ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp2
    COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp2 ${CMAKE_CURRENT_BINARY_DIR}/
    COMMAND cppfront -p ${CMAKE_CURRENT_BINARY_DIR}/main.cpp2
    COMMAND ${CMAKE_COMMAND} -E rm ${CMAKE_CURRENT_BINARY_DIR}/main.cpp2
)

add_executable(main main.cpp)
target_include_directories(main SYSTEM PUBLIC "${cppfront_SOURCE_DIR}/include")
set_target_properties(main PROPERTIES CXX_STANDARD 20 CXX_STANDARD_REQUIRED True)