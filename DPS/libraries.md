# Chapter 41: Fundamentals of Shared Libraries

## 1. Object Libraries
- **Object libraries** contain reusable code that can be used in different programs. There are two types of object libraries: static and shared.
- Libraries help avoid rewriting functions and enable code management and reusability.

## 2. Static Libraries
- **Static libraries** (.a files) are collections of object files that are linked directly into the executable at **compile time**.
- When a static library is used, all required functions are embedded into the final executable.
- **Advantages**:
  - No dependency on external libraries at runtime.
  - Code portability as the executable is self-contained.
- **Disadvantages**:
  - **Larger executable**: Embedding all the code from the library increases the program’s size.
  - **Inflexibility**: If the library is updated, the program must be recompiled.

## 3. Overview of Shared Libraries
- **Shared libraries** (.so files) are loaded dynamically at **runtime** instead of being embedded during compile time.
- Shared libraries allow multiple programs to share the same code, resulting in **smaller executables**.
- **Advantages**:
  - **Memory efficiency**: Multiple programs share the same memory for the library, reducing memory usage.
  - **Upgradability**: Programs automatically use new versions of the library without recompiling.
- **Disadvantages**:
  - **Runtime dependencies**: Programs depend on the correct version of the shared library being available at runtime.
  - **Compatibility issues**: If a shared library is updated with incompatible changes, it can cause errors.

## 4. Creating and Using Shared Libraries
- **Creating a shared library**:
  - Shared libraries are created using position-independent code (PIC), which can be generated using the `-fPIC` flag in GCC.
  - Example:
    ```bash
    gcc -fPIC -c mylib.c
    gcc -shared -o libmylib.so mylib.o
    ```
- **Using a shared library**:
  - Use the `-l` option in GCC to link the shared library at compile time.
  - Example:
    ```bash
    gcc -o myprogram myprogram.c -L. -lmylib
    ```

## 5. Position-Independent Code (PIC)
- **Position-independent code (PIC)** allows a shared library to be loaded at different memory locations, as required by different programs.
- Without PIC, libraries would have to be loaded at fixed addresses, which isn’t feasible when multiple programs use the same library.

## 6. Shared Library Soname
- **Soname** (shared object name) is an identifier for a shared library, used for version control and backward compatibility.
- The soname remains consistent as long as the library’s interface (function signatures, etc.) doesn’t change, ensuring **binary compatibility**.
- Libraries typically have three names:
  - **Real name**: Full version name, e.g., `libmylib.so.1.2.3`.
  - **Soname**: General version, e.g., `libmylib.so.1`.
  - **Linker name**: Used during compilation, e.g., `libmylib.so`.

## 7. Useful Tools for Working with Shared Libraries
- **ldd**: Lists the shared libraries required by a program.
  - Example: `ldd myprogram`
- **ldconfig**: Configures and maintains the shared library cache.
  - Example: `ldconfig /usr/local/lib`
- **nm**: Lists symbols (functions, variables) in a library.
  - Example: `nm libmylib.so`

## 8. Shared Library Versions and Naming Conventions
- Libraries use different names to manage versions:
  - **Real name**: Full version, e.g., `libmylib.so.1.2.3`.
  - **Soname**: Used for linking, e.g., `libmylib.so.1`.
  - **Linker name**: General name, e.g., `libmylib.so`.
- Versioning ensures that older programs using an older version of the library continue to work even after upgrades.

## 9. Installing Shared Libraries
- Shared libraries are installed in standard directories like `/lib`, `/usr/lib`, or `/usr/local/lib`.
- **ldconfig** updates the runtime cache of shared library locations.

## 10. Compatible vs. Incompatible Libraries
- **Compatible library**: Older programs can still work with the updated library. This happens when internal changes or new functions are added without changing the existing functions.
- **Incompatible library**: Changes to the function signatures or removal of functions can break programs depending on older versions.

## 11. Upgrading Shared Libraries
- When upgrading a shared library, it’s important to maintain compatibility by keeping the **soname** consistent.
- If the soname changes (due to an incompatible update), programs will need to be recompiled to link to the new version.

## 12. Specifying Library Search Directories
- The `-L` option in GCC specifies custom directories for library search during compile time.
  - Example:
    ```bash
    gcc -o myprogram myprogram.c -L/usr/local/lib -lmylib
    ```
- **LD_LIBRARY_PATH** environment variable is used to specify search paths for shared libraries at runtime.

## 13. Run-Time Symbol Resolution
- When a shared library is loaded at runtime, the **dynamic linker** resolves symbols (functions, variables) as they are used.
- **Lazy binding** defers symbol resolution until the program actually calls a function, improving startup time.

## 14. Using a Static Library Instead of a Shared Library
- In some cases, you may prefer using a **static library** for portability, making the program self-contained without relying on runtime dependencies.
- This leads to larger binaries but avoids issues related to shared libraries at runtime.

## Summary
Shared libraries offer many advantages in terms of memory efficiency, flexibility, and upgradeability in Linux. Mastering the creation, versioning, and use of shared libraries—along with understanding tools like `ldd` and `ldconfig`—is essential for efficient system programming. Make sure to grasp the key concepts of PIC, soname, and run-time linking for your midterm.
