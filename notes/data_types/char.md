# `char`

## Definition

* `char` is a **fundamental type** in C. It is classified under the integral types (integer types) rather than floating‑point.
* Its **main purpose** is to represent character data (members of the “basic execution character set”) and also to serve as the smallest addressable storage unit (a byte) in many contexts.
* It differs from derived types like arrays, structs, pointers because `char` is a primitive scalar type: it directly holds a value rather than aggregating multiple values or pointing to another object. An array of `char` is a derived type built from `char`.
* According to the C standard (§6.2.5 “Types” in ISO/IEC 9899:2011): “Three types of char are specified: `char`, `signed char`, and `unsigned char`. The implementation shall define `char` to have the same range, representation, and behaviour as either `signed char` or `unsigned char`.”

---

## Declaration and Initialization

* Basic declaration:

  ```c
  char c;
  ```
* Optional initialization examples:

  ```c
  char letter = 'A';
  char digit  = '3';
  char zero   = 0;          /* numeric zero */
  char newline = '\n';      /* escape sequence */
  ```
* Storage class specifiers apply as usual (e.g., `static`, `extern`, `auto`, `register`):

  ```c
  static char global_char = 'G';
  extern char external_char;
  auto char local_char;      /* in C89 this is implied in block scope */
  ```
* Multi‑variable declaration example:

  ```c
  char a = 'x', b = 'y', c = '\0';
  ```
* Common pitfalls to avoid:

  * Assuming `char` is always signed or always unsigned—this is implementation‑defined.
  * Using `char` for numeric calculations when you really need a signed or unsigned integer type and expect precise behaviour.
  * Relying on `sizeof(char)` being 1 but also assuming that means 8 bits—while `sizeof(char)` is always 1, the number of bits (`CHAR_BIT`) may differ.

---

## Modifiers and Variants

* Valid modifiers/variants for `char` in C:

  * `signed char`; explicitly a signed variant
  * `unsigned char`; explicitly an unsigned variant
  * Plain `char`; distinct type, implementation-defined whether signed or unsigned
* What each variant guarantees:

  * `signed char` is guaranteed to represent negative values (e.g., -128 to +127 for 8-bit).
  * `unsigned char` is guaranteed to represent non‑negative values only (0 to 255 for 8-bit).
  * `char` has the same representation and range as either `signed char` or `unsigned char`, but which one is used is implementation-defined.
* Invalid or unsupported modifiers:

  * `short char` or `long char`
  * `unsigned signed char`
  * Declaring `char` with both `signed` and `unsigned` simultaneously
* Although `char`, `signed char`, and `unsigned char` share size and alignment, they are **distinct types**.

---

## Size, Range and Format Specifiers

* `sizeof(char)` is always 1.
* The number of bits in a `char` is given by the macro `CHAR_BIT` defined in `<limits.h>` (must be ≥8).
* Typical size: On most platforms, `CHAR_BIT = 8`.
* Minimum and maximum values (macros in `<limits.h>`):

  * `SCHAR_MIN`, `SCHAR_MAX` for `signed char` (e.g., −128 to +127)
  * `UCHAR_MAX` for `unsigned char` (0 to 255)
  * `CHAR_MIN`, `CHAR_MAX` for plain `char` (depends on signedness)
* Format specifiers:

  * Print character: `printf("%c", c);`
  * Print numeric value: cast to `int` and use `%d` or `%u`
  * Read character: `scanf("%c", &c);`

Example:

```c
#include <limits.h>
printf("CHAR_BIT = %d\n", CHAR_BIT);
printf("CHAR_MIN = %d\n", CHAR_MIN);
printf("CHAR_MAX = %d\n", CHAR_MAX);
```

---

## Operations and Promotions

* Supports arithmetic (`+`, `-`, `*`, `/`), relational (`<`, `>`, `==`, `!=`), logical (`&&`, `||`, `!`), bitwise (`&`, `|`, `^`, `~`, `<<`, `>>`) operations.
* Increment/decrement: `c++`, `c--`, `++c`, `--c`.
* Integer promotions: `char` is promoted to `int` (or `unsigned int`) in expressions if its width is smaller than `int`.
* Overflow/underflow behavior:

  * `unsigned char`: modulo wrapping.
  * `signed char`: overflow is undefined behaviour.
  * Plain `char`: behavior depends on implementation.

Example of promotion:

```c
char a = 50, b = 60;
char c = a + b; // a + b promoted to int, result converted back to char
```

---

## Practical Uses

* Representing characters in strings: `char s[] = "Hello";`
* Representing small integer values in memory-efficient buffers.
* Representing raw bytes for binary data, memory buffers, and I/O streams.

Example:

```c
#include <stdio.h>

int main(void) {
    char c = 'Z';
    printf("Character: %c\n", c);
    printf("As integer: %d\n", (int)c);

    unsigned char u = 200u;
    printf("Unsigned char as integer: %u\n", (unsigned)u);
    return 0;
}
```

---

## Example Code

```c
#include <stdio.h>
#include <limits.h>

int main(void) {
    char ch = 'A';
    printf("ch = %c, numeric value = %d\n", ch, (int)ch);

    printf("CHAR_BIT   = %d\n", CHAR_BIT);
    printf("CHAR_MIN   = %d\n", CHAR_MIN);
    printf("CHAR_MAX   = %d\n", CHAR_MAX);

    unsigned char uc = (unsigned char)UCHAR_MAX;
    printf("uc before overflow = %u\n", (unsigned)uc);
    uc = uc + 1u;
    printf("uc after overflow  = %u\n", (unsigned)uc);

    return 0;
}
```

---

## Portability and Best Practices

* Implementation-defined behaviours:

  * Plain `char` may be signed or unsigned.
  * `CHAR_BIT` may vary; must be ≥8.
* Recommended choices:

  * Use `signed char` or `unsigned char` for numeric computations.
  * Plain `char` for text.
  * For raw bytes, use `unsigned char`.
* Guidelines:

  * Avoid using plain `char` for numeric calculations if range matters.
  * Use `CHAR_BIT` instead of assuming 8 bits.
  * For text input, prefer `fgets()` over `scanf("%c")` for safety.

---

## Related Types

* Variants: `signed char`, `unsigned char`, plain `char`
* Fixed-width alternatives: `int8_t`, `uint8_t`
* Wide-character types: `wchar_t`, `char16_t`, `char32_t`
* `unsigned char` can be used to access raw object bytes safely.

---
