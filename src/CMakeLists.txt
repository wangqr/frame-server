cmake_minimum_required(VERSION 3.0)
project(frame-server)

add_compile_definitions(_UNICODE UNICODE)

add_library(common STATIC
    fscommon/autoupdate.cpp
    fscommon/blankavi.cpp
    fscommon/fscommon.cpp
    utils/utils.cpp
)
target_include_directories(common PRIVATE dfsc utils)

set(PREMIERE_INCLUDE_DIRS sdks/Premiere/Examples/Headers CACHE PATH "Path to Premiere SDK Examples directory")
if(NOT EXISTS "${PREMIERE_INCLUDE_DIRS}/PrSDKExport.h")
message( FATAL_ERROR "Premiere SDK not found." )
endif()

add_library(dfscPremiere SHARED PremiereV2/PremiereFS.cpp)
set_target_properties(dfscPremiere PROPERTIES SUFFIX ".prm")
target_include_directories(dfscPremiere PRIVATE "${PREMIERE_INCLUDE_DIRS}" fscommon dfsc utils)
target_link_libraries(dfscPremiere common rpcrt4 wininet Winmm)

add_executable(DFsNetClient WIN32 NetClient/NetClient.cpp)
target_include_directories(DFsNetClient PRIVATE fscommon dfsc utils)
target_link_libraries(DFsNetClient rpcrt4 wininet Winmm Ws2_32)

add_executable(DFsNetServer WIN32 NetServer/NetServer.cpp)
target_include_directories(DFsNetServer PRIVATE fscommon dfsc utils)
target_link_libraries(DFsNetServer rpcrt4 wininet Ws2_32)