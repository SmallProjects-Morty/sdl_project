# CMake Tutorial

## Prerequisits (installations)

- Install C++ plugin.
- Install cmake (brew install cmake).
- Install CMake Tools plugin.

## CMakeLists.txt (generates files that can build the executable)

- cmake_minimum_required(VERSION 3.23.1)
- project(sdl_project)
- add_executable(${PROJECT_NAME} main.cpp)

### CMake build process (builds executable)

1. mkdir build
2. cmake ./build
3. make -C ./build

## Debugging

- Add `set(CMAKE_BUILD_TYPE Debug)` to the CMakeLists.txt
- Install `CMake Tools` plugin (if not already installed)
- Click on the new "CMake" plugin icon on the left
- Select "Configure All Projects"
- If no build option is already availble, select "Build" and whichever project you want (default is "all")
- Right click on the wanted project from the "CMake" plugin panel (sdl_project in my case) and select "debug".

## VS Code

### launch.json

`{ "version": "0.2.0", "configurations": [ { "name": "GDB Debug", "type": "cppdbg", "request": "launch", // Resolved by CMake Tools: "program": "${command:cmake.launchTargetPath}", "args": [], "stopAtEntry": false, "cwd": "${workspaceFolder}/build", "environment": [ { // add the directory where our target was built to the PATHs // it gets resolved by CMake Tools: "name": "PATH", "value": "$PATH:${command:cmake.launchTargetDirectory}" }, { "name": "OTHER_VALUE", "value": "Something something" } ], "externalConsole": true, "MIMode": "gdb", "setupCommands": [ { "description": "Enable pretty-printing for gdb", "text": "-enable-pretty-printing", "ignoreFailures": true } ] } ] }`

### tasks.json

`{ "version": "2.0.0", "tasks": [ { "type": "shell", "label": "C/C++: clang build active file", "command": "/usr/bin/clang++", "args": [ "-std=c++17", "-stdlib=libc++", "-fdiagnostics-color=always", "-g", "${file}", "-o", "${fileDirname}/${fileBasenameNoExtension}" ], "options": { "cwd": "${fileDirname}" }, "problemMatcher": [ "$gcc" ], "group": "build", "detail": "compiler: /usr/bin/clang++" }, { "type": "cppbuild", "label": "C/C++: g++ build active file", "command": "/usr/bin/g++", "args": [ "-fdiagnostics-color=always", "-g", "${file}", "-o", "${fileDirname}/${fileBasenameNoExtension}" ], "options": { "cwd": "${fileDirname}" }, "problemMatcher": [ "$gcc" ], "group": { "kind": "build", "isDefault": true }, "detail": "Task generated by Debugger." } ] }`
