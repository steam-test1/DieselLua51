cmake_minimum_required (VERSION 3.19)

set(CMAKE_GENERATOR_PLATFORM Win32)

project(lua51)

# include_directories ( src ${CMAKE_CURRENT_BINARY_DIR} )
# set ( SRC_CORE src/lapi.c src/lcode.c src/ldebug.c src/ldo.c src/ldump.c src/lfunc.c src/lgc.c src/llex.c
#   src/lmem.c src/lobject.c src/lopcodes.c src/lparser.c src/lstate.c src/lstring.c src/ltable.c
#   src/ltm.c src/lundump.c src/lvm.c src/lzio.c )
# set ( SRC_LIB src/lauxlib.c src/lbaselib.c src/ldblib.c src/liolib.c
#   src/lmathlib.c src/loslib.c src/lstrlib.c src/ltablib.c src/loadlib.c src/linit.c )

# set ( SRC_LUA src/lua.c )
# set ( SRC_LUAC src/luac.c src/print.c )

# add_library(lua_static STATIC ${SRC_LIB})
# set_target_properties(lua_static PROPERTIES OUTPUT_NAME lua51 COMPILE_OPTIONS "-m32" LINK_FLAGS "-m32")

# include_directories(${PROJECT_SOURCE_DIR}/src)
# file(GLOB SRCS "${PROJECT_SOURCE_DIR}/src/*.cpp" "${PROJECT_SOURCE_DIR}/src/*.c")
# add_library(${PROJECT_NAME} STATIC ${SRCS})

# Sources and headers
include_directories ( src ${CMAKE_CURRENT_BINARY_DIR} )
set ( SRC_LIB src/lapi.c src/lcode.c src/ldebug.c src/ldo.c src/ldump.c src/lfunc.c
  src/lgc.c src/llex.c src/lmem.c src/lobject.c src/lopcodes.c src/lparser.c src/lstate.c
  src/lstring.c src/ltable.c src/ltm.c src/lundump.c src/lvm.c src/lzio.c src/lauxlib.c
  src/lbaselib.c src/ldblib.c src/liolib.c src/lmathlib.c src/loslib.c src/ltablib.c
  src/lstrlib.c src/linit.c )
set ( SRC_LUA src/lua.c )
set ( SRC_LUAC src/luac.c src/print.c )

# Create static library, this is needed to compile luac in the 5.1.x Lua series
add_library ( liblua_static STATIC ${SRC_LIB} )
target_link_libraries ( liblua_static ${LIBS} )

add_executable ( lua ${SRC_LUA} ${LUA_RC} )
target_link_libraries ( lua liblua )