# Copyright (C) 2018-2019 Intel Corporation
# SPDX-License-Identifier: Apache-2.0
#

if (ENABLE_MYRIAD)
    set(XLINK_DIR "${IE_MAIN_SOURCE_DIR}/thirdparty/movidius/XLink" CACHE PATH "path to Xlink")
    add_subdirectory("${XLINK_DIR}" "${CMAKE_BINARY_DIR}/thirdparty/movidius/XLink")

    add_subdirectory(
        "${IE_MAIN_SOURCE_DIR}/thirdparty/movidius/mvnc"
        "${CMAKE_BINARY_DIR}/thirdparty/movidius/mvnc")


    if(ENABLE_TESTS)
        add_subdirectory(tests)
    endif()
endif()
