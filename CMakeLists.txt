cmake_minimum_required(VERSION 3.0.2)

set(CMAKE_C_COMPILER_INIT g++)

project(fun_sfml)

include_directories(include)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")

find_package(SFML 2 REQUIRED network audio graphics window system)
if (SFML_FOUND)
	include_directories(${SFML_INCLUDE_DIR})
endif ()

add_subdirectory(src)

foreach (execFile ${EXECUTABLES})
	get_filename_component(execName ${execFile} NAME_WE)

	set(${execName} "fun_sfml")
	add_executable(${execName} ${execFile})
	target_link_libraries(${execName} ${SFML_LIBRARIES} ${SFML_DEPENDENCIES})

	install(TARGETS ${execName} DESTINATION bin)
endforeach ()
