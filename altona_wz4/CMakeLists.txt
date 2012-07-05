cmake_minimum_required(VERSION 2.8)

project(werkzeug)
set(CMAKE_CXX_FLAGS "-fpermissive -w -Wno-unused-function -Wno-invalid-offsetof -fno-exceptions -fno-common -fno-strict-aliasing -fno-rtti -fshort-wchar -finput-charset=ISO8859-1")

#ADD_DEFINITIONS("-DsCONFIG_GUID={0xB405548B,{0xF306,0x45C9,0x856B},{0x76,0x7B,0xB3,0xF6,0xB6,0xE0}}")
#ADD_DEFINITIONS("-DsCONFIG_GUID=\{0xB405548B,\{0xF306,0x45C9,0x856B\},\{0x76,0x7B,0xB3,0xF6,0xB6,0xE0\}\}")
#ADD_DEFINITIONS(-DsCONFIG_GUID=0)
ADD_DEFINITIONS(-DsCONFIG_BUILD_DEBUG)
ADD_DEFINITIONS(-DsCONFIG_RENDER_BLANK)
ADD_DEFINITIONS(-DsCONFIG_OPTION_SHELL=1)
ADD_DEFINITIONS(-DsCONFIG_SYSTEM_LINUX)

message("foo ${COMPILE_DEFINITIONS}")

include_directories(
  altona/main/
  altona/
)

set(ALTONA_BASE
altona/main/base/graphics.cpp
altona/main/base/graphics_blank.cpp
altona/main/base/math.cpp
altona/main/base/sound.cpp
altona/main/base/system.cpp
altona/main/base/system_linux.cpp
altona/main/base/input2.cpp
altona/main/base/devices_win.cpp
altona/main/base/types.cpp
altona/main/base/types2.cpp
altona/main/base/serialize.cpp
altona/main/base/windows.cpp
altona/main/base/windows_xlib.cpp

#altona/main/base/graphics_dx11.cpp    
#altona/main/base/graphics_dx9.cpp     

#altona/main/base/graphics_ogl2.cpp    
#altona/main/base/glprocs.c

#altona/main/base/graphics_ogles2.cpp  
altona/main/base/npplugin.cpp         
altona/main/base/serialize.cpp
)

add_library(base ${ALTONA_BASE})

file(GLOB_RECURSE ALTONA_GUI altona/main/gui/*.cpp)
add_library(gui ${ALTONA_GUI})

#file(GLOB_RECURSE ALTONA_EXTRA altona/main/extra/*.cpp)
#add_library(extra ${ALTONA_EXTRA})

file(GLOB_RECURSE ALTONA_NET altona/main/network/*.cpp)
add_library(network ${ALTONA_NET})

file(GLOB_RECURSE ALTONA_OGG altona/main/ogg/*.cpp)
add_library(ogg ${ALTONA_OGG})

#file(GLOB_RECURSE ALTONA_SHADER altona/main/shadercomp/*.cpp)
#add_library(shader ${ALTONA_SHADER})

file(GLOB_RECURSE ALTONA_UTIL altona/main/util/*.cpp)
add_library(util ${ALTONA_UTIL})

file(GLOB_RECURSE ALTONA_WIKI altona/main/wiki/*.cpp)
add_library(wiki ${ALTONA_WIKI})

#file(GLOB_RECURSE ALTONA_WZ4 altona/main/wz4lib/*.cpp)
set(ALTONA_WZ4
altona/main/wz4lib/doc.cpp 
altona/main/wz4lib/gui.cpp 
altona/main/wz4lib/view.cpp 
altona/main/wz4lib/build.cpp 
altona/main/wz4lib/script.cpp 
altona/main/wz4lib/incbin.asm 
altona/main/wz4lib/wiki.cpp 
altona/main/wz4lib/videoencoder_win.cpp
altona/main/wz4lib/basic.cpp 
altona/main/wz4lib/poc.cpp 
#altona/main/wz4lib/poc_ops.ops 
altona/main/wz4lib/basic_ops.cpp 
altona/main/wz4lib/wz4shaders.cpp
)

#add_library(werkzeug ${ALTONA_WZ4})

file(GLOB_RECURSE WZ4OPS altona/tools/wz4ops/*.cpp)
add_executable(wz4ops ${WZ4OPS})
target_link_libraries(wz4ops base gui network ogg util wiki GL GLU pthread rt X11)

