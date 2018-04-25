cmake_minimum_required (VERSION 3.7)
project(vkglformat)

add_library(vkglformat INTERFACE)
target_include_directories(vkglformat SYSTEM INTERFACE
		${CMAKE_CURRENT_LIST_DIR}/include
	)
