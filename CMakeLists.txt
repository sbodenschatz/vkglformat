cmake_minimum_required (VERSION 3.10)
project(vkglformat LANGUAGES CXX)

add_library(vkglformat INTERFACE)
target_include_directories(vkglformat SYSTEM INTERFACE
		${CMAKE_CURRENT_LIST_DIR}/include
	)

install(
		TARGETS vkglformat
		EXPORT vkglformat-dev
		DESTINATION lib
		COMPONENT vkglformat-dev
	)

export(
		EXPORT vkglformat-dev 
		NAMESPACE vkglformat::
		FILE vkglformatConfig.cmake
	)

install(
		DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
		DESTINATION include
		COMPONENT vkglformat-dev
	)

if(NOT TARGET vkglformat::vkglformat)
	add_library(vkglformat::vkglformat INTERFACE IMPORTED GLOBAL)
	target_link_libraries(vkglformat::vkglformat INTERFACE vkglformat)
endif()

add_custom_target(
	install-vkglformat-dev
	DEPENDS vkglformat
	COMMAND
		"${CMAKE_COMMAND}" -DCMAKE_INSTALL_COMPONENT=vkglformat-dev -DCMAKE_INSTALL_CONFIG_NAME="$<CONFIG>" -P "${CMAKE_CURRENT_BINARY_DIR}/cmake_install.cmake"
)
