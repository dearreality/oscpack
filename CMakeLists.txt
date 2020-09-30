cmake_minimum_required(VERSION 2.6)
project(TestOscpack)

add_library(oscpack)

if (${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
    target_link_libraries(oscpack PRIVATE Ws2_32 winmm)
    set(IPSYSTEMTYPE_PATH source/win32)
elseif (${CMAKE_SYSTEM_NAME} STREQUAL "Darwin")
    set(IPSYSTEMTYPE_PATH source/posix)
endif ()

target_sources(oscpack PRIVATE
        source/IpEndpointName.cpp
        ${IPSYSTEMTYPE_PATH}/NetworkingUtils.cpp
        ${IPSYSTEMTYPE_PATH}/UdpSocket.cpp
        source/OscTypes.cpp
        source/OscReceivedElements.cpp
        source/OscPrintReceivedElements.cpp
        source/OscOutboundPacketStream.cpp)

target_include_directories(oscpack PUBLIC include)

