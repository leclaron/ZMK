# Find Zephyr. This also loads Zephyr's build system.
cmake_minimum_required(VERSION 3.13.1)

list(APPEND BOARD_ROOT ${CMAKE_SOURCE_DIR})
list(APPEND DTS_ROOT ${CMAKE_SOURCE_DIR})

# Add our custom Zephyr module for drivers w/ syscalls, etc.
list(APPEND DTS_ROOT ${CMAKE_SOURCE_DIR}/drivers/zephyr)

list(APPEND ZEPHYR_EXTRA_MODULES
  ${CMAKE_CURRENT_SOURCE_DIR}/drivers
)
list(APPEND SYSCALL_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/drivers/zephyr)

include(cmake/keymap.cmake)

find_package(Zephyr)
project(zmk)


if(EXISTS ${KEYMAP_DIR}/keymap.c)
	target_sources(app PRIVATE ${KEYMAP_DIR}/keymap.c)
endif()


# Add your source file to the "app" target. This must come after
# find_package(Zephyr) which defines the target.
target_include_directories(app PRIVATE include)
target_sources(app PRIVATE src/kscan.c)
target_sources(app PRIVATE src/keymap.c)
target_sources(app PRIVATE src/hid.c)
target_sources_ifdef(CONFIG_ZMK_BLE app PRIVATE src/ble.c)
target_sources_ifdef(CONFIG_ZMK_KSCAN_MOCK_DRIVER app PRIVATE src/kscan_mock.c)
target_sources_ifdef(CONFIG_ZMK_KSCAN_COMPOSITE_DRIVER app PRIVATE src/kscan_composite.c)
target_sources_ifdef(CONFIG_ZMK_USB app PRIVATE src/usb_hid.c)
target_sources_ifdef(CONFIG_ZMK_BLE app PRIVATE src/hog.c)
target_sources(app PRIVATE src/endpoints.c)
target_sources(app PRIVATE src/main.c)
target_sources(app PRIVATE src/handlers.c)

