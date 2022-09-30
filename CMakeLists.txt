cmake_minimum_required( VERSION 3.24 )
project( gcmake-emscripten-targets )

if( NOT TARGET emscripten_NODEFS )
  add_library( emscripten_NODEFS INTERFACE )
  add_library( emscripten::NODEFS ALIAS emscripten_NODEFS )
  target_link_libraries( emscripten_NODEFS
    INTERFACE
      "$<$<AND:$<BOOL:${USING_EMSCRIPTEN}>,$<STREQUAL:${EMSCRIPTEN_MODE},NodeJS>>:nodefs.js>"
  )
endif()

if( NOT TARGET emscripten_IDBFS )
  add_library( emscripten_IDBFS INTERFACE )
  add_library( emscripten::IDBFS ALIAS emscripten_IDBFS )
  target_link_libraries( emscripten_IDBFS
    INTERFACE
      "$<$<AND:$<BOOL:${USING_EMSCRIPTEN}>,$<STREQUAL:${EMSCRIPTEN_MODE},Browser>>:idbfs.js>"
  )
endif()

if( NOT TARGET emscripten_WORKERFS )
  add_library( emscripten_WORKERFS INTERFACE )
  add_library( emscripten::WORKERFS ALIAS emscripten_WORKERFS )
  target_link_libraries( emscripten_WORKERFS
    INTERFACE
      "$<$<BOOL:${USING_EMSCRIPTEN}>:workerfs.js>"
  )
endif()

if( NOT TARGET emscripten_PROXYFS )
  add_library( emscripten_PROXYFS INTERFACE )
  add_library( emscripten::PROXYFS ALIAS emscripten_PROXYFS )
  target_link_libraries( emscripten_PROXYFS
    INTERFACE
      "$<$<BOOL:${USING_EMSCRIPTEN}>:proxyfs.js>"
  )
endif()