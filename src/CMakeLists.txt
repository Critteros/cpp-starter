find_package(fmt REQUIRED)
find_package(spdlog REQUIRED)
find_package(indicators REQUIRED)
find_package(Boost REQUIRED)


# Generic test that uses conan libs
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(
  ${PROJECT_NAME}
  PRIVATE project_options
          project_warnings
          fmt::fmt
          spdlog::spdlog
          Boost::locale
)

target_include_directories(${PROJECT_NAME} SYSTEM
 PRIVATE "../submodules/indicators/include")