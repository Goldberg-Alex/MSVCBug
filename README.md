# MSVCBug

This small repository demonstrates a compiler bug in Microsoft Visual C++ (MSVC) related to list-initialization of dynamic arrays.
note that the Project is compiled with /clr.

## Files

- `CompilerBug.cpp` — minimal reproducer

## Expected behavior

Per the C++ standard (C++11 and later) a new-expression can use list-initialization to initialize elements of a dynamically allocated array. The code above should compile and value-/list-initialize the first array element with `a == 0.0`.

## Observed MSVC behavior

MSVC reports a compilation error when encountering the brace initializer on the `new S[rows]{ ... }` expression. This is a compiler bug in MSVC's handling of list-initialization for dynamically-sized arrays.

## How to reproduce

Prerequisites: a C++ compiler (MSVC, GCC, or Clang). Use a Developer Command Prompt for MSVC.

- MSVC (reproduce the failure):

  1. Open "Developer Command Prompt for VS".
  2. Run:

     `cl /EHa /clr CompilerBug.cpp`

  Note: behavior depends on MSVC version; newer MSVC releases may have fixed the issue.
