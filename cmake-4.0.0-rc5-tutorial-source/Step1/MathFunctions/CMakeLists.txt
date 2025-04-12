# TODO 14: Remove mysqrt.cxx from the list of sources

# TODO 1: Add a library called MathFunctions with sources MathFunctions.cxx
# and mysqrt.cxx
# Hint: You will need the add_library command
add_library(MathFunctions MathFunctions.cxx)
# TODO 7: Create a variable USE_MYMATH using option and set default to ON
#state that anybody linking to us needs to include the current source dir
# to find MathFunctions.h, while we don't.
target_include_directories(MathFunctions
        INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
)
option(USE_MYMATH "Use my math functions" ON)
# TODO 8: If USE_MYMATH is ON, use target_compile_definitions to pass
# USE_MYMATH as a precompiled definition to our source files
if(USE_MYMATH)
    target_compile_definitions(MathFunctions
        PUBLIC USE_MYMATH)
    add_library(SqrtLibrary mysqrt.cxx)
    target_link_libraries(MathFunctions PRIVATE SqrtLibrary)
    target_link_libraries(SqrtLibrary PUBLIC tutorial_compiler_flags)
endif()
# TODO 12: When USE_MYMATH is ON, add a library for SqrtLibrary with
# source mysqrt.cxx

# TODO 13: When USE_MYMATH is ON, link SqrtLibrary to the MathFunctions Library
# TODO 1: Create a variable called installable_libs that is a list of all
# libraries we want to install (e.g. MathFunctions and tutorial_compiler_flags)
# Then install the installable libraries to the lib folder.
# Hint: Use the TARGETS and DESTINATION parameters
set(install_libs MathFunctions tutorial_compiler_flags)
if(TARGET SqrtLibrary)
    list(APPEND install_libs SqrtLibrary)
endif()
install(TARGETS ${install_libs} DESTINATION "${PROJECT_BINARY_DIR}/lib")

# TODO 2: Install the library headers to the include folder.
# Hint: Use the FILES and DESTINATION parameters
install(FILES MathFunctions.h DESTINATION "${PROJECT_BINARY_DIR}/include")