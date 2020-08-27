<!-- .slide: data-background="#111111" -->

# `cmake`

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## CMake

* <!-- .element: class="fragment fade-in" --> automates the build process for C/C++
* <!-- .element: class="fragment fade-in" --> supports generating projects for multiple IDEs
* <!-- .element: class="fragment fade-in" --> can consists of many modules that are combined (equivalent of #include)
* <!-- .element: class="fragment fade-in" --> platform independent (if well written)
* <!-- .element: class="fragment fade-in" --> build configuration in CMakeLists.txt file
* <!-- .element: class="fragment fade-in" --> generate a build systems (e.g. Makefiles)

___

## Minimal `CMakeLists.txt`

```cmake
cmake_minimum_required(VERSION 3.10)
project(ProjectName)

add_executable(execName main.cpp file.cpp)
```

___

## Building with CMake'a

```bash
mkdir build     # create a directory with the results of the building
cd build        # enter this directory
cmake ..        # generate the build system by specifying the path to the CMakeLists.txt file
cmake --build . # build a project
```

`cmake --build` can be changed for `make` if we're sure, that we're generating Makefile.
<!-- .element: class="fragment fade-in" -->

`cmake --build` is universal.
<!-- .element: class="fragment fade-in" -->

___

## Exercise

Write simple CMakeLists.txt for program from `greeter` directory, build it with `cmake` and run.

Notice that there are also tests. Write additional target for tests.

___

## Q&A

___

## CMake - variables

Variables are created with `set` command
<!-- .element: class="fragment fade-in" -->

```cmake
set(VARIABLE value)  # Convention - UPPERCASE_WITH_UNDERSCORE
```
<!-- .element: class="fragment fade-in" -->

For example
<!-- .element: class="fragment fade-in" -->

```cmake
set(NAME TheGreatestProject)
```
<!-- .element: class="fragment fade-in" -->

We refer to them later by enclosing them in `{}` parentheses and preceding them with the `$` sign
<!-- .element: class="fragment fade-in" -->

```cmake
add_executable(${NAME} main.cpp)
```
<!-- .element: class="fragment fade-in" -->

That will create a target `TheGreatestProject` in which `main.cpp` file will be compiled
<!-- .element: class="fragment fade-in" -->

___

## CMake - predefined variables

CMake supplies several variables by default. Referring to them directly or modifying them is usually not considered good practice.
<!-- .element: class="fragment fade-in" -->

We can use the `$ {PROJECT_NAME}` variable without any problems. It contains the project name defined by the `project ()` command
<!-- .element: class="fragment fade-in" -->

```cmake
project(vectorFunctions)
add_executable(${PROJECT_NAME} main.cpp vectorFunctions.cpp)
```
<!-- .element: class="fragment fade-in" -->

___

## Create applications and libraries

[CMake manual](https://cmake.org/cmake/help/latest/manual/cmake-commands.7.html#id4)

You can treat the following commands as "constructors". They form "targets"

```cmake
add_executable(<name> [source1] [source2 ...])
```

```cmake
add_library(<name> [STATIC | SHARED | MODULE] [source1] [source2 ...])
```

```cmake
add_library(${PROJECT_NAME}-lib STATIC functions.cpp modules.cpp)
add_executable(${PROJECT_NAME} main.cpp functions.cpp modules.cpp)
add_executable(${PROJECT_NAME}-ut test.cpp functions.cpp modules.cpp)
```
<!-- .element: class="fragment fade-in" -->

### Problem
<!-- .element: class="fragment fade-in" -->

Duplicated list of files in different "targets"
<!-- .element: class="fragment fade-in" -->

___

### Problem #1

Duplicated list of files in different "targets"

### Solution
<!-- .element: class="fragment fade-in" -->

Putting a list of files into a variable
<!-- .element: class="fragment fade-in" -->

## Exercise
<!-- .element: class="fragment fade-in" -->

Put a list of files into a variable and use it
<!-- .element: class="fragment fade-in" -->

___

### Problem #2

Minor differences in files between targets
<!-- .element: class="fragment fade-in" -->

### Solution
<!-- .element: class="fragment fade-in" -->

Creating a library
<!-- .element: class="fragment fade-in" -->

___

## Libraries

My library definition - a cluster of multiple cpp files without the `main ()` function. Therefore, the library cannot be run.
<!-- .element: class="fragment fade-in" -->

### Analogy to object oriented programming
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> Library = class (base)
  * <!-- .element: class="fragment fade-in" --> fields, methods = cpp files
* <!-- .element: class="fragment fade-in" --> Binary = derived class
  * <!-- .element: class="fragment fade-in" --> final, cannot be inherited from it
* <!-- .element: class="fragment fade-in" --> Linking = inheritance
  * <!-- .element: class="fragment fade-in" --> linking a binary to a library means adding code from the library to it
  * <!-- .element: class="fragment fade-in" --> libraries can be linked with each other

___

## Linking libraries

```cmake
target_link_libraries(<target> ... <item>... ...)
```
<!-- .element: class="fragment fade-in" -->

```cmake
add_library(lib STATIC functions.cpp modules.cpp)
add_executable(main main.cpp)
add_executable(ut tests.cpp)
target_link_libraries(main lib)
target_link_libraries(ut lib)
```
<!-- .element: class="fragment fade-in" -->

### Exercise
<!-- .element: class="fragment fade-in" -->

Create a library that will contain duplicate cpp files and link to it with the targets that used them.
<!-- .element: class="fragment fade-in" -->

___

## Build flags

```cmake
target_compile_options(<target> [BEFORE]
                                <INTERFACE|PUBLIC|PRIVATE> [items1...]
                                [<INTERFACE|PUBLIC|PRIVATE> [items2...]
                                ...])
```
<!-- .element: class="fragment fade-in" -->

```cmake
add_executable(${PROJECT_NAME} main.cpp)
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Werror)
```
<!-- .element: class="fragment fade-in" -->

### Exercise
<!-- .element: class="fragment fade-in" -->

Add build flags `-Wall -Wextra -Werror -pedantic -Wconversion -O3` to the greeter project
<!-- .element: class="fragment fade-in" -->

___

## Enabling the C ++ 17 standard

```cmake
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
```
<!-- .element: class="fragment fade-in" -->

The above may not work for MSVC.
<!-- .element: class="fragment fade-in" -->

```cmake
set_target_properties(${PROJECT_NAME} PROPERTIES
                      CXX_STANDARD 17
                      CXX_STANDARD_REQUIRED ON)
```
<!-- .element: class="fragment fade-in" -->

```cmake
add_executable(${PROJECT_NAME} main.cpp)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)
```
<!-- .element: class="fragment fade-in" -->

### Exercise
<!-- .element: class="fragment fade-in" -->

Enable the C++17 standard in the greeter project
<!-- .element: class="fragment fade-in" -->

___

## Adding tests to `ctest`

```cmake
enable_testing()
add_test(NAME <name> COMMAND <command> [<arg>...])
```
<!-- .element: class="fragment fade-in" -->

```cmake
enable_testing()
add_test(NAME someTests COMMAND ${PROJECT_NAME}-ut)
```
<!-- .element: class="fragment fade-in" -->

### Exercise
<!-- .element: class="fragment fade-in" -->

Add a test binary that should be run with `ctest`
<!-- .element: class="fragment fade-in" -->

___

## Build in debug mode

By default, the "Release" mode is built (no debugging symbols)
<!-- .element: class="fragment fade-in" -->

```cmake
cmake -DCMAKE_BUILD_TYPE=Debug ..
```
<!-- .element: class="fragment fade-in" -->

If we want to support building in Debug and Release modes, we should have separate directories with build results
<!-- .element: class="fragment fade-in" -->

```bash
mkdir buildDebug
cd buildDebug
cmake -DCMAKE_BUILD_TYPE=Debug ..
cmake --build
```
<!-- .element: class="fragment fade-in" -->

___

## Links for learning more

* [CMake - from zero to something - prezentacja z Wro.cpp](https://muttleyxd.github.io)
* [19 reasons why CMake is actually awesome](https://kubasejdak.com/19-reasons-why-cmake-is-actually-awesome)
* [Modern CMake is like inheritance](https://kubasejdak.com/modern-cmake-is-like-inheritance)
* [CMake basics](https://www.siliceum.com/en/blog/post/cmake_01_cmake-basics)

___

## Q&A
