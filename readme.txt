
CMake is a cross-platform build system generator. Projects specify their build process with platform-independent CMake listfiles included in each directory of a source tree with the name CMakeLists.txt. Users build a project by using CMake to generate a build system for a native tool on their platform.
provide version information
update project name
update executable and binary and source files 

add version to project
configure input interface file to generate uoutput header file==configure_file
target_include_directories() to specify where the executable target should look for include files.

we can add libraries inside subdirectories (individual cmake) and link them to top directory build 
conditional statements in order to provide option

usage requirements: specify the depending library include directories in cmake of mathfunctions itself.(instead of in top level)
the only thing our executable target does to use our library is call target_link_libraries() with the name of the library target. In larger projects, the classic method of specifying library dependencies manually becomes very complicated very quickly.

Generator expressions may be used to enable conditional linking, conditional definitions used when compiling, conditional include directories and more. The conditions may be based on the build configuration, target properties, platform information or any other queryable information.


A runtime output artifact of a buildsystem target may be:

The executable file (e.g. .exe) of an executable target created by the add_executable() command.

On DLL platforms: the executable file (e.g. .dll) of a shared library target created by the add_library() command with the SHARED option.

A library output artifact of a buildsystem target may be:

The loadable module file (e.g. .dll or .so) of a module library target created by the add_library() command with the MODULE option.

 cmake -G "MinGW Makefiles" ..\cmake-4.0.0-rc5-tutorial-source\Step1
 cmake --build . --target install --config Debug
 cmake --install .

 ctest
 enable_testing()
 add_test(), set_tests_properties()

 commands: ctest -N  -lists the test information without testing
 ctest -V : verbose: detailed information and testing 
 ctest -VV: very detailed verbose


 As a dashboard client, CTest performs a sequence of steps to configure, build, and test software, and then submits the results to a CDash server. 