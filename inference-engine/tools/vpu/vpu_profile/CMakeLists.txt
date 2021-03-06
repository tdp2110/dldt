#
# Copyright (C) 2018-2019 Intel Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

set(TARGET_NAME vpu_profile)

file(GLOB SOURCES
    ${IE_MAIN_SOURCE_DIR}/tools/vpu/common/*.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp
)

add_executable(${TARGET_NAME} ${SOURCES})

if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    target_compile_options(${TARGET_NAME} PRIVATE
        "-Wall"
    )
endif()

target_include_directories(${TARGET_NAME} SYSTEM PRIVATE
    "${IE_MAIN_SOURCE_DIR}/include"
    "${IE_MAIN_SOURCE_DIR}/src/inference_engine"
    "${IE_MAIN_SOURCE_DIR}/samples/common"
    "${IE_MAIN_SOURCE_DIR}/samples/common/format_reader"
    "${IE_MAIN_SOURCE_DIR}/tools/vpu/common"
)

target_link_libraries(${TARGET_NAME} PRIVATE
    inference_engine format_reader vpu_graph_transformer
    gflags
)

set_target_properties(${TARGET_NAME} PROPERTIES COMPILE_PDB_NAME ${TARGET_NAME})

add_cpplint_target(${TARGET_NAME}_cpplint FOR_TARGETS ${TARGET_NAME})

