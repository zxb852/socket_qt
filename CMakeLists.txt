cmake_minimum_required(VERSION 2.6)

project(socket_qt)
add_definitions(-D Linux)
set (Developing_VERSION_MAJOR 1)
set (Developing_VERSION_MINOR 0)
set( CMAKE_CXX_FLAGS "-std=c++11 -O3")

find_package(OpenCV REQUIRED)

message(STATUS "OpenCV library status:")
message(STATUS "    version: ${OpenCV_VERSION}")
message(STATUS "    libraries: ${OpenCV_LIBS}")
message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")


include_directories("../socket_connect/lib")
include_directories("../socket_connect/src/developing")
include_directories("../socket_connect/src/client")
include_directories("../socket_connect/src/server")
include_directories("../socket_connect/src/relay_server")


add_library(
                test-lib
                SHARED
                ../socket_connect/lib/socket_connect.cpp
                ../socket_connect/src/client/client.cpp
                ../socket_connect/src/server/server.cpp
                ../socket_connect/src/relay_server/relay_server.cpp
)

# add the executable
add_executable(test_server ../socket_connect/src/developing/server.cpp)
add_executable(test_client ../socket_connect/src/developing/client.cpp)
add_executable(client ../socket_connect/src/client/main.cpp)
add_executable(server ../socket_connect/src/server/main.cpp)
add_executable(relay_server ../socket_connect/src/relay_server/main.cpp)


target_link_libraries(test_server test-lib ${OpenCV_LIBS})
target_link_libraries(test_client test-lib ${OpenCV_LIBS})
target_link_libraries(client test-lib ${OpenCV_LIBS})
target_link_libraries(server test-lib ${OpenCV_LIBS})
target_link_libraries(relay_server test-lib ${OpenCV_LIBS})

