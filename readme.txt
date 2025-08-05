file structure : 
MyProject/
│── CMakeLists.txt
│── src/
│   ├── main.cpp
│   ├── math.cpp
│── include/
│   ├── math.h

---------------------------------------
cmake_minimum_required(VERSION 3.10)
project(MyProject)

set(CMAKE_CXX_STANDARD 11)

include_directories(include)

add_library(math_lib src/math.cpp)
add_executable(main src/main.cpp)
target_link_libraries(main math_lib)

add_library 命令是CMake 中创建库的关键命令。 它允许你指定库的名称、类型和源文件。 

然后，使用 target_link_libraries 命令将库链接到其他目标，以便在构建过程中使用。
