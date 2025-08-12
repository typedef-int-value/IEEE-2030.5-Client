CMAKE_MINIMUM_REQUIRED (VERSION 3.1)

project (ieee2030.5_client)

if(CMAKE_COMPILER_IS_GNUCXX)
    add_compile_options (-std=c++17 -fpermissive)
endif()

if (MSVC_VERSION GREATER_EQUAL "1900")
    include(CheckCXXCompilerFlag)
    CHECK_CXX_COMPILER_FLAG("/std:c++latest" _cpp_latest_flag_supported)
    if (_cpp_latest_flag_supported)
        add_compile_options("/std:c++latest")
    endif()
endif()

file(GLOB_RECURSE PROJECT_SOURCES CONFIGURE_DEPENDS
        se_core.c
        client_test.c
)

file(GLOB_RECURSE CSIP_SOURCES CONFIGURE_DEPENDS
        se_core.c
        csip_test.c
)

add_executable(client_test ${PROJECT_SOURCES})
target_link_libraries(client_test ssl crypto pthread)

add_executable(csip_test ${CSIP_SOURCES})
target_link_libraries(csip_test ssl crypto pthread)