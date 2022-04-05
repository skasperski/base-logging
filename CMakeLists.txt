cmake_minimum_required(VERSION 3.9)
project(base-logging
	VERSION 2.0.0
	DESCRIPTION "Basic logging utilities."
)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

find_package(base-types)

# Where to install .cmake, .pc and .hpp files
set(CMAKE_DESTINATION      ${CMAKE_INSTALL_LIBDIR}/cmake/base-logging)
set(PKGCONFIG_DESTINATION  ${CMAKE_INSTALL_LIBDIR}/pkgconfig)

add_subdirectory(src)

# Export the library interface
install(EXPORT base-logging-targets
	NAMESPACE base::
	DESTINATION ${CMAKE_DESTINATION}
)

# Create and install the version file
write_basic_package_version_file("base-logging-config-version.cmake"
	COMPATIBILITY SameMajorVersion
)

install(
	FILES
		base-logging-config.cmake
		${PROJECT_BINARY_DIR}/base-logging-config-version.cmake
	DESTINATION
		${CMAKE_DESTINATION}
)

