# TODO 1: Set the minimum required version of CMake to be 3.10

# TODO 2: Create a project named Tutorial

# TODO 7: Set the project version number as 1.0 in the above project command

# TODO 6: Set the variable CMAKE_CXX_STANDARD to 11
#         and the variable CMAKE_CXX_STANDARD_REQUIRED to True

# TODO 8: Use configure_file to configure and copy TutorialConfig.h.in to
#         TutorialConfig.h

# TODO 3: Add an executable called Tutorial to the project
# Hint: Be sure to specify the source file as tutorial.cxx

# TODO 9: Use target_include_directories to include ${PROJECT_BINARY_DIR}
#cmake_minimum_required(VERSION 3.10)
cmake_minimum_required(VERSION 3.15)
project(Tutorial VERSION 2.2)
add_library(tutorial_compiler_flags INTERFACE)
target_compile_features(tutorial_compiler_flags INTERFACE cxx_std_11)
set(gcc_like_cxx "$<COMPILE_LANG_AND_ID:CXX,ARMClang,AppleClang,Clang,GNU,LCC>")
set(msvc_cxx "$<COMPILE_LANG_AND_ID:CXX,MSVC>")
target_compile_options(tutorial_compiler_flags INTERFACE "$<${gcc_like_cxx}:$<BUILD_INTERFACE:-Wall;-Wextra;-Wshadow;-Wformat=2;-Wunused>>" "$<${msvc_cxx}:$<BUILD_INTERFACE:-W3>>")
#target_compile_options(tutorial_compiler_flags INTERFACE
#"$<${gcc_like_cxx}:$<BUILD_INTERFACE:-Wall;-Wextra;-Wshadow;-Wformat=2;-Wunused>>"
 # "$<${msvc_cxx}:$<BUILD_INTERFACE:-W3>>"
#)
configure_file(TutorialConfig.h.in TutorialConfig.h)
add_subdirectory(MathFunctions)
add_executable(Tutorial tutorial.cxx)
target_link_libraries(Tutorial MathFunctions tutorial_compiler_flags)
#TODO X: Remove use of EXTRA_INCLUDES
target_include_directories(Tutorial PUBLIC "${PROJECT_BINARY_DIR}")


#TODO 3: Install Tutorial in the bin directory
# Hint: Use the TARGETS and DESTINATION parameters

# TODO 4: Install TutorialConfig.h to the include directory
# Hint: Use the FILES and DESTINATION parameters

install(TARGETS Tutorial DESTINATION "${PROJECT_BINARY_DIR}/bin")
install(FILES "${PROJECT_BINARY_DIR}/TutorialConfig.h" DESTINATION "${PROJECT_BINARY_DIR}/include")
