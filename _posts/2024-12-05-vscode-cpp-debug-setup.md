---
layout: post
title: 'Setup vscode cpp debugger for mac' 
tags: note
---

*This is a rather simple boiled down version, just in case I need to set it up again.*

**Prerequiste: c++ is already installed on mac.**

There are 3 files are required under `.vscode` folder: 
```
c_cpp_properties
tasks.json
launch.json 
```

Here is how to generate them: 

## Simplest: run a single cpp file. 
- Generate `c_cpp_properties.json` file. 
  IntelliSense is required for this step to generate the file. 
  To generate the file:
    1. Install C/C++ extension, this will include IntelliSense as part of it.
    2. Make sure C/C++ has allowed IntelliSense: in `setting.json` file (command+,) checked `C_Cpp.intelliSenseEngine` is set to **default**. 
    3. Generate the property file by command `C/C++: C/C++: Edit Configurations (UI)`. Edit configuration as needed. This configuration will generate the c_cpp_properties.json file. 


  Example: 
  ```
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "macFrameworkPath": [
                "/Library/Developer/CommandLineTools/SDKs/MacOSX14.sdk/System/Library/Frameworks"
            ],
            "compilerPath": "/opt/homebrew/bin/g++-14",
            "cStandard": "c17",
            "cppStandard": "c++17",
            "intelliSenseMode": "macos-clang-arm64"
        }
    ],
    "version": 4
}
  ```

- Generate `tasks.json`. 
    After c_cpp_properties.json file is generated, should be able to see the cpp files have the option to run/debug (icons on the top right). Now click the run/debug icon, vscode will ask if generate tasks. A task is baiscally a command to build the file, so edit the task as much as needed. 
  
  Example: 
  ```
{
  "tasks": [
    {
      "type": "cppbuild",
      "label": "g++ build cpp",
      "command": "/opt/homebrew/bin/g++-14",
      "args": [
        "-fdiagnostics-color=always",
        "-g",
        "${file}",
        "-o",
        "${fileDirname}/${fileBasenameNoExtension}"
      ],
      "options": {
        "cwd": "${fileDirname}"
      },
      "problemMatcher": [
        "$gcc"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "detail": "Task generated by Debugger."
    }
  ],
  "version": "2.0.0"
}
  ```

- Generate `launch.json`
    This file can be generated directly use "Add configuration" under `Run` to generate the file. The catch here is lldb might not work correctly, instead, use codelldb extension and change the "type" to "lldb".
    
    gdb doesn't work on mac directly (need extra setup, not doing it here). lldb has attach and launch mode, attach mode is to start from an running instance, launch is just launch a new one. 
  
  Example:
  ```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "debug-cpp",
      "type": "lldb",
      "request": "launch",
      "program": "${workspaceFolder}/hello.cpp",
      "args": [],
      "cwd": "${workspaceFolder}",
      "preLaunchTask": "g++ build cpp"
    }
  ]
}
  ```

## Sightly bigger project with cmake and stuff: 
Basically just change the command in tasks.json to shell for building the project, then change the program to run in launch.json to directly run the test. In this case might need a different debug program for each group of tests.  

Misc: 
- To make debug console autuomactially show after build, in `setting.json`, set `"internalConsoleOptions": "openOnSessionStart"`. 
- Pass "-g" to g++ is not really skippabled, "-g" means turn on debugging, which is required for further debugger behavior. 

### Reference 
- <https://stackoverflow.com/questions/49583381/how-to-debug-a-cmake-make-project-in-vscode> 
- <https://stackoverflow.com/questions/67270447/visual-studio-code-lldb-on-macos-error-when-starting-debugging-session>



