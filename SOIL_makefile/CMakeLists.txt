cmake_minimum_required( VERSION 2.6)

PROJECT( SOIL )

set (SOURCEFILES
	src/image_DXT.c
	src/image_helper.c
	src/SOIL.c
	src/stb_image_aug.c
)

set (HEADERFILES
	src/image_DXT.h
	src/image_helper.h
	src/SOIL.h
	src/stb_image_aug.h
	src/stbi_DDS_aug.h
	src/stbi_DDS_aug_c.h
)
source_group("Header Files" FILES ${HEADERFILES})

include_directories( "${CMAKE_SOURCE_DIR}/src" )

if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
  # Linux specific code
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11") 
	set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS}")
endif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

if (MSVC)
	# Windows specific code
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP")
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /MP")
endif (MSVC)

add_library( SOIL STATIC ${SOURCEFILES} )

install(TARGETS SOIL DESTINATION lib)
install(FILES SOIL.h DESTINATION include)