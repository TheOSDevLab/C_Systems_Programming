# GCC Installation

## Installing GCC for regular C programming

### Prerequisites

* A Linux system (e.g., Debian/Ubuntu, Fedora/RHEL, etc.).
* A user account with **sudo** privileges (or root access).
* Internet access to fetch packages or sources.
* Some free disk space (compiler + libraries ≈ hundreds of MB).
* Basic shell/terminal familiarity.

### Installation via package manager (recommended)

For most purposes you simply install GCC from your distribution’s package repository.

**On Debian/Ubuntu-based systems:**

```bash
sudo apt update
sudo apt install build-essential    # this includes gcc, g++, libc headers, etc.
```

After installation verify by:

```bash
gcc --version
```

This method is the fastest and most reliable.

**On RPM-based (Fedora/RHEL) systems:**

```bash
sudo dnf install gcc gcc-c++     # or yum on older systems
```

Or in general:

```bash
sudo yum install gcc     # for older CentOS/RHEL
```

### Test that installation works

Create a simple C file, e.g., `hello.c`:

```c
#include <stdio.h>

int main(void) {
    printf("Hello, world!\n");
    return 0;
}
```

Compile and run:

```bash
gcc hello.c -o hello
./hello
```

If you see “Hello, world!” printed, your tool-chain works.

### (Optionally) Install a specific version or build from source

If you need a newer or specific version of GCC beyond what your distro provides:

* Some repositories (e.g., PPAs for Ubuntu) allow installing multiple GCC versions.
* Alternatively you can build GCC from source following the official instructions at the GNU Project site.

  * You will need dependencies like `libgmp-dev`, `libmpfr-dev`, `libmpc-dev`.
  * The install process involves `configure`, `make`, `make install`.

### Conclusion

By completing this section you now have a working GCC compiler on your Linux system. You can compile, link, and run standard C programs. This covers almost all general C development tasks. For OS development (kernel/bootloader/firmware) you’ll likely need a different tool-chain (cross-compiler) which is covered next.

---

## Installing GCC cross-compiler for OS development

When you are developing an operating system (or low-level code) you often target a different architecture or environment than your host system. A cross-compiler allows you to compile on one platform (host) and generate code for another (target).

### Conceptual overview

* **Host**: the machine where the compiler runs (your Linux box).
* **Target**: the architecture and environment for which the compiler produces code.
* A cross-compiler is configured with a `--target=<arch-triple>` parameter so it knows which architecture to generate code for.
* For OS development you typically choose a “bare metal” or “freestanding” target (e.g., `i686-elf`, `x86_64-elf`, etc.) meaning you generate code without relying on an existing OS.
* Often you must build both binutils (assembler/linker) and GCC for the cross-target.

---

### High-level steps

Below is a typical workflow. Specific version numbers and paths may vary.

#### 1 Set up directories and variables

```bash
# Example: create a working directory
mkdir ~/osdev-cross
cd ~/osdev-cross

# Set a prefix and target
export PREFIX="$HOME/osdev-cross/tools"
export TARGET=x86_64-elf        # example for 64-bit freestanding
export PATH="$PREFIX/bin:$PATH"
```

#### 2 Download and build Binutils for the cross-target

```bash
# download binutils source (choose version)
tar xf binutils-<version>.tar.gz
cd binutils-<version>
mkdir build && cd build
../configure --target=$TARGET --prefix="$PREFIX" --with-sysroot --disable-nls --disable-werror
make
make install
cd ../../
```

This installs the assembler (`$TARGET-as`), linker (`$TARGET-ld`), etc., configured for the target architecture.

#### 3 Download and build GCC for the cross-target

```bash
# download gcc source (choose version)
tar xf gcc-<version>.tar.gz
cd gcc-<version>
# configure only the C language (for OS dev you might not need C++)
mkdir build && cd build
../configure --target=$TARGET --prefix="$PREFIX" --disable-native-language-support --enable-languages=c --without-libstdcxx-v3
make all-gcc
make all-target-libgcc
make install-gcc
make install-target-libgcc
cd ../../
```

This will produce a `gcc` executable that when invoked as, e.g., `x86_64-elf-gcc`, compiles for the target.

#### 4 Verify the cross-compiler

```bash
x86_64-elf-gcc --version
x86_64-elf-gcc -v
```

Compile a simple freestanding test (e.g., a stub .c file) and check that it produces target architecture object code (use `objdump` or similar).

---

### Using the cross-compiler in your OS-dev workflow

* When building your kernel or bootloader, set your build system to use e.g. `CROSS_COMPILE=x86_64-elf-` so that `gcc`, `ld`, `as` refer to the cross versions.
* Link in freestanding mode (`-ffreestanding`, `-nostdlib`) because you don’t have the normal host OS runtime.
* Ensure your output format (e.g., ELF) and target ABI match your OS loader expectations.

---

### Caveats and advanced notes

* Building a cross-compiler is **not strictly mandatory** for OS development if you target exactly the same architecture and environment as your host, but it is strongly recommended to avoid unintended host-dependencies.
* If you intend to support “hosted” user-space (i.e., a libc, user-mode processes) you will eventually need a more advanced “OS-specific toolchain” configured with knowledge of your OS.
* Be careful about version mismatches of binutils, GCC, and target libraries.
* Cross-compiler builds can take long, and require dependencies (e.g., GMP, MPFR, MPC libraries) when building GCC from source.

### Conclusion

By following this section you establish a compiler toolchain that runs on your host system but emits code for a different architecture + environment (typically freestanding) suited to OS development. This gives you greater control and avoids subtle issues that may arise if you accidentally use libraries or runtime features tied to your host OS.

---
