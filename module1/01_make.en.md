<!-- .slide: data-background="#111111" -->

# `make`

<a href="https://coders.school">
    <img width="500" data-src="../coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## Makefiles

### The structure of the Makefile

```Makefile
VARIABLE = value

targetA: dependencyA1 dependencyA2
[TAB] command $(VARIABLE)

targetB: dependencyB1
[TAB] command
```

___

## Example - generating a presentation in LaTeX

```Makefile
TEX = pdflatex -shell-escape -interaction=nonstopmode -file-line-error
MAKE = make
CODE_DIR = src

.PHONY: all view

all: calculator pdf

view:
	evince ContractProgramming.pdf

pdf: ContractProgramming.tex
	$(TEX) ContractProgramming.tex

calculator:
	$(MAKE) -C $(CODE_DIR)
```

___

## Compilation in C++

### Do you remember the build phases?
<!-- .element: class="fragment fade-in" -->

```Makefile
SOURCES=$(wildcard src/*.cpp)
OBJECTS=$(patsubst %.cpp, %.o, $(SOURCES))

main: $(OBJECTS)
	g++ $^ -o $@

$(OBJECTS): src/%.o : src/%.cpp src/%.hpp
	g++ -c $< -o $@
```
<!-- .element: class="fragment fade-in" -->

### Variables remembering the context
<!-- .element: class="fragment fade-in" -->

* <!-- .element: class="fragment fade-in" --> <code>$@</code> - the name of the target file in the currently running rule
* <!-- .element: class="fragment fade-in" --> <code>$<</code> - first dependency name
* <!-- .element: class="fragment fade-in" --> <code>$^</code> - list of all dependencies (includes any duplicates)
* <!-- .element: class="fragment fade-in" --> <code>$?</code> - a list of all dependencies that are newer than target

___

## Exercise

In the greeter directory you will find a small program. Familiarize yourself with its code.

* Compile the program from the command line and run it.
* Write a simple Makefile for this program. Build it with `make` and run it.

### Spell of building

```bash
g++ -std=c++17 -Wall -Werror -Wextra -pedantic *.cpp -o greeter
./greeter
```

___

## `make` command

* <!-- .element: class="fragment fade-in" --> by default it looks for a Makefile in the current directory
* <!-- .element: class="fragment fade-in" --> automates activities by executing recipes saved in Makefile files
* <!-- .element: class="fragment fade-in" --> executes the first recipe by default
* <!-- .element: class="fragment fade-in" --> allows for conditional performance of activities
* <!-- .element: class="fragment fade-in" --> allows defining many dependencies
* <!-- .element: class="fragment fade-in" --> by default, it takes into account dependency modification dates and on this basis decides whether to execute a given recipe

___

## Q&A

### links

[cpp-polska.pl](https://cpp-polska.pl/post/potwor-przeszlosci-makefile-cz-2)
