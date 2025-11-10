# Program Structure

## Program Entry Point: The `main` Function

**Explanation:** In the hosted (standard OS) environment for the C language, a function named `main` is the designated start of the program.
**Syntax examples:**

```c
int main(void) {
    // code
    return 0;
}
```

or

```c
int main(int argc, char *argv[]) {
    // code
    return 0;
}
```

**Note:** A return value of `0` typically indicates success.  
**Example full program:**

```c
#include <stdio.h>

int main(void) {
    printf("Hello, world!\n");
    return 0;
}
```

---

## Role of Header Files in Modular C Programs

**Explanation:** Header files in C declare functions, types, macros and other interfaces so that source files know how to call library functions or link with other modules. For example `#include <stdio.h>` gives you the declaration of `printf`.
**Example usage:**

```c
#include <stdio.h>
#include "my_module.h"  // your own header
```

**Best practice note:** Use `<…>` for system/library headers, `"` for your own headers; wrap your own header’s contents in include guards or `#pragma once`.

---

## Comment Syntax and Usage in C

**Explanation:** Comments are ignored by the compiler and are used to document code, explain logic, or temporarily disable code.
**Types:**

* Single‐line comment:

  ```c
  // This is a single‐line comment
  ```
* Multi‐line (block) comment:

  ```c
  /* This is a
     multi‐line comment */
  ```

**Note:** Single‐line `//` comments were formally added in C99 standard.
**Example in context:**

```c
#include <stdio.h>

int main(void) {
    // Print greeting
    printf("Hello, world!\n");  /* end‐of‐line comment */
    return 0;  // indicate success
}
```

---

## Program Termination and Return Values

**Explanation:** In `int main()` the return value is passed back to the host environment (operating system). A return value of `0` conventionally means success, nonzero means error.
**Important note:** Since C99, if control reaches the end of `main()` without a `return`, it is as if `return 0;` was executed.
**Example:**

```c
int main(void) {
    // ... your code
    return 0;  // success
}
```

---
