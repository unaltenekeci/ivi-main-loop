
set(LIBRARY_SOURCE_FILES ivi-main-loop.cpp
                         UNIXSignalHandler.cpp
)

if(ENABLE_GLIB_BACKEND)
    set(LIBRARY_SOURCE_FILES ${LIBRARY_SOURCE_FILES} glib/ivi-main-loop-glib.cpp)
    set(LIBRARY_LINK_LIBRARIES ${LIBRARY_LINK_LIBRARIES} ${GLIB_LIBRARIES})
endif()

add_library( ivi-main-loop SHARED
	${LIBRARY_SOURCE_FILES}
)

set(INCLUDE_FOLDER ../include)
include_directories(${INCLUDE_FOLDER})

set_target_properties(ivi-main-loop PROPERTIES VERSION ${PACKAGE_VERSION} SOVERSION ${API_MAJOR_VERSION})

TARGET_LINK_LIBRARIES( ivi-main-loop
   ${LOGGING_LIBRARIES}
   ${LIBRARY_LINK_LIBRARIES}
)

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -nostdlib -fno-exceptions -fno-rtti")

INSTALL(TARGETS ivi-main-loop
  DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

#set(INCLUDE_FILES ${INCLUDE_FOLDER}/glib/ivi-main-loop-glib.h)

#INSTALL(FILES ${INCLUDE_FILES}
#  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PACKAGE_NAME}/glib
#)
