add_executable(gfxrecon-toascii "")

target_sources(gfxrecon-toascii
               PRIVATE
                   main.cpp
              )

target_include_directories(gfxrecon-toascii PUBLIC ${CMAKE_BINARY_DIR})

target_link_libraries(gfxrecon-toascii gfxrecon_decode gfxrecon_format gfxrecon_util platform_specific)

common_build_directives(gfxrecon-toascii)

install(TARGETS gfxrecon-toascii RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
