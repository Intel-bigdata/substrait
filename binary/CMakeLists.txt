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