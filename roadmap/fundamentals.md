# Fundamentals

## Environment Setup

* **Compiler:** Install GCC or Clang.  
* **Editor/IDE:** VS Code, CLion, or Vim. Enable syntax highlighting and linting.  
* **Build and Run Cycle:**
  * Compile: `gcc main.c -o main`
  * Run: `./main`
  * Use flags: `-Wall -Wextra -pedantic -std=c11` for strict compilation.
* Learn to separate source (`.c`) and headers (`.h`).
* Understand the compilation pipeline: preprocessing → compilation → assembly → linking.

---

## Program Structure

* Every C program must have a `main` function as the entry point.
* Header files (`#include <stdio.h>`) bring declarations.
* The linker combines compiled object files into one executable.
* Comments: single-line (`//`), multi-line (`/* */`).
* `return 0;` indicates successful execution.

---

## Primitive Data Types

* **Integral types:** `char`, `short`, `int`, `long`, `long long`
* **Floating types:** `float`, `double`, `long double`
* **Qualifiers:** `signed`, `unsigned`
* **Void:** represents “no type”; used for functions returning nothing or generic pointers.
* Use `sizeof(type)` to check size in bytes.
* Understand how integer overflow behaves (implementation-defined).

---

## Variables and Scope

* **Declaration vs. definition:**  
  * Declaration tells the compiler a variable exists.  
  * Definition allocates memory.
* **Initialization:** `int x = 5;`  
* **Scope:**  
  * Local (inside blocks `{}`)  
  * Global (outside all functions)  
  * File scope (`static` globals)
* **Lifetime:**  
  * Automatic (created on entry, destroyed on exit)  
  * Static (persists entire program)
* **Storage classes:**  
  * `auto` – default for local variables  
  * `register` – suggests CPU register
  * `static` – internal linkage or persistent local  
  * `extern` – external linkage across translation units

---

## Operators

* **Arithmetic:** `+`, `-`, `*`, `/`, `%`
* **Assignment:** `=`, compound forms (`+=`, `-=`, `*=`, `/=`, `%=`)  
* **Relational:** `<`, `>`, `<=`, `>=`, `==`, `!=`
* **Logical:** `&&`, `||`, `!`
* **Increment/Decrement:** `++`, `--` (prefix and postfix)
* **Bitwise:** `&`, `|`, `^`, `~`, `<<`, `>>`
* **Type casting:** `(int)3.7` → `3`
* **Operator precedence:** learn to use parentheses to clarify order.

---

## Control Flow

* **Conditional:**  
  * `if`, `if-else`, `else if`  
  * `switch-case-default` (use `break` to prevent fallthrough)
* **Loops:**  
  * `for (init; condition; update)`  
  * `while (condition)`  
  * `do { ... } while (condition);`
* **Flow control:**  
  * `break` – exits current loop or switch  
  * `continue` – skips rest of current iteration  
  * `return` – exits the current function

---

## Input and Output

* Include `<stdio.h>` for I/O functions.  
* **Output:** `printf("Sum = %d\n", sum);`  
* **Input:** `scanf("%d", &num);`  
* Understand format specifiers:
  * `%d` – `int`
  * `%f` – `float`
  * `%lf` – `double`
  * `%c` – `char`
  * `%s` – string
* Always match specifiers to variable types.
* Avoid buffer overflows when using `scanf("%s", str)`; prefer specifying limits (`%19s`).

---

## Practice Exercises

* Write programs to:
  * Compute area/perimeter of shapes.
  * Check whether a number is even/odd, prime, or palindrome.
  * Print multiplication tables.
  * Find factorial using loops.
  * Sum elements of an array entered by the user.
* Compile and run each with `-Wall -Wextra` to learn from compiler warnings.
* Use `printf` extensively to trace logic.

---

## Mastery Goals

* Comfortably write, compile, and debug small programs.  
* Understand every compiler warning.  
* Know how data moves through memory for basic types.  
* Recognize variable scope and lifetime clearly.  
* Be fluent with loops, conditions, and formatted I/O.

---
