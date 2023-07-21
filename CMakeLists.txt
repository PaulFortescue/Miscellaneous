cmake_minimum_required(VERSION 3.12)
include(${PICO_SDK_PATH}/pico_sdk_init.cmake)

project(PicoSDKProject4 C CXX ASM)
pico_sdk_init()

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
cmake_minimum_required(VERSION 3.13)

add_executable(host_cdc_msc_hid
  usb_descriptors.c
  msc_app.c
  msc_disk.c)
# Example source
target_sources(host_cdc_msc_hid PUBLIC
        ${CMAKE_CURRENT_LIST_DIR}/main.c
        )

# Make sure TinyUSB can find tusb_config.h
target_include_directories(host_cdc_msc_hid PUBLIC
        ${CMAKE_CURRENT_LIST_DIR})

# In addition to pico_stdlib required for common PicoSDK functionality, add dependency on tinyusb_host
# for TinyUSB device support and tinyusb_board for the additional board support library used by the example
target_link_libraries(host_cdc_msc_hid PUBLIC pico_stdlib tinyusb_host tinyusb_board tinyusb_device )
pico_add_extra_outputs(host_cdc_msc_hid)

pico_add_extra_outputs(host_cdc_msc_hid)
set_source_files_properties(tusb_config.h PROPERTIES HEADER_FILE_ONLY TRUE)

# add url via pico_set_program_url
# example_auto_set_url(host_cdc_msc_hid)
