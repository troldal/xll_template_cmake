#==============================================================================
# Preamble
#==============================================================================
cmake_minimum_required(VERSION 3.20)
project(Xll.Library)

#==============================================================================
# Set compiler settings
#==============================================================================
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#==============================================================================
# Add the bundled XLCALL32.lib library for both 32 and 64 bit configurations
#==============================================================================
add_library(xlcall STATIC IMPORTED GLOBAL)
if( CMAKE_SIZEOF_VOID_P EQUAL 8 )
    set_target_properties(xlcall PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/xll/x64/XLCALL32.LIB)
else()
    set_target_properties(xlcall PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/xll/XLCALL32.LIB)
endif()

#==============================================================================
# Add Xll library and set source file paths
#==============================================================================
add_library(
        xll
        STATIC
        ${CMAKE_CURRENT_LIST_DIR}/xll/auto.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/debug.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/defines.c
        ${CMAKE_CURRENT_LIST_DIR}/xll/dllmain.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/error.cpp

        ${CMAKE_CURRENT_LIST_DIR}/xll/macrofun/xll_document.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/macrofun/xll_function.cpp

        ${CMAKE_CURRENT_LIST_DIR}/xll/macrofun/xll_macrofun.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/macrofun/xll_paste.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/macrofun/xll_spreadsheet.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/macrofun/xll_utility.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/utility/xll_throttle.cpp
        ${CMAKE_CURRENT_LIST_DIR}/xll/XLCALL.CPP
)

#==============================================================================
# Set Xll library properties and compile options
#==============================================================================
target_compile_definitions(xll PRIVATE -DUNICODE -D_UNICODE)
target_compile_options(xll PRIVATE "/J" "/utf-8")
target_include_directories(xll PUBLIC ${CMAKE_CURRENT_LIST_DIR}/xll)