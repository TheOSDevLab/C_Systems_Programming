# C Roadmap

## Level 1: Fundamentals

* Set up a C development environment (compiler, editor, build/run cycle)
* Understand program structure: `main`, headers, compilation, linking
* Primitive types: `int`, `char`, `float`, `double`, signed/unsigned, `void`
* Variables: declaration, initialization, scope (local/global), lifetime, storage classes (auto, static, extern)
* Basic operators: arithmetic (`+ - * / %`), assignment, relational, logical, increment/decrement, type-casting
* Control flow: `if`, `if-else`, `switch`, `for`, `while`, `do-while`, `break`, `continue`
* Simple I/O: `printf`, `scanf`, understanding format specifiers
* Practice: write multiple small programs (e.g., arithmetic operations, conditional logic, loops).

---

## Level 2: Data Aggregation and Modularity

* Arrays: single and multi-dimensional, indexing, relationship to pointers
* Strings: character arrays, null termination, standard library string functions
* Functions: declaration vs definition, arguments (by value), return values, recursion
* Modular code: header files, `static` vs `extern`, splitting code into multiple `.c`/`.h` files
* Typedefs, `enum`, and simple `structs`
* Practice: build a small module with functions, arrays, strings, and structs.

---

## Level 3: Pointers, Dynamic Memory and Advanced Types

* Pointers: concept of address, `*`, `&`, pointer arithmetic, pointers and arrays, pointers to pointers
* Dynamic memory: `malloc`, `calloc`, `realloc`, `free`, memory leaks, NULL checks
* More complex `structs`: linked lists, trees, pointers inside structs
* `union` type, alignment, padding, `sizeof`, bit-fields
* Practice: implement a linked list library, with functions to add/remove nodes, traverse, free memory.

---

## Level 4: Preprocessor, File I/O, and Library Usage

* Preprocessor directives: `#define`, `#include`, conditional compilation (`#ifdef`, `#ifndef`, `#endif`)
* Macros: function-like macros, macro pitfalls, inline functions vs macros
* File I/O: `fopen`, `fclose`, `fread`, `fwrite`, `fprintf`, `fscanf`, binary vs text mode
* Error handling: return codes, `errno`, `perror`, assertions (`assert.h`)
* Standard library usage: `<stdlib.h>`, `<string.h>`, `<stdio.h>`, `<ctype.h>`, `<math.h>`
* Practice: write a simple library to read data files, process data, and write results; include proper error handling.

---

## Level 5: Efficiency, Robustness and Best Practices

* Memory safety: avoid buffer overflows, off-by-ones, dangling pointers
* Defined vs undefined behavior: understand what is not guaranteed by the language standard.
* Performance awareness: algorithmic complexity, efficient data structures, minimize expensive operations
* Coding style and readability: naming conventions, modular design, separation of concerns
* Use of static analysis tools, debug builds, sanitizers (e.g., `-fsanitize=address`)
* Practice: refactor previous modules to improve clarity, add unit tests, measure performance of alternate implementations.

---

## Level 6: Deep C Language Features and Cross-Platform Considerations

* Pointer to function, callback patterns
* Variable-length arrays, `const` correctness, `volatile`, `restrict` qualifiers
* Bitwise operations: `&`, `|`, `^`, `~`, shifts, masking, endianness
* Portability: fixed-width types (`int32_t`, `uint64_t`), `size_t`, `ptrdiff_t`, understanding platform differences
* The C standard (C11 / C18): language features, macro semantics, translation phases
* Practice: build a small portable library that works across different architectures (e.g., 32-bit vs 64-bit) and uses fixed-width types and bitwise operations.

---

## Level 7: Large-Scale C Programming and Maintenance

* Designing libraries/APIs: header stability, versioning, ABI considerations
* Modular build systems: using `make`, proper header inclusion guards, documentation
* Code review and maintenance: readability, comments, minimal duplication, test coverage
* Legacy code understanding: reading large C codebases, understanding memory management in real systems
* Practice: pick an open-source C project, read its code, contribute a small module or fix a bug, ensure your code aligns with project style.

---

### Suggested Timeline

* Weeks 1–2: Level 1
* Weeks 3–4: Level 2
* Weeks 5–8: Level 3
* Weeks 9–12: Level 4
* Months 4–6: Level 5
* Months 6–9: Level 6
* Ongoing: Level 7

---
