# Copyright 2021, Collabora, Ltd.
#
# SPDX-License-Identifier: MIT

add_executable(main_test main.cpp testing.h)
target_link_libraries(main_test PRIVATE jnipp)
add_test(NAME main_test COMMAND main_test)

if(NOT JNIPP_USE_EXCEPTION_HANDLING)
  if (CMAKE_CXX_COMPILER_ID STREQUAL "Clang" OR CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    target_compile_options(main_test PRIVATE -fno-exceptions)
  endif()
endif()

add_executable(external_create external_create.cpp testing.h)
target_link_libraries(external_create PUBLIC jnipp ${JNI_LIBRARIES})
target_include_directories(external_create PUBLIC ${JNI_INCLUDE_DIRS})
add_test(NAME external_create COMMAND external_create)


add_executable(external_detach external_detach.cpp testing.h)
target_link_libraries(external_detach PUBLIC jnipp ${JNI_LIBRARIES})
target_include_directories(external_detach PUBLIC ${JNI_INCLUDE_DIRS})
add_test(NAME external_detach COMMAND external_detach)
