# Copyright (c) 2020 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

add_subdirectory(TARGET_NUCLEO_F401RE EXCLUDE_FROM_ALL)

if(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
    set(STARTUP_FILE TOOLCHAIN_GCC_ARM/startup_stm32f401xe.S)
    set(LINKER_FILE TOOLCHAIN_GCC_ARM/STM32F401XE.ld)
elseif(${MBED_TOOLCHAIN} STREQUAL "ARM")
    set(STARTUP_FILE TOOLCHAIN_ARM/startup_stm32f401xe.S)
    set(LINKER_FILE TOOLCHAIN_ARM/stm32f401xe.sct)
endif()

add_library(mbed-stm32f401xe INTERFACE)

target_sources(mbed-stm32f401xe
    INTERFACE
        ${STARTUP_FILE}
)

target_include_directories(mbed-stm32f401xe
    INTERFACE
        .
)

mbed_set_linker_script(mbed-stm32f401xe ${CMAKE_CURRENT_SOURCE_DIR}/${LINKER_FILE})

target_link_libraries(mbed-stm32f401xe INTERFACE mbed-stm32f4)
