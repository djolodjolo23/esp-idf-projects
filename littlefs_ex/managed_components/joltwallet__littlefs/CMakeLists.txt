cmake_minimum_required(VERSION 3.10)

# Gather source files
file(GLOB SOURCES src/littlefs/*.c)
list(APPEND SOURCES src/esp_littlefs.c src/littlefs_api.c src/lfs_config.c)

# Register the component with the required dependencies
idf_component_register(
    SRCS ${SOURCES}
    INCLUDE_DIRS include
    PRIV_INCLUDE_DIRS src
    PRIV_REQUIRES esptool_py spi_flash vfs esp_partition
)

# Set compilation flags for the source files
set_source_files_properties(
    ${SOURCES}
    PROPERTIES COMPILE_FLAGS "-DLFS_CONFIG=lfs_config.h"
)
