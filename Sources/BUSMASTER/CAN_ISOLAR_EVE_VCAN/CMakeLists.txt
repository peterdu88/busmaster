set(sources
  CAN_ISOLAR_EVE_VCAN.cpp
  CAN_ISOLAR_EVE_VCAN_stdafx.cpp)

set(headers
  CAN_ISOLAR_EVE_VCAN.h
  CAN_ISOLAR_EVE_VCAN_Defines.h
  CAN_ISOLAR_EVE_VCAN_Extern.h
  CAN_ISOLAR_EVE_VCAN_stdafx.h)

add_library(CAN_ISOLAR_EVE_VCAN SHARED ${sources} ${headers})

include_directories(
  ..
  ${ICONV_INCLUDE_DIR}
  ${LIBXML2_INCLUDE_DIR}
  ${ATL_INCLUDE_DIRS}
  ${MFC_INCLUDE_DIRS})

# compiler options
add_definitions(-D_USRDLL)

# linker options
set_target_properties(CAN_ISOLAR_EVE_VCAN PROPERTIES LINK_FLAGS "/NODEFAULTLIB:daouuid")
target_link_libraries(CAN_ISOLAR_EVE_VCAN
  Advapi32
  DataTypes
  Utils)

# installer options
add_custom_command(
  TARGET CAN_ISOLAR_EVE_VCAN
  POST_BUILD
  COMMAND ${CMAKE_COMMAND} ARGS -E make_directory ${PROJECT_SOURCE_DIR}/BIN/${CMAKE_BUILD_TYPE}/
  COMMAND ${CMAKE_COMMAND} ARGS -E copy $<TARGET_FILE:CAN_ISOLAR_EVE_VCAN> ${PROJECT_SOURCE_DIR}/BIN/${CMAKE_BUILD_TYPE}/
  COMMAND ${CMAKE_COMMAND} ARGS -E copy ${CMAKE_CURRENT_SOURCE_DIR}/Controller_0.dll ${PROJECT_SOURCE_DIR}/BIN/${CMAKE_BUILD_TYPE}/
  COMMAND ${CMAKE_COMMAND} ARGS -E copy ${CMAKE_CURRENT_SOURCE_DIR}/Controller_1.dll ${PROJECT_SOURCE_DIR}/BIN/${CMAKE_BUILD_TYPE}/)
