cmake_minimum_required(VERSION 3.23)
project(watcher)
add_library(watcher INTERFACE)
add_library(watcher::watcher ALIAS watcher)
target_sources(watcher INTERFACE
	FILE_SET HEADERS
	BASE_DIRS include/wtr
	FILES
		include/wtr/watcher.hpp
)
include(CMakePackageConfigHelpers)
install(TARGETS watcher EXPORT watcher-targets FILE_SET HEADERS DESTINATION include/wtr)
install(EXPORT watcher-targets FILE watcher-targets.cmake NAMESPACE watcher:: DESTINATION lib/cmake/watcher)
configure_package_config_file(
    "${CMAKE_CURRENT_LIST_DIR}/cmake/watcher-config.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/watcher-config.cmake"
    INSTALL_DESTINATION lib/cmake/watcher
)
install(FILES "${CMAKE_CURRENT_BINARY_DIR}/watcher-config.cmake" DESTINATION lib/cmake/watcher)
