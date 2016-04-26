cmake_minimum_required(VERSION 3.5)
project(yuan)
include_directories(src)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(CUCKOO_FILTER_FILES src/cuckoo_filter/cuckoofilter.h src/cuckoo_filter/hashutil.cc src/cuckoo_filter/hashutil.h src/cuckoo_filter/debug.h src/cuckoo_filter/bitsutil.h src/cuckoo_filter/packedtable.h src/cuckoo_filter/permencoding.h src/cuckoo_filter/singletable.h)
set(SOURCE_FILES src/main.cpp src/common.h src/pbtree/pbtree.cpp src/pbtree/pbtree.h src/pctree/pctree.cpp src/pctree/pctree.h src/scan/scan.cpp src/scan/scan.h)

add_subdirectory(src/libbf)
add_executable(yuan ${SOURCE_FILES} ${CUCKOO_FILTER_FILES})

# Search OpenSSL
find_package(PkgConfig REQUIRED)
pkg_search_module(OPENSSL REQUIRED openssl)
include_directories(${OPENSSL_INCLUDE_DIRS})
message(STATUS "Using OpenSSL ${OPENSSL_VERSION}")
target_link_libraries(yuan ${OPENSSL_LIBRARIES})
