set(PROJECT_BIN  libplist)
set(PROJECT_NAME LibPlist)
project(${PROJECT_NAME})

# find libxml2
find_package(LibXml2 REQUIRED)

# includes
include_directories(
	${LIBXML2_INCLUDE_DIR}
	${CMAKE_SOURCE_DIR}/include
	${CMAKE_SOURCE_DIR}/include/libcnary
	${CMAKE_SOURCE_DIR}/source
)

# sources
set(LIBPLIST_SOURCES
	${CMAKE_SOURCE_DIR}/source/base64.c
	${CMAKE_SOURCE_DIR}/source/bplist.c
	${CMAKE_SOURCE_DIR}/source/bytearray.c
	${CMAKE_SOURCE_DIR}/source/hashtable.c
	${CMAKE_SOURCE_DIR}/source/plist.c
	${CMAKE_SOURCE_DIR}/source/ptrarray.c
	${CMAKE_SOURCE_DIR}/source/xplist.c
	
	${CMAKE_SOURCE_DIR}/source/Array.cpp
	${CMAKE_SOURCE_DIR}/source/Boolean.cpp
	${CMAKE_SOURCE_DIR}/source/Data.cpp
	${CMAKE_SOURCE_DIR}/source/Date.cpp
	${CMAKE_SOURCE_DIR}/source/Dictionary.cpp
	${CMAKE_SOURCE_DIR}/source/Integer.cpp
	${CMAKE_SOURCE_DIR}/source/Key.cpp
	${CMAKE_SOURCE_DIR}/source/Node.cpp
	${CMAKE_SOURCE_DIR}/source/Real.cpp
	${CMAKE_SOURCE_DIR}/source/String.cpp
	${CMAKE_SOURCE_DIR}/source/Structure.cpp
	${CMAKE_SOURCE_DIR}/source/Uid.cpp
	
	${CMAKE_SOURCE_DIR}/source/libcnary/cnary.c
	${CMAKE_SOURCE_DIR}/source/libcnary/iterator.c
	${CMAKE_SOURCE_DIR}/source/libcnary/list.c
	${CMAKE_SOURCE_DIR}/source/libcnary/node.c
	${CMAKE_SOURCE_DIR}/source/libcnary/node_iterator.c
	${CMAKE_SOURCE_DIR}/source/libcnary/node_list.c
)

# use win_iconv when compiling under msvc
if(MSVC)
	include_directories(${CMAKE_SOURCE_DIR}/include/win_iconv)
	set(LIBPLIST_SOURCES ${LIBPLIST_SOURCES}
		${CMAKE_SOURCE_DIR}/source/win_iconv/win_iconv.c
	)
endif()

add_library(${PROJECT_BIN} SHARED
	${LIBPLIST_SOURCES}
)

target_link_libraries(${PROJECT_BIN}
	${LIBXML2_LIBRARIES}
)
