cmake_minimum_required(VERSION 2.8)

# Project Name
PROJECT(Engine3)

if (NOT APPLE)
	if (WIN32)
		set(GLEW_ROOT_FOLDER "" CACHE PATH "Path to GLEW folder")
		include_directories(${GLEW_ROOT_FOLDER})
		link_directories(${GLEW_ROOT_FOLDER})
	else(WIN32)
		find_package(GLEW REQUIRED)
		include_directories(${GLEW_INCLUDE_DIRS})
		link_libraries(${GLEW_LIBRARIES})
	endif(WIN32)
endif(NOT APPLE)

find_package(GLUT REQUIRED)
include_directories(${GLUT_INCLUDE_DIR})
link_directories(${GLUT_LIBRARY_DIRS})
add_definitions(${GLUT_DEFINITIONS})

find_package(OpenGL REQUIRED)
include_directories(${OpenGL_INCLUDE_DIRS})
link_directories(${OpenGL_LIBRARY_DIRS})
add_definitions(${OpenGL_DEFINITIONS})

add_executable(${PROJECT_NAME} main.cpp)


if (WIN32)
	target_link_libraries(${PROJECT_NAME} ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} glew32)
else(WIN32)
	target_link_libraries(${PROJECT_NAME} ${OPENGL_LIBRARIES} ${GLUT_LIBRARY})
endif (WIN32)
