cmake_minimum_required(VERSION 3.13)

#Insert your project name here
#project("<nazwa_projektu>" LANGUAGES CXX)
project("testproj" LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)                  # Enforcing C++17
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_DIR "src")
set(INCLUDE_DIR "include")

file(GLOB includes "${INCLUDE_DIR}/*.hpp" "${INCLUDE_DIR}/*.h")
file(GLOB sources "${SRC_DIR}/*.cpp")

# Main compilation target
add_executable(${PROJECT_NAME} ${sources} ${includes})

# Includes
target_include_directories(${PROJECT_NAME} PUBLIC ${INCLUDE_DIR})


set(OUTPUT_ARTIFACT files.tar.gz)
add_custom_command(
    TARGET ${PROJECT_NAME}
    POST_BUILD
    COMMAND tar -zcvf ${OUTPUT_ARTIFACT} ${SRC_DIR}/ ${INCLUDE_DIR}/ CMakeLists.txt
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)

add_custom_command(
    TARGET ${PROJECT_NAME}
    PRE_BUILD
    COMMAND if [ -f ${OUTPUT_ARTIFACT} ]\; then rm ${OUTPUT_ARTIFACT} \; fi
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)


