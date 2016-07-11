cmake_minimum_required (VERSION 2.8)

# Project name
project(TinyXML)

set(INSTALL_BIN_DIR "${CMAKE_INSTALL_PREFIX}/bin" CACHE PATH "Installation directory for executables")
set(INSTALL_LIB_DIR "${CMAKE_INSTALL_PREFIX}/lib" CACHE PATH "Installation directory for libraries")
set(INSTALL_INC_DIR "${CMAKE_INSTALL_PREFIX}/include" CACHE PATH "Installation directory for headers")
set(INSTALL_MAN_DIR "${CMAKE_INSTALL_PREFIX}/share/man" CACHE PATH "Installation directory for manual pages")
set(INSTALL_PKGCONFIG_DIR "${CMAKE_INSTALL_PREFIX}/share/pkgconfig" CACHE PATH "Installation directory for pkgconfig (.pc) files")

set(TINYXML_HDRS_DIR include)
set(TINYXML_SRCS_DIR src)

set(TINYXML_HDRS
	${TINYXML_HDRS_DIR}/tinystr.h
	${TINYXML_HDRS_DIR}/tinyxml.h)

set(TINYXML_SRCS
	${TINYXML_SRCS_DIR}/tinystr.cpp
	${TINYXML_SRCS_DIR}/tinyxml.cpp
	${TINYXML_SRCS_DIR}/tinyxmlerror.cpp
	${TINYXML_SRCS_DIR}/tinyxmlparser.cpp)

include_directories(${TINYXML_HDRS_DIR})

if(APPLE)
    set(CMAKE_MACOSX_RPATH 1)
endif()

set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11 -stdlib=libc++ -fno-rtti -g -Wall")
add_library(TinyXML STATIC ${TINYXML_SRCS} ${TINYXML_HDRS})

if(NOT SKIP_INSTALL_LIBRARIES AND NOT SKIP_INSTALL_ALL)
    install(TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION "${INSTALL_BIN_DIR}"
        ARCHIVE DESTINATION "${INSTALL_LIB_DIR}"
        LIBRARY DESTINATION "${INSTALL_LIB_DIR}")
endif()

if(NOT SKIP_INSTALL_HEADERS AND NOT SKIP_INSTALL_ALL)
    install(FILES ${TINYXML_HDRS} DESTINATION "${INSTALL_INC_DIR}")
endif()