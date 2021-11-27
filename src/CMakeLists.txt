find_package(fmt)
find_package(spdlog)


# Generic test that uses conan libs
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(
  ${PROJECT_NAME}
  PRIVATE project_options
          project_warnings
          fmt::fmt
          spdlog::spdlog)
