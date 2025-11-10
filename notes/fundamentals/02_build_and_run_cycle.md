# Build and Run Cycle

## Compile and Run a C program

1. Create a file `main.c`, for example:

   ```c
   #include <stdio.h>
   int main(void) {
       printf("Hello, world!\n");
       return 0;
   }
   ```
2. Compile using GCC:

   ```bash
   gcc main.c -o main
   ```
3. Run the resulting executable:

   ```bash
   ./main
   ```

### Use strict-compilation flags

To catch warnings and enforce a modern standard:

```bash
gcc main.c -o main -Wall -Wextra -pedantic -std=c11
```

* `-Wall` enables most common warnings.
* `-Wextra` enables additional warnings beyond `-Wall`.
* `-pedantic` enforces strict compliance with the C standard.
* `-std=c11` selects the C11 standard for compilation.

### Conclusion

By compiling with `gcc main.c -o main` and then `./main`, you perform the basic build-and-run cycle. Using `-Wall -Wextra -pedantic -std=c11` increases code robustness by making you aware of potential issues.

---

## Separating Source (`.c`) and Header (`.h`) Files

### Concept

* A **source file** (`.c`) contains definitions of functions, `main()`, variables, etc.
* A **header file** (`.h`) contains declarations (function prototypes, type definitions, macros) which you share across source files.

### Example

**my_funcs.h**

```c
#ifndef MY_FUNCS_H
#define MY_FUNCS_H

int add(int a, int b);

#endif
```

**my_funcs.c**

```c
#include "my_funcs.h"

int add(int a, int b) {
    return a + b;
}
```

**main.c**

```c
#include <stdio.h>
#include "my_funcs.h"

int main(void) {
    int result = add(5, 7);
    printf("Result = %d\n", result);
    return 0;
}
```

### Compile with separate files

```bash
gcc -Wall -Wextra -pedantic -std=c11 -c my_funcs.c   # produces my_funcs.o
gcc -Wall -Wextra -pedantic -std=c11 -c main.c       # produces main.o
gcc main.o my_funcs.o -o my_program                  # link to produce executable
./my_program
```

### Why separation matters

* Promotes modularity and reuse.
* Reduces recompilation when only one `.c` changes.
* Clear interface vs implementation separation.
* Easier team work and large-scale projects.

---

## Understanding the Compilation Pipeline: Preprocessing → Compilation → Assembly → Linking

### Pipeline overview

When you invoke `gcc main.c -o main`, under the hood there are typically **four** major stages:

1. **Preprocessing**; handles `#include`, `#define`, and other preprocessor directives.
2. **Compilation**; takes the preprocessed code and translates it into assembly language for the target architecture.
3. **Assembly**; converts assembly code into machine language object files (`.o`).
4. **Linking**; combines object files (and libraries) into a final executable.

### Stopping at intermediate stages

You can inspect what each stage produces:

* Preprocessing only:

  ```bash
  gcc -E main.c -o main.i
  ```

  Produces `main.i`, the preprocessed source.
* Compilation to assembly only:

  ```bash
  gcc -S main.c -o main.s
  ```

  Produces `main.s`, human-readable assembly.
* Assembly only (no linking):

  ```bash
  gcc -c main.c -o main.o
  ```

  Produces `main.o`, object file.
* Full compile + link:

  ```bash
  gcc main.c -o main
  ```

  Performs all stages and produces executable `main`.

### Example walk-through

Let’s say you have `main.c`.

1. `gcc -E main.c -o main.i`: expand headers, macros, remove comments.
2. `gcc -S main.i -o main.s`: generate assembly code.
3. `gcc -c main.s -o main.o`: convert assembly to object code.
4. `gcc main.o -o main`: link object file into executable.

### Why this matters for OS-level / systems programming

* Understanding each stage helps you catch errors (macros not expanded, missing function definitions, linker errors).
* When writing low-level code (bootloader, kernel) you might stop before linking or use custom linkers.
* When using separate source/header files you’ll understand how the linker resolves symbols across modules.

### Conclusion

The build pipeline is essential to understand how your `.c` file becomes machine code and finally an executable. Knowing `-E`, `-S`, `-c`, and full command usage gives you full visibility into what the compiler is doing.

---
