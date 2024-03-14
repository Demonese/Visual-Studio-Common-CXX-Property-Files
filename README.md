# Visual Studio Common CXX Property Files

Better project structure.

## Usage

Clone this repository into a Visual Studio solution, for example:

```batch
git clone https://github.com/Demonese/Visual-Studio-Common-CXX-Property-Files.git property
```

```
example-solution-folder
    property
    other folders...
    example-solution.sln
    other files...
```

Add property files as needed to the project.

## Property files

This repository provides the following commonly used property files:

* utf-8.props
* cpp-20.props
* universal-build-output.props
* hybrid-c-runtime.props

### utf-8.props

Ensure all source files are parsed in UTF-8 encoding and string literals are compiled into binaries in UTF-8.

Reference: [`/utf-8` (Set source and execution character sets to UTF-8)](https://learn.microsoft.com/en-us/cpp/build/reference/utf-8-set-source-and-executable-character-sets-to-utf-8?view=msvc-170)
