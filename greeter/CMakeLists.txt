cmake_minimum_required(VERSION 3.10)
project(greeter)

set(SRC
    person.cpp
    greeter.cpp)

set(FLAGS -Wall -Wextra -Werror -pedantic -Wconversion)

Include(FetchContent)

FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG        v3.2.1
)

FetchContent_MakeAvailable(Catch2)

add_library(${PROJECT_NAME}-lib STATIC ${SRC})
target_compile_options(${PROJECT_NAME}-lib PRIVATE ${FLAGS})
target_compile_features(${PROJECT_NAME}-lib PRIVATE cxx_std_17)

add_executable(${PROJECT_NAME} main.cpp)
target_compile_options(${PROJECT_NAME} PRIVATE ${FLAGS})
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)

add_executable(${PROJECT_NAME}-ut test/greeter.ut.cpp)
target_link_libraries(${PROJECT_NAME}-ut ${PROJECT_NAME}-lib Catch2::Catch2WithMain)
target_compile_options(${PROJECT_NAME}-ut PRIVATE ${FLAGS})
target_compile_features(${PROJECT_NAME}-ut PRIVATE cxx_std_17)

enable_testing()
add_test(NAME someTests COMMAND ${PROJECT_NAME}-ut)

include(Catch)
catch_discover_tests(${PROJECT_NAME}-ut)