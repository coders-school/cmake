<!-- .slide: data-background="#111111" -->

# Tools #3

## Summary

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## What do you remember from today?

### Write as many topics as possible in the chat
<!-- .element: class="fragment fade-in" -->

___

### Pre-work

* Read about the SOLID rules for writing good object-oriented code
* Read about the principles of good code in C ++ at [CppCoreGuidelines](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)
* Find out what the diamond problem is on Object Orientation #4

___

### Post-work

* Add the `cmake` building system to the SHM project (10 points, 2 for each subtask)
* Prepare SHM for testing (10 points, 2 for each subtask)

#### Bonus

* Delivery before Sunday 05.07.2020 23:59 (2 points per task, 4 in total) <!--Czy zmienić zapis daty na amerykański (07/05/2020)-->

___

### `cmake` in SHM

* Use the variable `${PROJECT_NAME}`
* List of cpp files in the variable
* Everything except `main.cpp` should compile to a static library
* Binary (main.cpp) should be linked with the above library.
* Write an appropriate file `.github/workflows/main.yml` which will cause GitHub to automatically run a project build for each new commit.

___

### The foundations for testing in SHM

On the basis of reading CMakeLists.txt files from homework, deduce how the `gtest` library is added to tests

* Create simple tests for SHM project (at least 1 test with Copy&Paste method from other homework)
* Copy the appropriate files that will allow the use of `gtest`
* Add the test binary to CMakeLists.txt. Name it `${PROJECT_NAME}-ut`
* Add test run with `ctest`
* Modify the file `.github/workflows/main.yml` so GitHub will also run tests
