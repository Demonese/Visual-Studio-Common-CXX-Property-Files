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
* universal-build-output.props
* hybrid-c-runtime.props
* cpp-20.props
* more-cpp-diagnostics.props

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

### hybrid-c-runtime.props

Developer tests application and it runs fine locally. Developer build, package and distribute application to users, users feedback that the application cannot run: VC++ runtime library is missing.

Developer thinking: Okay, let's statically link to the C runtime.

But wait a minute, Windows 10 has bundled universal C runtime, can we take advantage of it and reduce the application size?

The answer is yes, we have a trick called "hybrid C runtime".

> Note: Please only add hybrid-c-runtime.props file to the Release configuration, it does not support Debug like configuration.

Reference: [Hybrid CRT](https://github.com/microsoft/WindowsAppSDK/blob/main/docs/Coding-Guidelines/HybridCRT.md)

### cpp-20.props

Using C++ 20.

### more-cpp-diagnostics.props

This property file enable these features:

* SDL check
* warning level 4
* caret fiagnostics format

It is strongly recommended to delete the following contents of the .vcxproj file:

```diff
 <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'">
   <ClCompile>
-    <WarningLevel>Level3</WarningLevel>
-    <SDLCheck>true</SDLCheck>
-    <ConformanceMode>true</ConformanceMode>
     <PreprocessorDefinitions>WIN32;_DEBUG;_CONSOLE;%(PreprocessorDefinitions)</PreprocessorDefinitions>
   </ClCompile>
   ...
 </ItemDefinitionGroup>
 <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'">
   <ClCompile>
-    <WarningLevel>Level3</WarningLevel>
-    <SDLCheck>true</SDLCheck>
-    <ConformanceMode>true</ConformanceMode>
     <FunctionLevelLinking>true</FunctionLevelLinking>
     <IntrinsicFunctions>true</IntrinsicFunctions>
     <PreprocessorDefinitions>WIN32;NDEBUG;_CONSOLE;%(PreprocessorDefinitions)</PreprocessorDefinitions>
   </ClCompile>
   ...
 </ItemDefinitionGroup>
 <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">
   <ClCompile>
-    <WarningLevel>Level3</WarningLevel>
-    <SDLCheck>true</SDLCheck>
-    <ConformanceMode>true</ConformanceMode>
     <PreprocessorDefinitions>_DEBUG;_CONSOLE;%(PreprocessorDefinitions)</PreprocessorDefinitions>
   </ClCompile>
   ...
 </ItemDefinitionGroup>
 <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'">
   <ClCompile>
-    <WarningLevel>Level3</WarningLevel>
-    <SDLCheck>true</SDLCheck>
-    <ConformanceMode>true</ConformanceMode>
     <FunctionLevelLinking>true</FunctionLevelLinking>
     <IntrinsicFunctions>true</IntrinsicFunctions>
     <PreprocessorDefinitions>NDEBUG;_CONSOLE;%(PreprocessorDefinitions)</PreprocessorDefinitions>
   </ClCompile>
   ...
 </ItemDefinitionGroup>
```
