FILE(GLOB SRC *.cpp *.h)

LIST(REMOVE_ITEM SRC ${CMAKE_CURRENT_SOURCE_DIR}/export_cb_dlg.cpp ${CMAKE_CURRENT_SOURCE_DIR}/builder_logic.cpp)

ENABLE_LANGUAGE(RC)
ADD_DEFINITIONS(${MFC_DEFINITIONS})
SET(CMAKE_MFC_FLAG 2)

ADD_EXECUTABLE(world_editor WIN32 ${SRC} world_editor.rc)

INCLUDE_DIRECTORIES(${LIBXML2_INCLUDE_DIR})

SOURCE_GROUP(Resources FILES world_editor.rc)

TARGET_LINK_LIBRARIES(world_editor	
					nelmisc
					nelligo
					nel3d
					nelgeorges
					nelpacs)

NL_DEFAULT_PROPS(world_editor "Ryzom, Tools, World: World Editor")
NL_ADD_RUNTIME_FLAGS(world_editor)

IF(WITH_PCH)
  ADD_NATIVE_PRECOMPILED_HEADER(world_editor ${CMAKE_CURRENT_SOURCE_DIR}/stdafx.h ${CMAKE_CURRENT_SOURCE_DIR}/stdafx.cpp)
ENDIF(WITH_PCH)

INSTALL(TARGETS world_editor RUNTIME DESTINATION ${RYZOM_BIN_PREFIX} COMPONENT tools)
