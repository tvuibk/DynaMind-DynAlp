FILE(GLOB MODULE_CPPS *.cpp)
FILE(GLOB MODULE_HEADER *.h)

INCLUDE_DIRECTORIES(.)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})

ADD_LIBRARY(DynAlp SHARED ${MODULE_CPPS} ${MODULE_H})

IF(${CMAKE_CXX_COMPILER_ID} STREQUAL GNU)
		SET_TARGET_PROPERTIES(DynAlp PROPERTIES COMPILE_FLAGS "-frounding-math -fPIC")
ENDIF()

TARGET_LINK_LIBRARIES(DynAlp ${DYNAMIND_TOOLBOX_LIBRARY} ${DYNAMIND_CORE_LIBRARY} ${DYNAMIND_EXTENSIONS_LIBRARY} ${QT_LIBRARIES} ${CGAL_LIBRARIES} ${CGAL_3RD_PARTY_LIBRARIES} ${GDAL_LIBRARY})

INSTALL(TARGETS DynAlp
		DESTINATION "lib/DynaMind"
		PERMISSIONS OWNER_READ OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)
