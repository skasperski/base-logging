add_library(logging
	logging/logging_printf_style.cpp
)

target_include_directories(logging
	PUBLIC
		$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
		$<INSTALL_INTERFACE:include>
)

target_link_libraries(logging
	PUBLIC
		base::types
)

set_target_properties(logging PROPERTIES
	OUTPUT_NAME base-logging
)

# Install header files
install(DIRECTORY ./
	DESTINATION ${INCLUDE_DESTINATION}
	FILES_MATCHING PATTERN "*.hpp"
)

# Install the binary
install(TARGETS logging EXPORT logging-targets)

# Install pkg-config file
configure_file(base-logging.pc.in base-logging.pc @ONLY)
install(
	FILES ${PROJECT_BINARY_DIR}/base/base-logging.pc
	DESTINATION ${PKGCONFIG_DESTINATION}
)

