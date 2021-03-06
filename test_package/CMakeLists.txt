project(PackageTest CXX)
cmake_minimum_required(VERSION 2.8.12)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(SKIP_RPATH)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR})
find_package(LibRDKafka)

find_package(Threads)
find_package(ZLIB)

message(INFO "libc++ =  ${LibRDKafka_LIBRARIES}")
message(INFO "libc = ${LibRDKafka_C_LIBRARIES}")

# also see https://github.com/edenhill/librdkafka/tree/master/packaging/cmake for static linking
add_definitions(-DLIBRDKAFKA_STATICLIB)

add_executable(example example.cpp)
target_link_libraries(
  example
  ${LibRDKafka_LIBRARIES}
  ${LibRDKafka_C_LIBRARIES}
  ${CMAKE_THREAD_LIBS_INIT}
  ${ZLIB_LIBRARIES}
  ${CMAKE_DL_LIBS}
)
