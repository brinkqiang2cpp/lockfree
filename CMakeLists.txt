cmake_minimum_required(VERSION 3.2)

PROJECT(lockfree)

LIST(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
INCLUDE(cmake/ModuleImport.cmake)
INCLUDE(cmake/ModuleCompileOptions.cmake)
ModuleSetCompileOptions()

SET(LOCKFREE_VERSION_MAJOR "1")
SET(LOCKFREE_VERSION_MINOR "0")
SET(LOCKFREE_VERSION_PATCH "1")
SET(LOCKFREE_VERSION "${LOCKFREE_VERSION_MAJOR}.${LOCKFREE_VERSION_MINOR}.${LOCKFREE_VERSION_PATCH}")

MESSAGE(STATUS "VERSION: ${LOCKFREE_VERSION}")

OPTION(USE_LOCKFREE "use lockfree" OFF)
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/include/lockfree_config.h.in ${CMAKE_CURRENT_SOURCE_DIR}/include/lockfree_config.h)

ModuleImport("dmlog" "thirdparty/dmlog")
LibImport("lockfree" "src/lockfree_module")
ExeImport("test" "lockfree;dmlog")

#ADD_CUSTOM_COMMAND(
#TARGET lockfreetest
#PRE_BUILD
#COMMAND ${CMAKE_COMMAND} -E copy_if_different
#${CMAKE_CURRENT_SOURCE_DIR}/config/test.csv
#$<TARGET_FILE_DIR:lockfreetest>
#)

#INSTALL(DIRECTORY include/ DESTINATION include)
#INSTALL(TARGETS lockfree
#        RUNTIME DESTINATION bin
#        LIBRARY DESTINATION lib
#        ARCHIVE DESTINATION lib)

#SET(LOCKFREE_LIBS "lockfree")
#MARK_AS_ADVANCED(${LOCKFREE_LIBS})