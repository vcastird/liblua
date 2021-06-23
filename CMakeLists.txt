cmake_minimum_required(VERSION 3.1)
project(LuaLibrary LANGUAGES C VERSION 5.4.2)

include(GNUInstallDirs)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/install)
endif()

add_library(liblua STATIC
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lapi.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lauxlib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lbaselib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lcode.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lcorolib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lctype.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/ldblib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/ldebug.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/ldo.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/ldump.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lfunc.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lgc.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/linit.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/liolib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/llex.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lmathlib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lmem.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/loadlib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lobject.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lopcodes.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/loslib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lparser.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lstate.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lstring.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lstrlib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/ltable.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/ltablib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/ltm.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lundump.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lutf8lib.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lvm.c
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lzio.c
)

set(public_headers
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lauxlib.h
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lua.h
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/lualib.h
  ${CMAKE_CURRENT_LIST_DIR}/lua/src/luaconf.h
)

set_target_properties(liblua
  PROPERTIES
    OUTPUT_NAME lua
    PUBLIC_HEADER "${public_headers}"
)

set(public_header_dir "include/lua")

target_include_directories(liblua
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/lua/src>
    $<INSTALL_INTERFACE:${public_header_dir}>
)

if(UNIX)
  target_link_libraries(liblua PRIVATE m)
endif()

if(MSVC)
  # Suppress warnings due to not using the _s function variants on MSVC.
  target_compile_definitions(liblua PUBLIC _CRT_SECURE_NO_WARNINGS)
endif()

install(TARGETS liblua
  EXPORT LibLuaTargets
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
  PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/lua
)
