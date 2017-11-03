
set(XDG_SHELL_V6_XML ${WAYLAND_PROTOCOLS_SOURCE_DIR}/unstable/xdg-shell/xdg-shell-unstable-v6.xml)
set(XDG_SHELL_V6_CLIENT_HEADER "xdg-shell-unstable-v6-client-protocol.h")
set(XDG_SHELL_V6_SERVER_HEADER "xdg-shell-unstable-v6-server-protocol.h")
set(XDG_SHELL_V6_SOURCE "xdg-shell-unstable-v6-protocol.c")

#message(STATUS "Generate XDG shell v6 protocol:")
#execute_process(
#        COMMAND ${WAYLAND_SCANNER} client-header ${XDG_SHELL_V6_XML} ${XDG_SHELL_V6_CLIENT_HEADER}
#        COMMAND ${WAYLAND_SCANNER} server-header ${XDG_SHELL_V6_XML} ${XDG_SHELL_V6_SERVER_HEADER}
#        COMMAND ${WAYLAND_SCANNER} code ${XDG_SHELL_V6_XML} ${XDG_SHELL_V6_SOURCE}
#        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
#)

add_library(
        xdg-shell-unstable-v6
        ${XDG_SHELL_V6_CLIENT_HEADER}
        ${XDG_SHELL_V6_SERVER_HEADER}
        ${XDG_SHELL_V6_SOURCE}
)

add_custom_target(
        xdg_shell_generate_protocol
        COMMAND ${WAYLAND_SCANNER} client-header ${XDG_SHELL_V6_XML} ${XDG_SHELL_V6_CLIENT_HEADER}
        COMMAND ${WAYLAND_SCANNER} server-header ${XDG_SHELL_V6_XML} ${XDG_SHELL_V6_SERVER_HEADER}
        COMMAND ${WAYLAND_SCANNER} code ${XDG_SHELL_V6_XML} ${XDG_SHELL_V6_SOURCE}
        DEPENDS ${XDG_SHELL_V6_XML}
        COMMENT "Generate xdg shell v6 protocol source files"
        VERBATIM
)

set_source_files_properties(
        ${XDG_SHELL_V6_CLIENT_HEADER}
        PROPERTIES
        GENERATED TRUE
)

set_source_files_properties(
        ${XDG_SHELL_V6_SERVER_HEADER}
        PROPERTIES
        GENERATED TRUE
)

set_source_files_properties(
        ${XDG_SHELL_V6_SOURCE}
        PROPERTIES
        GENERATED TRUE
)

add_dependencies(
        xdg-shell-unstable-v6
        xdg_shell_generate_protocol
)
