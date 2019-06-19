CMAKE_MINIMUM_REQUIRED( VERSION 3.7 )

if(POLICY CMP0060)
	cmake_policy(SET CMP0060 NEW)
endif(POLICY CMP0060) 
if(POLICY CMP0074)
	cmake_policy(SET CMP0074 NEW)
endif(POLICY CMP0074)

project(TinyXML
	VERSION 2.6.2
    LANGUAGES CXX)
    
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_C_STANDARD 11)

add_library(tinyxml SHARED)

set_target_properties(tinyxml
    PROPERTIES SOVERSION ${PROJECT_VERSION})

target_sources(tinyxml
    PRIVATE 
        tinystr.cpp
        tinyxml.cpp
        tinyxmlerror.cpp
        tinyxmlparser.cpp
        tinystr.h
        tinyxml.h)

target_include_directories(tinyxml
    PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    PUBLIC
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_PREFIX}/include>)

install(TARGETS tinyxml
    EXPORT TinyXML-exports
    LIBRARY DESTINATION "lib"
    ARCHIVE DESTINATION "lib"
    PUBLIC_HEADER DESTINATION "include"
    INCLUDES DESINATION "include")

install(EXPORT TinyXML-exports
    DESTINATION "lib/cmake")

install(FILES tinystr.h tinyxml.h
    DESTINATION "include")

install(DIRECTORY docs/
    DESTINATION "share/doc/${PROJECT_NAME}-${PROJECT_VERSION}")