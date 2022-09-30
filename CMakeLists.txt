cmake_minimum_required( VERSION 3.24 )
project( gcmake-emscripten-compat
  VERSION "1.0.0"
)

if( NOT TARGET emscripten-compat_NODEFS )
  add_library( emscripten-compat_NODEFS INTERFACE )
  add_library( emscripten::emscripten-compat_NODEFS ALIAS emscripten-compat_NODEFS )
  target_link_libraries( emscripten-compat_NODEFS
    INTERFACE
      # Even when building for the browser, node is still able to run the .js output file.
      "$<$<BOOL:${USING_EMSCRIPTEN}>:nodefs.js>"
      # "$<$<AND:$<BOOL:${USING_EMSCRIPTEN}>,$<STREQUAL:${EMSCRIPTEN_MODE},NodeJS>>:nodefs.js>"
  )
  target_compile_definitions( emscripten-compat_NODEFS
    INTERFACE
      "$<$<BOOL:${USING_EMSCRIPTEN}>:EMSCRIPTEN_NODEFS_ENABLED=1>"
      # "$<$<AND:$<BOOL:${USING_EMSCRIPTEN}>,$<STREQUAL:${EMSCRIPTEN_MODE},NodeJS>>:EMSCRIPTEN_NODEFS_ENABLED=1>"
  )
endif()

if( NOT TARGET emscripten-compat_IDBFS )
  add_library( emscripten-compat_IDBFS INTERFACE )
  add_library( emscripten::emscripten-compat_IDBFS ALIAS emscripten-compat_IDBFS )
  target_link_libraries( emscripten-compat_IDBFS
    INTERFACE
      "$<$<AND:$<BOOL:${USING_EMSCRIPTEN}>,$<STREQUAL:${EMSCRIPTEN_MODE},Browser>>:idbfs.js>"
  )
  target_compile_definitions( emscripten-compat_IDBFS
    INTERFACE
      "$<$<AND:$<BOOL:${USING_EMSCRIPTEN}>,$<STREQUAL:${EMSCRIPTEN_MODE},Browser>>:EMSCRIPTEN_IDBFS_ENABLED=1>"
  )
endif()

if( NOT TARGET emscripten-compat_WORKERFS )
  add_library( emscripten-compat_WORKERFS INTERFACE )
  add_library( emscripten::emscripten-compat_WORKERFS ALIAS emscripten-compat_WORKERFS )
  target_link_libraries( emscripten-compat_WORKERFS
    INTERFACE
      "$<$<BOOL:${USING_EMSCRIPTEN}>:workerfs.js>"
  )
  target_compile_definitions( emscripten-compat_WORKERFS
    INTERFACE
      "$<$<BOOL:${USING_EMSCRIPTEN}>:EMSCRIPTEN_WORKERFS_ENABLED=1>"
  )
endif()

if( NOT TARGET emscripten-compat_PROXYFS )
  add_library( emscripten-compat_PROXYFS INTERFACE )
  add_library( emscripten::emscripten-compat_PROXYFS ALIAS emscripten-compat_PROXYFS )
  target_link_libraries( emscripten-compat_PROXYFS
    INTERFACE
      "$<$<BOOL:${USING_EMSCRIPTEN}>:proxyfs.js>"
  )
  target_compile_definitions( emscripten-compat_PROXYFS
    INTERFACE
      "$<$<BOOL:${USING_EMSCRIPTEN}>:EMSCRIPTEN_PROXYFS_ENABLED=1>"
  )
endif()

install(
  TARGETS
    emscripten-compat_IDBFS
    emscripten-compat_NODEFS
    emscripten-compat_PROXYFS
    emscripten-compat_WORKERFS
  EXPORT ${PROJECT_NAME}Targets
  LIBRARY
    DESTINATION lib
  ARCHIVE
    DESTINATION lib
)

install( EXPORT ${PROJECT_NAME}Targets
  FILE ${PROJECT_NAME}Targets.cmake
  NAMESPACE "emscripten::"
  DESTINATION "lib/cmake/${PROJECT_NAME}"
)

include( CMakePackageConfigHelpers )

configure_package_config_file( "${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
  INSTALL_DESTINATION "lib/cmake"
)

write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake"
  VERSION "${PROJECT_VERSION}"
  COMPATIBILITY AnyNewerVersion
)

install( FILES 
  "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake"
  "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake"
  DESTINATION "lib/cmake/${PROJECT_NAME}"
)

export( EXPORT ${PROJECT_NAME}Targets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Targets.cmake"
  NAMESPACE "emscripten::"
)
