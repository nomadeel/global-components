#
# Copyright 2020, Data61
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

project(dynamic-untyped-allocators-package C)

CAmkESAddImportPath(camkes-include)
CAmkESAddCPPInclude(camkes-include)
CAmkESAddTemplatesPath(templates)

DeclareCAmkESConnector(
    DynamicUntypedAllocatorEnvironment
    FROM
    dynamic-untyped-allocators.template.c
    FROM_HEADER
    dynamic-untyped-allocators.template.h
    FROM_LIBS
    sel4allocman
    TO
    empty.c
)
