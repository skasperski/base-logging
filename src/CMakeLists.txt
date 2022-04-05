add_library(logging
	logging_printf_style.cpp
)

target_include_directories(logging
	PUBLIC
		$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>/src
		$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

target_link_libraries(logging
	PUBLIC
		base::types
)

set_target_properties(logging PROPERTIES
	OUTPUT_NAME base-logging
)

# Install header files
install(DIRECTORY base
	DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
	FILES_MATCHING PATTERN "*.hpp"
)

# Install the binary
install(TARGETS logging EXPORT base-logging-targets)

# Install pkg-config file
configure_file(base-logging.pc.in base-logging.pc @ONLY)
install(
	FILES ${PROJECT_BINARY_DIR}/src/base-logging.pc
	DESTINATION ${PKGCONFIG_DESTINATION}
)

