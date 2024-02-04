# CMake: Getting C++20 Modules to Work

This example demonstrates the use of C++20 modules, including module partition. The example module (namely, `foo`) has a module partition (`:bar`) in another file.

When you run this example code, you should see:
```
hello world
42
```

(Code is adapted and modified from [Kitware](https://www.kitware.com/import-cmake-the-experiment-is-over/)).

## Latest Versions Needed

CMake has native support for C++ Modules since CMake version 3.28. It also requires pretty recent versions of the compilers and the Ninja build system (on Linux).

Since the official Ubuntu APT repository does not yet (as of writing) provide these versions, get the APT configuration scripts from the respective vendors (e.g., Kitware, Inc., which develops CMake) except for Ninja and install the newest tools with APT.

As a reminder, the latest versions are required for:

- CMake (version 3.28+)
- The C++ compiler suite (GCC 14+ or Clang 16+)
- Ninja 1.11+ (on non-Windows systems)

For Ninja, specifically, download the binary from their official GitHub release page and then put it in /usr/local/bin. This path usually has priority over the other installation directories, so there’s no need to fiddle with the "PATH" environmental variable.

## Windows and Visual Studio

My Visual Studio (Community 2022; 17.8.6) uses its own CMake, which is, as of writing, one minor version too late.

To remedy this, I download the latest CMake binary from [Kitware downloads](https://cmake.org/download/),
and change the Visual Studio-specific file named `CMakeSettings.json`
to make it use the locally installed version of CMake,
following [a StackOverflow answer](https://stackoverflow.com/questions/58773901/configure-cmake-version-in-visual-studio-2019):

(File: `/CMakeSettings.json`):
```json
{
  "configurations": [
    {
      "name": "x64-Debug",
      "generator": "Ninja",
      "configurationType": "Debug",
      "inheritEnvironments": [ "msvc_x64_x64" ],
      "buildRoot": "${projectDir}\\out\\build\\${name}",
      "installRoot": "${projectDir}\\out\\install\\${name}",
      "cmakeExecutable": "C:\\Program Files\\CMake\\bin\\cmake.exe",
      "cmakeCommandArgs": "",
      "buildCommandArgs": "",
      "ctestCommandArgs": ""
    }
  ]
}
```

(If such a file doesn't exist, it can be generated by clicking
"Manage Configurations" in one of the drop-down buttons in the top bar.
See: [Microsoft](https://learn.microsoft.com/en-us/cpp/build/customize-cmake-settings?view=msvc-170)).

I haven't been able to find a corresponding setting (to set CMake executable) in `CMakePresets.json`,
which appears to be the planned successor of `CMakeSettings.json`.

## Error: "The target named ... may use modules ... but the compiler ... dependencies."

Configure the project with the latest compiler.

I have clang 18 installed, so I used (under key `configurations`):
```json
{
    "name": "WSL-Clang-Debug",
    ...
    "cmakeCommandArgs": "-DCMAKE_C_COMPILER:FILEPATH=/usr/bin/clang-18 -DCMAKE_CXX_COMPILER:FILEPATH=/usr/bin/clang++-18",
    ...
}
```
(the rest having been generated by Visual Studio).