#
# Copyright 2019, Data61
# Commonwealth Scientific and Industrial Research Organisation (CSIRO)
# ABN 41 687 119 230.
#
# This software may be distributed and modified according to the terms of
# the BSD 2-Clause license. Note that NO WARRANTY is provided.
# See "LICENSE_BSD2.txt" for details.
#
# @TAG(DATA61_BSD)
#

cmake_minimum_required(VERSION 3.8.2)

project(ClockServer C)

CAmkESAddImportPath(camkes-include)
CAmkESAddCPPInclude(camkes-include)
CAmkESAddCPPInclude("${CMAKE_CURRENT_LIST_DIR}/include/plat/${KernelPlatform}/")
CAmkESAddTemplatesPath(templates)

DeclareCAmkESConnector(
    ClockServerInit
    FROM
    ClockServer.template.c
    FROM_LIBS
    ClockServer-server
    TO
    empty.c
)

DeclareCAmkESConnector(
    ClockServerClientInit
    FROM
    ClockServer-client.template.c
    FROM_LIBS
    ClockServer-client
    TO
    empty.c
)

if("${KernelPlatform}" STREQUAL "tx2")
    set(ClockServerExtraLibs platsupportports)
endif()

add_subdirectory(
    "${CMAKE_CURRENT_LIST_DIR}/libClockServer-client"
    ${CMAKE_CURRENT_BINARY_DIR}/libClockServer-client
)

add_library(ClockServer-server EXCLUDE_FROM_ALL src/clock_server.c)
target_link_libraries(ClockServer-server sel4camkes ${ClockServerExtraLibs})
