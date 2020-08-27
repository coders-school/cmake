<!-- .slide: data-background="#111111" -->

# Narzędzia #3

## Podsumowanie

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Co pamiętasz z dzisiaj?

### Napisz na czacie jak najwięcej haseł
<!-- .element: class="fragment fade-in" -->

___

### Pre-work

* Poczytajcie o zasadach SOLID, dotyczących pisania dobrego kodu obiektowego
* Poczytajcie o zasadach dobrego kodu w C++ na [CppCoreGuidelines](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)
* Dowiedzcie się czym jest problem diamentowy na Obiektowość #4

___

### Post-work

* Dorzućcie do projektu SHM system budowania `cmake` (10 punktów, 2 za każdy podpunkt)
* Przygotujcie SHM do testowania (10 punktów, 2 za każdy podpunkt)

#### Bonus

* Dostarczenie przed niedzielą 05.07.2020 23:59 (2 punkty za zadanie, razem 4)

___

### `cmake` w SHM

* Użyjcie zmiennej `${PROJECT_NAME}`
* Lista plików cpp w zmiennej
* Wszystko poza plikiem `main.cpp` powinno kompilować się do biblioteki statycznej
* Binarka (main.cpp) powinna linkować się z powyższą biblioteką.
* Napiszcie odpowiedni plik `.github/workflows/main.yml` który spowoduje, że GitHub będzie automatycznie uruchamiał kompilację projektu dla każdego nowego commita.

___

### Podwaliny pod testy w SHM

Na podstawie lektury plików CMakeLists.txt z prac domowych wywnioskujcie, w jaki sposób dodawana jest biblioteka `gtest` do testów

* Utwórzcie proste testy do projektu SHM (co najmniej 1 test metodą Copy&Paste z innych prac domowych)
* Skopiujcie odpowiednie pliki, które pozwolą na użycie `gtesta`
* Dodajcie binarkę z testami do CMakeLists.txt. Nazwijcie ją `${PROJECT_NAME}-ut`
* Dodajcie odpalanie testów za pomocą `ctest`
* Zmodyfikujcie plik `.github/workflows/main.yml` aby GitHub dodatkowo uruchamiał jeszcze testy
