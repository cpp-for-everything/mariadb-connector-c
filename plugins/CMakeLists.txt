SET(PLUGIN_EXTRA_FILES ${CC_SOURCE_DIR}/libmariadb/ma_errmsg.c)

IF(WIN32 OR (CMAKE_C_COMPILER_ID MATCHES "GNU|Clang"))
  # Plugin exports handled via declspec(dllexport) or visibility attribute
  SET(CMAKE_C_VISIBILITY_PRESET hidden)
ENDIF()

FILE(GLOB plugin_dirs ${CC_SOURCE_DIR}/plugins/*)
FOREACH(dir ${plugin_dirs})
  IF (EXISTS ${dir}/CMakeLists.txt)
    INCLUDE(${dir}/CMakeLists.txt)
  ENDIF()
ENDFOREACH()
