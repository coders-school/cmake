<!-- .slide: data-background="#111111" -->

# `cmake`

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## CMake

* <!-- .element: class="fragment fade-in" --> automatyzuje proces budowania dla C/C++
* <!-- .element: class="fragment fade-in" --> obsługuje generowanie projektów dla wielu IDE
* <!-- .element: class="fragment fade-in" --> może składać się z wielu modułów, które się łączy (odpowiednik #include)
* <!-- .element: class="fragment fade-in" --> niezależny od platformy (jeśli jest dobrze napisany)
* <!-- .element: class="fragment fade-in" --> konfiguracja budowania w pliku CMakeLists.txt
* <!-- .element: class="fragment fade-in" --> generuje system budowania (np. pliki Makefile)

___

## Minimalny `CMakeLists.txt`

```cmake
cmake_minimum_required(VERSION 3.10)
project(ProjectName)

add_executable(execName main.cpp file.cpp)
```

___

## Budowanie za pomocą CMake'a

```bash
mkdir build     # tworzymy katalog z wynikami budowania
cd build        # wchodzimy do tego katalogu
cmake ..        # generujemy system budowania podając ścieżkę do pliku CMakeLists.txt
cmake --build . # budujemy projekt
```

`cmake --build` można zamienić na `make` jeśli wiemy, że na pewno generujemy Makefile.
<!-- .element: class="fragment fade-in" -->

`cmake --build` jest uniwersalne.
<!-- .element: class="fragment fade-in" -->

___

## Zadanie

Napisz prosty CMakeLists.txt dla programu z katalogu `greeter`, zbuduj go za pomocą `cmake` i uruchom.

Zauważ, że są tutaj też testy. Dopisz dodatkowy target dla testów.

___

## Q&A

___

## CMake - zmienne

Zmienne tworzymy za pomocą komendy `set`
<!-- .element: class="fragment fade-in" -->

```cmake
set(VARIABLE value)  # Konwencja - UPPERCASE_WITH_UNDERSCORE
```
<!-- .element: class="fragment fade-in" -->

Przykładowo
<!-- .element: class="fragment fade-in" -->

```cmake
set(NAME TheGreatestProject)
```
<!-- .element: class="fragment fade-in" -->

Odnosimy się do nich później obejmując w nawiasy `{}` i poprzedzając znakiem `$`
<!-- .element: class="fragment fade-in" -->

```cmake
add_executable(${NAME} main.cpp)
```
<!-- .element: class="fragment fade-in" -->

Spowoduje to utworzenie targetu `TheGreatestProject`, w ramach którego skompilowany zostanie plik `main.cpp`
<!-- .element: class="fragment fade-in" -->

___

## CMake - predefiniowane zmienne

CMake domyślnie dostarcza kilka zmiennych. Odwoływanie się do nich bezpośrednio lub ich modyfikacja zazwyczaj nie są uznawane za dobre praktyki.
<!-- .element: class="fragment fade-in" -->

Możemy za to bez większych problemów wykorzystać zmienną `${PROJECT_NAME}`. Zawiera ona nazwę projektu zdefiniowaną przez komendę `project()`
<!-- .element: class="fragment fade-in" -->

```cmake
project(vectorFunctions)
add_executable(${PROJECT_NAME} main.cpp vectorFunctions.cpp)
```
<!-- .element: class="fragment fade-in" -->

___

## Tworzenie aplikacji i bibliotek

[CMake manual](https://cmake.org/cmake/help/latest/manual/cmake-commands.7.html#id4)

Poniższe komendy możesz potraktować jako "konstruktory". Tworzą one "targety".

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

Powielona lista plików w różnych "targetach"
<!-- .element: class="fragment fade-in" -->

___

### Problem #1

Powielona lista plików w różnych "targetach"

### Rozwiązanie
<!-- .element: class="fragment fade-in" -->

Wrzucenie listy plików do zmiennej
<!-- .element: class="fragment fade-in" -->

## Zadanie
<!-- .element: class="fragment fade-in" -->

Wrzuć listę plików do zmiennej i skorzystaj z niej
<!-- .element: class="fragment fade-in" -->

___

### Problem #2

Drobne różnice w plikach pomiędzy targetami
<!-- .element: class="fragment fade-in" -->

### Rozwiązanie
<!-- .element: class="fragment fade-in" -->

Utworzenie biblioteki
<!-- .element: class="fragment fade-in" -->

___

## Biblioteki

Moja definicja biblioteki - zlepek wielu plików cpp bez funkcji `main()`. Biblioteki nie można z tego powodu uruchomić.
<!-- .element: class="fragment fade-in" -->

### Analogia do programowania obiektowego
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> Biblioteka = klasa (bazowa)
  * <!-- .element: class="fragment fade-in" --> pola, metody = pliki cpp
* <!-- .element: class="fragment fade-in" --> Binarka = klasa pochodna
  * <!-- .element: class="fragment fade-in" --> finalna, nie można po niej dziedziczyć
* <!-- .element: class="fragment fade-in" --> Linkowanie = dziedziczenie
  * <!-- .element: class="fragment fade-in" --> zlinkowanie binarki z biblioteką oznacza dorzucenie do niej kodu z biblioteki
  * <!-- .element: class="fragment fade-in" --> biblioteki można ze sobą wzajemnie linkować

___

## Linkowanie bibliotek

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

### Zadanie
<!-- .element: class="fragment fade-in" -->

Utwórz bibliotekę, która będzie zawierać powtarzające się pliki cpp i zlinkuj z nią targety, które ich używały.
<!-- .element: class="fragment fade-in" -->

___

## Flagi kompilacji

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

### Zadanie
<!-- .element: class="fragment fade-in" -->

Dodaj flagi kompilacji `-Wall -Wextra -Werror -pedantic -Wconversion -O3` do projektu greeter
<!-- .element: class="fragment fade-in" -->

___

## Włączanie standardu C++17

```cmake
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
```
<!-- .element: class="fragment fade-in" -->

Powyższe może nie działać dla MSVC.
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

### Zadanie
<!-- .element: class="fragment fade-in" -->

Włącz standard C++17 w projekcie greeter
<!-- .element: class="fragment fade-in" -->

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
cmake --build
```
<!-- .element: class="fragment fade-in" -->

___

## Linki dla poszerzenia wiedzy

* [CMake - from zero to something - prezentacja z Wro.cpp](https://muttleyxd.github.io)
* [19 reasons why CMake is actually awesome](https://kubasejdak.com/19-reasons-why-cmake-is-actually-awesome)
* [Modern CMake is like inheritance](https://kubasejdak.com/modern-cmake-is-like-inheritance)
* [CMake basics](https://www.siliceum.com/en/blog/post/cmake_01_cmake-basics)

___

## Q&A
