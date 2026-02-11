cmake_minimum_required(VERSION 3.21)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
include(FetchContent)

project(farsounder_client_example LANGUAGES CXX)

# Fetch the SDK
if (WIN32)
    FetchContent_Declare(
        farsounder_sdk
        URL https://github.com/farsounder/farsounder-cpp-client/releases/download/v0.1.4/farsounder-sdk-windows-release.zip
        DOWNLOAD_EXTRACT_TIMESTAMP TRUE
    )
else()
    FetchContent_Declare(
        farsounder_sdk
        URL https://github.com/farsounder/farsounder-cpp-client/releases/download/v0.1.4/farsounder-sdk-ubuntu-release.zip
        DOWNLOAD_EXTRACT_TIMESTAMP TRUE
    )
endif()

FetchContent_MakeAvailable(farsounder_sdk)

list(APPEND CMAKE_PREFIX_PATH ${farsounder_sdk_SOURCE_DIR})

find_package(farsounder REQUIRED)

add_executable(farsounder_client_example basic_client.cpp)
target_link_libraries(farsounder_client_example PRIVATE farsounder::farsounder)

if(WIN32)
    # Copy farsounder.dll next to the executable
    add_custom_command(TARGET farsounder_client_example POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
                $<TARGET_RUNTIME_DLLS:farsounder_client_example>
                $<TARGET_FILE_DIR:farsounder_client_example>
        COMMAND_EXPAND_LISTS
    )
endif()
