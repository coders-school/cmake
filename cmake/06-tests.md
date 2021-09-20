<!-- .slide: data-background="#111111" -->

# `cmake`

## Testy

<a href="https://coders.school">
    <img width="500" src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Dodawanie testów do `ctest`

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

### Zadanie
<!-- .element: class="fragment fade-in" -->

Dodaj binarkę z testami, która powinna być odpalana za pomocą `ctest`
<!-- .element: class="fragment fade-in" -->

___

## Budowanie w trybie debug

Domyślnie budowany jest tryb "Release" (bez symboli debugowania)
<!-- .element: class="fragment fade-in" -->

```cmake
cmake -DCMAKE_BUILD_TYPE=Debug ..
```
<!-- .element: class="fragment fade-in" -->

Jeśli chcemy wspierać budowanie w trybach Debug i Release powinniśmy mieć do nich oddzielne katalogi z rezultatami budowania
<!-- .element: class="fragment fade-in" -->

```bash
mkdir buildDebug
cd buildDebug
cmake -DCMAKE_BUILD_TYPE=Debug ..
cmake --build .
```
<!-- .element: class="fragment fade-in" -->

___

## Linki dla poszerzenia wiedzy

* [CMake - from zero to something - prezentacja z Wro.cpp](https://muttleyxd.github.io)
* [19 reasons why CMake is actually awesome](https://kubasejdak.com/19-reasons-why-cmake-is-actually-awesome)
* [Modern CMake is like inheritance](https://kubasejdak.com/modern-cmake-is-like-inheritance)
* [CMake basics](https://www.siliceum.com/en/blog/post/cmake_01_cmake-basics)
