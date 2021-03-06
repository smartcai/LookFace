# RUN for C++ 11
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

include_directories(${BOOST_INCLUDE_DIR})

SET(SOURCE
    src/pico.cpp
)

SET(HEADERS
    includes/pico.h
)
include_directories(./includes)
include_directories(/usr/include/libxml2)

# add_library( FacePico STATIC ${SOURCE} ${HEADERS})
add_library( FacePico SHARED ${SOURCE} ${HEADERS})

install (TARGETS FacePico DESTINATION bin)
install (FILES HEADERS DESTINATION include)
