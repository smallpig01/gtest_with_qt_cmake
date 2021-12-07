cmake_minimum_required(VERSION 3.5)

# custom project name and
set(MY_PROJECT_NAME "gtest_with_cmake")
# custom google test path
set(MY_GOOGLETEST_DIR "googletest")

project(${MY_PROJECT_NAME} LANGUAGES CXX)
set (CMAKE_CXX_STANDARD 11)
add_definitions(-DGTEST_LANGUAGE_CXX11)

# set google teset relate include path and source
if ($ENV{GOOGLETEST_DIR})
    set(GOOGLETEST_DIR $ENV{GOOGLETEST_DIR})
else ()
    if (NOT "" STREQUAL "")
        message(WARNING "Using googletest src dir specified at Qt Creator wizard")
    endif ()
    set(GOOGLETEST_DIR ${MY_GOOGLETEST_DIR})
endif ()

if (EXISTS ${GOOGLETEST_DIR})
    set(GTestSrc ${GOOGLETEST_DIR}/googletest)
    set(GMockSrc ${GOOGLETEST_DIR}/googlemock)
elseif (UNIX AND EXISTS /usr/src/gtest)
    set(GTestSrc /usr/src/gtest)
    message(WARNING "Using gtest from system")
    if (EXISTS /usr/src/gmock)
        set(GMockSrc /usr/src/gmock)
    endif ()
else ()
    message( FATAL_ERROR "No googletest src dir found - set GOOGLETEST_DIR to enable!")
endif ()

set(GTestFiles ${GTestSrc}/src/gtest-all.cc)
set(GTestIncludes ${GTestSrc} ${GTestSrc}/include)
if (NOT ${GMockSrc} STREQUAL "")
    list(APPEND GTestFiles ${GMockSrc}/src/gmock-all.cc)
    list(APPEND GTestIncludes ${GMockSrc} ${GMockSrc}/include)
endif ()

# set project link
include_directories(${GTestIncludes})
add_executable(${MY_PROJECT_NAME}
    main.cpp
    tst_case.h
    ${GTestFiles})
add_test(NAME ${MY_PROJECT_NAME} COMMAND ${MY_PROJECT_NAME})

# using Threads
find_package(Threads REQUIRED)
target_link_libraries(${MY_PROJECT_NAME} PRIVATE Threads::Threads)
