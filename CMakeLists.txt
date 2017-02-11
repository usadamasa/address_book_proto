cmake_minimum_required(VERSION 3.6)
project("testproto" "CXX")

# for protobuf
find_package(Protobuf REQUIRED)
PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS
        AddressBook.proto)
include_directories(${PROTOBUF_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS
        "-Wno-deprecated-declarations")

add_executable (writer
        ${PROTO_SRCS}
        ${PROTO_HDRS}
        writer.cpp)

add_executable (reader
        ${PROTO_SRCS}
        ${PROTO_HDRS}
        reader.cpp)

target_link_libraries(writer ${PROTOBUF_LIBRARIES})
target_link_libraries(reader ${PROTOBUF_LIBRARIES})
