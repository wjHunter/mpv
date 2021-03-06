INCLUDE_DIRECTORIES(include)
INCLUDE_DIRECTORIES(${OSG_INCLUDE_DIR})
INCLUDE_DIRECTORIES(${SDL_INCLUDE_DIR})

SET(osgSDL_PUBLIC_HDRS
    include/osgSDL/Cursor
    include/osgSDL/CursorChanger
    include/osgSDL/Export
    include/osgSDL/SDLEventAdapter
    include/osgSDL/TimeSource
    include/osgSDL/Viewer
    include/osgSDL/Viewport
    include/osgSDL/ViewportFocusHandler
    include/osgSDL/ViewportFrame
)
SET(osgSDL_SRCS
    src/osgSDL/Cursor.cpp
    src/osgSDL/Viewer.cpp
    src/osgSDL/Viewport.cpp
)

ADD_DEFINITIONS(-DOSGSDL_LIBRARY)

ADD_LIBRARY(osgSDL SHARED
    ${osgSDL_PUBLIC_HDRS} ${osgSDL_PRIVATE_HDRS} ${osgSDL_SRCS})
IF(CMAKE_MAJOR_VERSION EQUAL 2 AND
   CMAKE_MINOR_VERSION LESS 6)
    MPV_COPY_DLL_OUTPUT_TO_BINARY_DIR(osgSDL)
ENDIF()

SET_TARGET_PROPERTIES(osgSDL PROPERTIES
    DEFINE_SYMBOL OSGSDL_EXPORTS)

MPV_TARGET_LINK_OSG_LIBRARIES(osgSDL
    ${OSGGA_LIBRARY} ${OSGDB_LIBRARY} ${OSGUTIL_LIBRARY} ${OSG_LIBRARY})
TARGET_LINK_LIBRARIES(osgSDL
    ${SDL_LIBRARY}
    ${OPENGL_LIBRARIES})

INSTALL(TARGETS osgSDL
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib)
