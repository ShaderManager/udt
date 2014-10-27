cmake_minimum_required(VERSION 2.6)

project(UDT)

set( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/bin )
set( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/bin )
set( CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/lib )

option(BUILD_SHARED "Build shared library" ON)

set(public_headers src/udt.h)

set(sources 
	src/api.cpp src/api.h
	src/buffer.cpp src/buffer.h
	src/cache.cpp src/cache.h
	src/ccc.cpp src/ccc.h
	src/channel.cpp src/channel.h
	src/common.cpp src/common.h
	src/core.cpp src/core.h
	src/epoll.cpp src/epoll.h
	src/list.cpp src/list.h
	src/md5.cpp src/md5.h
	src/packet.cpp src/packet.h
	src/queue.cpp src/queue.h
	src/window.cpp src/window.h
	${public_headers}
)

if (UNIX)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -Wall -Wextra -DLINUX -fno-strict-aliasing -fvisibility=hidden")
endif ()

if (MSVC)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4 /WX /wd4267 /wd4127")
endif ()

if (BUILD_SHARED)
	add_library(UDT SHARED ${sources})
else ()
	add_definitions(-DUDT_STATIC)
	add_library(UDT STATIC ${sources})
endif ()

if (UNIX)
	target_link_libraries(UDT pthread)
elseif (WIN32)
	target_link_libraries(UDT ws2_32)
endif ()

install(TARGETS UDT RUNTIME DESTINATION bin LIBRARY DESTINATION lib ARCHIVE DESTINATION lib)
install(FILES ${public_headers} DESTINATION include)
install(DIRECTORY doc DESTINATION .)