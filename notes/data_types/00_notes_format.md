# `<DataTypeName>`

## Definition

* Fundamental integral/floating type (specify).
* Conceptual role: numeric, symbolic, or memory representation.
* Distinct from derived types (arrays, pointers, structs).
* Reference: ISO/IEC 9899 §6.2.5.

---

## Declaration and Initialization

```c
<DataTypeName> var;
<DataTypeName> var = initial_value;
```

* Compatible storage classes: automatic, static, extern, register.
* Multiple declarations: `var1, var2, var3;`
* Pitfalls: uninitialized variables, implicit signedness issues.

---

## Modifiers and Variants

* List relevant modifiers (`signed`, `unsigned`, `short`, `long`).
* Example: `signed char`, `unsigned char`.
* Notes: Not all modifiers valid for all types (e.g., `long char` invalid).

---

## Size, Range and Format Specifiers

* Typical `sizeof()` and bits (`CHAR_BIT` for `char`).
* Min/max values from `<limits.h>` or `<float.h>`.
* I/O format specifiers for `printf`/`scanf`.

Example for `char`:

```c
sizeof(char) == 1
CHAR_MIN, CHAR_MAX, SCHAR_MIN, SCHAR_MAX, UCHAR_MAX
printf("%c", c); printf("%d", (int)c);
```

---

## Operations and Promotions

* Supported operations: arithmetic, logical, bitwise, increment/decrement.
* Integer promotion and usual arithmetic conversions apply.
* Overflow/underflow behavior (wrap for unsigned, undefined for signed).
* Example:

```c
char a = 10, b = 20;
char c = a + b; // promoted to int, result cast back
```

---

## Practical Uses

* Character storage and text processing.
* Small integer storage or byte-level memory manipulation.
* Example (OS/embedded):

```c
unsigned char buf[256];
for(int i=0;i<256;i++) buf[i] = i;
```

---

## Example Code

```c
#include <stdio.h>
#include <limits.h>

int main(void) {
    char c = 'G';
    printf("Char: %c, Numeric: %d\n", c, (int)c);
    printf("Size: %zu bytes, CHAR_BIT = %d\n", sizeof(c), CHAR_BIT);
    return 0;
}
```

---

## Portability and Best Practices

* Signedness of plain `char` is implementation-defined.
* Use `signed char` or `unsigned char` for clarity.
* Prefer fixed-width types (`int8_t`, `uint8_t`) for portability.
* Avoid assuming `CHAR_BIT == 8`.

---

## Related Types

* `signed char`, `unsigned char`
* `<stdint.h>` types: `int8_t`, `uint8_t`
* Wide/Unicode characters: `wchar_t`, `char16_t`, `char32_t`

---
