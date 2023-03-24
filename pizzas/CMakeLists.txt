cmake_minimum_required(VERSION 3.11.0)
project(pizzas)

set(SRC
    ./src/Funghi.cpp
    ./src/Margherita.cpp
    ./src/Pizza.cpp
    ./src/Pizzeria.cpp)

set(FLAGS -Wall -Wextra -Werror -pedantic -Wconversion -O1)

add_library(${PROJECT_NAME}-lib STATIC ${SRC})
target_compile_options(${PROJECT_NAME}-lib PRIVATE ${FLAGS})
target_compile_features(${PROJECT_NAME}-lib PRIVATE cxx_std_17)

add_executable(${PROJECT_NAME} ./src/main.cpp)
target_compile_options(${PROJECT_NAME} PRIVATE ${FLAGS})
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)

add_executable(${PROJECT_NAME}-ut ./test/test_main.cpp ./test/PizzeriaTest.cpp)
target_link_libraries(${PROJECT_NAME}-ut ${PROJECT_NAME}-lib)
target_compile_options(${PROJECT_NAME}-ut PRIVATE ${FLAGS})
target_compile_features(${PROJECT_NAME}-ut PRIVATE cxx_std_17)

enable_testing()
add_test(NAME pizzasTests COMMAND ${PROJECT_NAME}-ut)
# TODO: Write proper build system :)
