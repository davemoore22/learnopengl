cmake_minimum_required(VERSION 3.1.6)
project(LearnOpenGL VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_THREAD_PREFER_PTHREAD TRUE)
set(THREADS_PREFER_PTHREAD_FLAG TRUE)
set(CMAKE_BUILD_PARALLEL_LEVEL 3)
set(OpenGL_GL_PREFERENCE LEGACY)

find_package(Threads REQUIRED)
find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)
find_package(X11 REQUIRED)

add_executable(${PROJECT_NAME}
	inc/glad/glad.c
	src/main.cpp)

include_directories(
	${CMAKE_SOURCE_DIR}/inc
	${GLFW3_INCLUDE_DIR}
	${OPENGL_INCLUDE_DIR}
	/usr/include
	/usr/include/X11
)

target_compile_options(${PROJECT_NAME} PRIVATE
	-Wall
	-Wextra
	-Wpedantic
	-Wunreachable-code
	-Wunused
	-Wignored-qualifiers
	-Wcast-align
	-Wformat-nonliteral
	-Wformat=2
	-Winvalid-pch
	-Wmissing-declarations
	-Wmissing-format-attribute
	-Wmissing-include-dirs
	-Wredundant-decls
	-Wswitch-default
	-Wodr
	-Wfatal-errors
	-fdiagnostics-color=always
	-pthread
	-pg
	-g)

target_link_libraries(${PROJECT_NAME} PRIVATE
	Threads::Threads 
	GL
	dl
	glfw
	X11
	pthread
	)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
