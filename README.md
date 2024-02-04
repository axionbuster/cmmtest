# CMake: Getting C++20 Modules to Work

This example demonstrates the use of C++20 modules, including module partition. The example module (namely, `foo`) has a module partition (`:bar`) in another file.

When you run this example code, you should see:
```
hello world
42
```

(Code is adapted and modified from [Kitware](https://www.kitware.com/import-cmake-the-experiment-is-over/)).

CMake has native support for C++ Modules since CMake version 3.28. It also requires pretty recent versions of the compilers and the Ninja build system (on Linux).

Since the official Ubuntu APT repository does not yet (as of writing) provide these versions, get the APT configuration scripts from the respective vendors (e.g., Kitware, Inc., which develops CMake) except for Ninja and install the newest tools with APT.

As a reminder, the latest versions are required for:

- CMake (version 3.28+)
- The C++ compiler suite (GCC 14+ or Clang 16+)
- Ninja 1.11+ (on non-Windows systems)

For Ninja, specifically, download the binary from their official GitHub release page and then put it in /usr/local/bin. This path usually has priority over the other installation directories, so there’s no need to fiddle with the "PATH" environmental variable.
