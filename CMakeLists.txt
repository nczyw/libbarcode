cmake_minimum_required(VERSION 3.25)
set(PRONAME "barcode")
project(${PRONAME} VERSION 1.0.0 LANGUAGES C)

# Set C language
set(CMAKE_C_STANDARD 17)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Find all .c files 
file(GLOB_RECURSE SOURCES "src/*.c")
#file(GLOB_RECURSE LIB_SOURCES "lib/src/*.c")
#list(APPEND SOURCES ${LIB_SOURCES})

# Find all .h files
file(GLOB_RECURSE HEADERS "inc/*.h")
#file(GLOB_RECURSE LIB_HEADERS "lib/inc/*.h")
#list(APPEND HEADERS ${LIB_HEADERS})



if (MSVC)
  set(CMAKE_DEBUG_POSTFIX "_d")
endif(MSVC)

# create library
add_library(${PRONAME} STATIC   ${SOURCES} 
                                ${HEADERS}
)

# Set include directories
target_include_directories(${PRONAME} PUBLIC 
                            inc
)
# install 
set_target_properties(${PRONAME} PROPERTIES PUBLIC_HEADER "${CMAKE_CURRENT_SOURCE_DIR}/inc/barcode.h" OUTPUT_NAME ${PRONAME})
install(TARGETS ${PRONAME} LIBRARY ARCHIVE RUNTIME PUBLIC_HEADER)
