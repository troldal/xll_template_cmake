#==============================================================================
# Preamble
#==============================================================================
cmake_minimum_required(VERSION 3.20)
project(Xll.Template)

#==============================================================================
# Set compiler settings
#==============================================================================
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#==============================================================================
# Add the Xll base library
#==============================================================================
add_subdirectory(xll)

#==============================================================================
# Add xll template library and set source file paths
#==============================================================================
add_library(
        xlltemplate
        SHARED
        ${CMAKE_CURRENT_SOURCE_DIR}/xll_template.cpp
)

#==============================================================================
# Set Xll library properties and compile options
#==============================================================================
target_compile_options(xlltemplate PRIVATE "/J" "/utf-8")
target_link_libraries(xlltemplate PRIVATE xlcall xll)
set_target_properties(xlltemplate PROPERTIES OUTPUT_NAME "xll_template" SUFFIX ".xll")
