# Visual Studio Common CXX Property Files

Better project structure.

## Usage

1. Clone this repository into a Visual Studio solution, for example:

    ```batch
    git clone https://github.com/Demonese/Visual-Studio-Common-CXX-Property-Files.git property
    ```

    * example-solution-directory
        * property
        * other directories...
        * example-solution.sln
        * other files...

2. Add property files as needed to the project.

## Property files

This repository provides the following commonly used property files:

* utf-8.props
* cpp-20.props
* universal-build-output.props
* hybrid-c-runtime.props

### utf-8.props

Ensure all source files are parsed in UTF-8 encoding and string literals are compiled into binaries in UTF-8.

Reference: [`/utf-8` (Set source and execution character sets to UTF-8)](https://learn.microsoft.com/en-us/cpp/build/reference/utf-8-set-source-and-executable-character-sets-to-utf-8?view=msvc-170)

### universal-build-output.props

By default, projects created by Visual Studio, build intermediate directories under the project directory, and build output directories are under the solution directory. This default value is not optimal.

The following directory structure is more reasonable:


* example-solution-directory
    * build
        * Debug
            * objects
                * intermediate files...
            * foo.exe
            * foo.pdb
            * bar.dll
            * bar.lib
            * bar.pdb
            * other files...
        * Release
            * objects
                * intermediate files...
            * foo.exe
            * bar.dll
            * bar.lib
            * other files...
        * other configurations...
    * other directories...
    * example-solution.sln
    * other files...

All build output files are located in build directory.
