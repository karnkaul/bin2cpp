cmake_minimum_required(VERSION 3.24)

project(embedder VERSION "0.1.1")

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_DEBUG_POSTFIX "-d")

add_subdirectory(ext)

message(STATUS "[${PROJECT_NAME}]")

configure_file(src/build_version.hpp.in "${CMAKE_CURRENT_BINARY_DIR}/include/build_version.hpp")

add_executable(${PROJECT_NAME})

target_link_libraries(${PROJECT_NAME} PRIVATE
  klib::klib
)

if(PROJECT_IS_TOP_LEVEL)
  target_link_libraries(${PROJECT_NAME} PRIVATE
    klib::klib-warnings
    klib::klib-ndwerror
  )
endif()

target_include_directories(${PROJECT_NAME} PRIVATE
  src
  "${CMAKE_CURRENT_BINARY_DIR}/include"
)

file(GLOB_RECURSE sources LIST_DIRECTORIES false "src/*.[hc]pp")
target_sources(${PROJECT_NAME} PRIVATE
  ${sources}
)
