cmake_minimum_required(VERSION 2.6)

project(lsclient)

include(GNUInstallDirs)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)

SET (CMAKE_CXX_FLAGS       "-g -O3 -std=c++11 -fPIC")
SET (CMAKE_LINKER_FLAGS    "-rdynamic")

add_library(
        lsclient SHARED
        src/utils.cpp
        src/lsclient.cpp
        src/lstable.cpp
        src/lssubscription.cpp
        src/http.cpp
)

add_executable(
  sample
  sample.cpp
)

find_library (CURL curl)

target_link_libraries(
  lsclient
  curl
)
target_include_directories(lsclient PUBLIC include)

target_link_libraries(
  sample
  lsclient
)

install(TARGETS lsclient
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/lsclient)
