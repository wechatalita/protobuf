cmake_minimum_required (VERSION 3.6)

set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}" CACHE PATH "Installation directory" FORCE)
message(STATUS "CMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}")

project (mars-protobuf)

include(../../../mars/mars/comm/CMakeUtils.txt)

include_directories(.)
include_directories(..)

set(SELF_SRC_FILES
        google/protobuf/extension_set.cc
        google/protobuf/generated_message_util.cc
        google/protobuf/io/coded_stream.cc
        google/protobuf/io/zero_copy_stream.cc
        google/protobuf/io/zero_copy_stream_impl_lite.cc
        google/protobuf/message_lite.cc
        google/protobuf/repeated_field.cc
        google/protobuf/stubs/atomicops_internals_x86_msvc.cc
        google/protobuf/stubs/atomicops_internals_x86_gcc.cc
        google/protobuf/stubs/common.cc
        google/protobuf/stubs/once.cc
        google/protobuf/stubs/stringprintf.cc
        google/protobuf/wire_format_lite.cc)
    

if(MSVC)
    include_directories(../../../mars/mars/comm/windows)
endif()

list(FILTER SELF_SRC_FILES EXCLUDE REGEX ".*unittest.cc$")
add_library(${PROJECT_NAME} STATIC ${SELF_SRC_FILES})
install(TARGETS ${PROJECT_NAME} ARCHIVE DESTINATION ${CMAKE_SYSTEM_NAME}.out)
    
