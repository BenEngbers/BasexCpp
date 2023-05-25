cmake_minimum_required (VERSION 3.25.1)
project (libBasexTest VERSION 1.0)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++20")
# set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_OBJCXX_STANDARD_REQUIRED ON)

file (GLOB_RECURSE SOURCES src/*.cpp)
add_executable(libBasexTest ${SOURCES})

target_include_directories(libBasexTest PUBLIC
	"${PROJECT_BINARY_DIR}"
	)

target_link_libraries(${PROJECT_NAME} PUBLIC libBasexCpp libBasexSocket)
# message(STATUS "Dir 1 : ${PROJECT_NAME} PUBLIC subproject/libBasexCpp subproject/libBasexSocket")

add_subdirectory("/home/bengbers/Thuis/C_CPP_Werkbank/libBasexCpp"    subproject/libBasexCpp)
add_subdirectory("/home/bengbers/Thuis/C_CPP_Werkbank/libBasexSocket" subproject/libBasexSocket)
add_library(BasexCpp SHARED IMPORTED)						
add_library(BasexSocket SHARED IMPORTED)			

# message(STATUS "Dir 2 : ${CMAKE_CURRENT_SOURCE_DIR}")

target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR}/../libBasexTest/src)
# message(STATUS "Dir 3 : ${PROJECT_BINARY_DIR}/../libBasexTest/src")
target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR}/../libBasexCpp/src)
# message(STATUS "Dir 3 : ${PROJECT_BINARY_DIR}/../libBasexCpp/src")
target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR}/../libBasexSocket/src)
# message(STATUS "Dir 4 : ${PROJECT_BINARY_DIR}/../libBasexSocket/src")

