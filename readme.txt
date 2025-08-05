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

---------
a. 
创建一个名为 my_library 的静态库
add_library(my_library STATIC source1.cpp source2.cpp)

b. 
创建一个名为 my_shared_library 的动态库：
add_library(my_shared_library SHARED source3.cpp source4.cpp)

-----cmake导入外部链接库---------
how to include so library ???? 

$ add_library(MyExternalLibrary SHARED IMPORTED)
$     set_target_properties(MyExternalLibrary PROPERTIES
$         IMPORTED_LOCATION "/path/to/your/libMyExternalLibrary.so"
$        INTERFACE_INCLUDE_DIRECTORIES "/path/to/your/headers"
$    )

MyExternalLibrary: This is the internal name you'll use for the library within your CMake project.
SHARED: Specifies that it's a shared library.
IMPORTED: Indicates that the library is pre-existing and not built by this project.
IMPORTED_LOCATION: Sets the absolute path to the .so file.
INTERFACE_INCLUDE_DIRECTORIES: Specifies the directory containing the public header files needed to use the library.

-------------------------------------------
how to Link the Library to your Executable or another Library ???

$ add_executable(MyExecutable main.cpp)
$ target_link_libraries(MyExecutable PRIVATE MyExternalLibrary)

MyExecutable: The name of your executable target.
PRIVATE: Indicates that MyExternalLibrary is a private dependency of MyExecutable, meaning it's only needed for linking MyExecutable and not exposed to targets linking to MyExecutable. Use PUBLIC or INTERFACE if the dependency needs to be propagated.

-------------------
how to include System Libraries ??

Alternatively, for System Libraries:
If the library is a standard system library (e.g., pthread, m), 
you can directly link it without declaring an imported target:

$ target_link_libraries(MyExecutable PRIVATE pthread)

-----------
https://medium.com/@abhishekjainindore24/static-library-vs-dynamic-library-understanding-the-differences-26e47cac93b6

Static Library vs Dynamic Library: Understanding the Differences

static libraries have extensions like .lib (Windows) or .a (Unix/Linux).

Typically, dynamic libraries have extensions like .dll (Windows) or .so (Unix/Linux).

C++ programs are built in two phases

Compilation - produces object code (.obj)
Linking - produces executable code (.exe or .dll)
Static library (.lib) is just a bundle of .obj files and therefore isn't a complete program. 
It hasn't undergone the second (linking) phase of building a program. Dlls, on the other hand, 
are like exe's and therefore are complete programs.














