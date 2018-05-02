cmake_minimum_required (VERSION 3.10)
project(vkglformat LANGUAGES CXX)

add_library(vkglformat INTERFACE)
target_include_directories(vkglformat SYSTEM INTERFACE
		${CMAKE_CURRENT_LIST_DIR}/include
	)

install(TARGETS vkglformat
		EXPORT vkglformat-dev
		DESTINATION lib
		COMPONENT vkglformat-dev
	)

export(
		EXPORT vkglformat-dev 
		NAMESPACE vkglformat::
		FILE vkglformatConfig.cmake
	)
