
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS 1)
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -DDEBUG")


# Build rules for MD4C parser library

configure_file(md4c.pc.in md4c.pc @ONLY)
# for CSPro ... building everything as one library
# add_library(md4c md4c.c md4c.h)
add_library(md4c md4c.c md4c.h md4c-html.c md4c-html.h entity.c entity.h)
set_target_properties(md4c PROPERTIES
    COMPILE_FLAGS "-DMD4C_USE_UTF8"
    VERSION ${MD_VERSION}
    SOVERSION ${MD_VERSION_MAJOR}
    PUBLIC_HEADER "md4c.h;md4c-html.h;entity.h"
)

# Install rules

install(
    TARGETS md4c
    EXPORT md4cConfig
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/md4c
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
