cmake_minimum_required(VERSION 3.8)
project(sds)

set(CMAKE_CXX_STANDARD 11)

file(GLOB SOURCES
        *.h
        *.cpp
        )

add_library(sds ${SOURCES})


include(ExternalProject)

ExternalProject_Add(zmalloc
        GIT_REPOSITORY https://github.com/iNevd/zmalloc.git
        CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=<INSTALL_DIR>
        )

ExternalProject_Get_Property(zmalloc INSTALL_DIR)
MESSAGE( STATUS "zmalloc INSTALL_DIR:        " ${INSTALL_DIR} )

include_directories(${INSTALL_DIR}/include)
link_directories(${INSTALL_DIR}/libstatic)


install(TARGETS sds
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION libstatic)

install(FILES ${PROJECT_SOURCE_DIR}/sds.h DESTINATION include)