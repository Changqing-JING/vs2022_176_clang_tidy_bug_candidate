This repo describes a bug candidate that enable clang-tidy leads to Build failed.

clang-tidy check is added by cmake:
```cmake
set_target_properties(${PROJECT_NAME} PROPERTIES
        VS_GLOBAL_RunCodeAnalysis true
        VS_GLOBAL_EnableMicrosoftCodeAnalysis false
        VS_GLOBAL_EnableClangTidyCodeAnalysis true
)
```

reproduce steps
Use MSBuild version 17.6.3
```shell
mkdir build
cd build
cmake -A x64 ..
cmake --build .
```
Observed behavior:
Build failed with error
```
cmake --build .
MSBuild version 17.6.3+07e294721 for .NET Framework

  Checking Build System
  Building Custom Rule D:/code/workspace/github/vs2022_176_clang_tidy_bug_candidate/C1/CMakeLists.txt
  C1.cpp
D:\code\workspace\github\vs2022_176_clang_tidy_bug_candidate\C1\C1.cpp(5,5): warning G49EBC149: do not call c-style vararg functions [cppcoreguidelines-pro-type-vararg] [D:\code\workspace\github\vs
2022_176_clang_tidy_bug_candidate\build\C1\C1.vcxproj]
      printf("foo\n");
      ^
C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(1621,5): error MSB3025: The source file "D:\code\workspace\github\vs2022_176_clang_tidy
_bug_candidate\build\C1\" is actually a directory.  The "Copy" task does not support copying directories. [D:\code\workspace\github\vs2022_176_clang_tidy_bug_candidate\build\C1\C1.vcxproj]
```


Expected behavior:
Build success with clang-tidy waring
