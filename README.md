# Cpp2-Example

Cmake project to play with Herb Sutter cppfront (cpp2 -> cpp1). It is using cppfront code https://github.com/hsutter/cppfront to process `*.cpp2` files and compile them with your C++20 capable compiler.

## Use

1. Edit `main.cpp2`file.
2. Create a build directory and run `cmake ..` (assuming build is in the project directory),
3. Build it with `cmake --build .``
4. Run it with `./main`

## Note

Cppfront is used with `-p` options which means that you can only compile pure cpp2 code. If you want to use it with mixed mode change `cppfront -p` to `cppfront` in the `CMakeLists.txt` file.