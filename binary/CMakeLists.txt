# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
INCLUDE(FindProtobuf)
FIND_PACKAGE(Protobuf REQUIRED)
INCLUDE_DIRECTORIES(${PROTOBUF_INCLUDE_DIR})
PROTOBUF_GENERATE_CPP(IR_SRC IR_HEADER expression.proto extensions.proto function.proto
        parameterized_types.proto plan.proto relations.proto selection.proto type.proto
        type_expressions.proto)
ADD_LIBRARY(substrait_IR_proto ${IR_HEADER} ${IR_SRC})

target_link_libraries(substrait_IR_proto ${Protobuf_LIBRARIES})
target_include_directories(substrait_IR_proto
        PUBLIC ${CMAKE_CURRENT_BINARY_DIR}/../../)