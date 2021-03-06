add_library(gfxrecon_application STATIC "")

target_sources(gfxrecon_application
               PRIVATE
                    application.h
                    application.cpp
                    $<$<BOOL:${XCB_FOUND}>:xcb_application.h>
                    $<$<BOOL:${XCB_FOUND}>:xcb_window.h>
                    $<$<BOOL:${XCB_FOUND}>:xcb_application.cpp>
                    $<$<BOOL:${XCB_FOUND}>:xcb_window.cpp>
                    $<$<BOOL:${WAYLAND_FOUND}>:wayland_application.h>
                    $<$<BOOL:${WAYLAND_FOUND}>:wayland_window.h>
                    $<$<BOOL:${WAYLAND_FOUND}>:wayland_application.cpp>
                    $<$<BOOL:${WAYLAND_FOUND}>:wayland_window.cpp>
                    $<$<BOOL:${WIN32}>:win32_application.h>
                    $<$<BOOL:${WIN32}>:win32_window.h>
                    $<$<BOOL:${WIN32}>:win32_application.cpp>
                    $<$<BOOL:${WIN32}>:win32_window.cpp>
              )

target_include_directories(gfxrecon_application
                           PUBLIC
                               $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}>)

target_link_libraries(gfxrecon_application
                      gfxrecon_decode
                      gfxrecon_format
                      gfxrecon_util
                      vulkan_registry
                      platform_specific
                     )

common_build_directives(gfxrecon_application)

if (${RUN_TESTS})
    add_executable(gfxrecon_application_test "")

    target_sources(gfxrecon_application_test PRIVATE
            test/main.cpp)

    common_build_directives(gfxrecon_application_test)
    common_test_directives(gfxrecon_application_test)
endif()
