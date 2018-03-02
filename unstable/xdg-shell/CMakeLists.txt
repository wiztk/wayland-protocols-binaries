# Copyright 2017 - 2018 Freeman Zhang <zhanggyb@gmail.com>
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

set(XDG_SHELL_V6_XML ${WAYLAND_PROTOCOLS_SOURCE_DIR}/unstable/xdg-shell/xdg-shell-unstable-v6.xml)
set(XDG_SHELL_V6_CLIENT_HEADER "xdg-shell-unstable-v6-client-protocol.h")
set(XDG_SHELL_V6_SERVER_HEADER "xdg-shell-unstable-v6-server-protocol.h")
set(XDG_SHELL_V6_SOURCE "xdg-shell-unstable-v6-protocol.c")

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
        COMMENT "Generate xdg shell v6 protocol source files."
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

install(TARGETS xdg-shell-unstable-v6
        DESTINATION unstable/xdg-shell)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/${XDG_SHELL_V6_CLIENT_HEADER}"
        DESTINATION unstable/xdg-shell)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/${XDG_SHELL_V6_SERVER_HEADER}"
        DESTINATION unstable/xdg-shell)
