cmake_minimum_required(VERSION 3.1)
project(base-logging VERSION 1.0)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

find_package(base-types)

# Where to install .cmake, .pc and .hpp files
set(CMAKE_DESTINATION      ${CMAKE_INSTALL_LIBDIR}/cmake/base-logging)
set(PKGCONFIG_DESTINATION  ${CMAKE_INSTALL_LIBDIR}/pkgconfig)
set(INCLUDE_DESTINATION    ${CMAKE_INSTALL_INCLUDEDIR}/base)

add_subdirectory(base)

# Export the library interface
install(EXPORT logging-targets
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

