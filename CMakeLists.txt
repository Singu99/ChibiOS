# Minimum required CMake version
cmake_minimum_required(VERSION 3.22.1)

#### CONFIGURATION ####
set(CHIBIOS_CONFIG_DIR ${PROJECT_DIR}/cfg)
set(CHIBIOS_BOARD_DIR ${PROJECT_DIR}/cfg/board)
set(CHIBIOS_BOARD_SRC ${CHIBIOS_BOARD_DIR}/board.c)

#### LICENSE ####
set(CHIBIOS_LICENSE_INC ${CHIBIOS_DIR}/os/license)

#### STARTUP ####
set(CHIBIOS_STARTUP_SRC
    ${CHIBIOS_DIR}/os/common/startup/ARMCMx/compilers/GCC/crt0_v7m.S
    ${CHIBIOS_DIR}/os/common/startup/ARMCMx/compilers/GCC/vectors.S
    ${CHIBIOS_DIR}/os/common/startup/ARMCMx/compilers/GCC/crt1.c    
    )   # TODO

set(CHIBIOS_STARTUP_INC 
    ${CHIBIOS_DIR}/os/common/portability/GCC
    ${CHIBIOS_DIR}/os/common/startup/ARMCMx/compilers/GCC
    ${CHIBIOS_DIR}/os/common/startup/ARMCMx/devices/STM32H7xx
    ${CHIBIOS_DIR}/os/common/ext/ARM/CMSIS/Core/Include
    ${CHIBIOS_DIR}/os/common/ext/ST/STM32H7xx
    ${CHIBIOS_CONFIG_DIR}
    ${CHIBIOS_BOARD_DIR}
)

#### LINKER ####
set(MCU_LINKER_SCRIPT ${CHIBIOS_DIR}/os/common/startup/ARMCMx/compilers/GCC/ld/STM32H723xG_ITCM64k.ld)      # TODO
set(CHIBIOS_LINKER_INC ${CHIBIOS_DIR}/os/common/startup/ARMCMx/compilers/GCC/ld)


#### RT ####
set(CHIBIOS_RTOS_SRC
    ## RT ##
    ${CHIBIOS_DIR}/os/rt/src/chsys.c 
    ${CHIBIOS_DIR}/os/rt/src/chrfcu.c 
    ${CHIBIOS_DIR}/os/rt/src/chdebug.c 
    ${CHIBIOS_DIR}/os/rt/src/chtrace.c 
    ${CHIBIOS_DIR}/os/rt/src/chvt.c 
    ${CHIBIOS_DIR}/os/rt/src/chschd.c 
    ${CHIBIOS_DIR}/os/rt/src/chinstances.c 
    ${CHIBIOS_DIR}/os/rt/src/chthreads.c 
    ${CHIBIOS_DIR}/os/rt/src/chtm.c 
    ${CHIBIOS_DIR}/os/rt/src/chstats.c 
    ${CHIBIOS_DIR}/os/rt/src/chregistry.c 
    ${CHIBIOS_DIR}/os/rt/src/chsem.c 
    ${CHIBIOS_DIR}/os/rt/src/chmtx.c 
    ${CHIBIOS_DIR}/os/rt/src/chcond.c 
    ${CHIBIOS_DIR}/os/rt/src/chevents.c 
    ${CHIBIOS_DIR}/os/rt/src/chmsg.c 
    ${CHIBIOS_DIR}/os/rt/src/chdynamic.c

    ## PORT ##
    ${CHIBIOS_DIR}/os/common/ports/ARMv7-M/chcore.c
    ${CHIBIOS_DIR}/os/common/ports/ARMv7-M/compilers/GCC/chcoreasm.S

)

set(CHIBIOS_RTOS_INC
    ## RT ##
    ${CHIBIOS_DIR}/os/rt/include

    ## PORT ##
    ${CHIBIOS_DIR}/os/common/portability/GCC
    ${CHIBIOS_DIR}/os/common/ports/ARM-common
    ${CHIBIOS_DIR}/os/common/ports/ARMv7-M
)

#### HAL ####
set(CHIBIOS_HAL_OSAL_SRC
    ## HAL ##
    ${CHIBIOS_DIR}/os/rt/src/chsys.c 
    ${CHIBIOS_DIR}/os/rt/src/chrfcu.c 
    ${CHIBIOS_DIR}/os/rt/src/chdebug.c 
    ${CHIBIOS_DIR}/os/rt/src/chtrace.c 
    ${CHIBIOS_DIR}/os/rt/src/chvt.c 
    ${CHIBIOS_DIR}/os/rt/src/chschd.c 
    ${CHIBIOS_DIR}/os/rt/src/chinstances.c 
    ${CHIBIOS_DIR}/os/rt/src/chthreads.c
    ${CHIBIOS_DIR}/os/hal/src/hal.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_st.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_buffers.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_queues.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_flash.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_mmcsd.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_adc.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_can.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_crypto.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_dac.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_efl.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_gpt.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_i2c.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_i2s.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_icu.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_mac.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_mmc_spi.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_pal.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_pwm.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_rtc.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_sdc.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_serial.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_serial_usb.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_sio.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_spi.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_trng.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_uart.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_usb.c 
    ${CHIBIOS_DIR}/os/hal/src/hal_wdg.c 
    # ${CHIBIOS_DIR}/os/hal/src/hal_wspi.c

    ## Platform ##
    ${CHIBIOS_DIR}/os/hal/ports/common/ARMCMx/nvic.c 
    ${CHIBIOS_DIR}/os/hal/ports/STM32/STM32H7xx/stm32_isr.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/STM32H7xx/hal_lld.c

    ### Drivers compatible with the platform ###
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/ADCv4/hal_adc_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/BDMAv1/stm32_bdma.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/CRYPv1/hal_crypto_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/DACv1/hal_dac_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/DMAv2/stm32_dma.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/EXTIv1/stm32_exti.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/FDCANv1/hal_can_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/GPIOv2/hal_pal_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/I2Cv3/hal_i2c_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/MACv2/hal_mac_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/MDMAv1/stm32_mdma.c
    # ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/OCTOSPIv2/hal_wspi_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/OTGv1/hal_usb_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/SDMMCv2/hal_sdc_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/SPIv3/hal_spi_v2_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/RNGv1/hal_trng_lld.c
    # ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/RTCv2/hal_rtc_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/SYSTICKv1/hal_st_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/TIMv1/hal_gpt_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/TIMv1/hal_icu_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/TIMv1/hal_pwm_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/USARTv3/hal_serial_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/USARTv3/hal_serial_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/USARTv3/hal_sio_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/USARTv3/hal_uart_lld.c
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/xWDGv1/hal_wdg_lld.c

    ## OSAL ##
    ${CHIBIOS_DIR}/os/hal/osal/rt-nil/osal.c

)

set(CHIBIOS_HAL_OSAL_INC
    ## HAL ##
    ${CHIBIOS_DIR}/os/hal/include

    ## Platform ##
    ${CHIBIOS_DIR}/os/hal/ports/common/ARMCMx
    ${CHIBIOS_DIR}/os/hal/ports/STM32/STM32H7xx

    ### Drivers compatible with the platform ###
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/ADCv4
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/BDMAv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/CRYPv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/DACv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/DMAv2
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/EXTIv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/FDCANv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/GPIOv2
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/I2Cv3
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/MACv2
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/MDMAv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/OCTOSPIv2
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/OTGv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/SDMMCv2
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/SPIv3
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/RNGv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/RTCv2
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/SYSTICKv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/TIMv1
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/USARTv3
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/USART
    ${CHIBIOS_DIR}/os/hal/ports/STM32/LLD/xWDGv1

    ## OSAL ##
    ${CHIBIOS_DIR}/os/hal/osal/rt-nil
)

#### OSLIB ####
set(CHIBIOS_OSLIB_SRC 
    ${CHIBIOS_DIR}/os/oslib/src/chmemchecks.c
    ${CHIBIOS_DIR}/os/oslib/src/chmemchecks.c
    ${CHIBIOS_DIR}/os/oslib/src/chmboxes.c 
    ${CHIBIOS_DIR}/os/oslib/src/chmemcore.c 
    ${CHIBIOS_DIR}/os/oslib/src/chmemheaps.c 
    ${CHIBIOS_DIR}/os/oslib/src/chmempools.c 
    ${CHIBIOS_DIR}/os/oslib/src/chpipes.c 
    ${CHIBIOS_DIR}/os/oslib/src/chobjcaches.c
    ${CHIBIOS_DIR}/os/oslib/src/chdelegates.c
    ${CHIBIOS_DIR}/os/oslib/src/chfactory.c
)

set(CHIBIOS_OSLIB_INC
    ${CHIBIOS_DIR}/os/oslib/include
)

#### CHIBIOS ####
set(CHIBIOS_SRC
    ${CHIBIOS_BOARD_SRC}
    ${CHIBIOS_STARTUP_SRC}
    ${CHIBIOS_RTOS_SRC}
    ${CHIBIOS_HAL_OSAL_SRC}
    ${CHIBIOS_OSLIB_SRC}
)

set(CHIBIOS_INC
    ${CHIBIOS_STARTUP_INC}
    ${CHIBIOS_RTOS_INC}
    ${CHIBIOS_HAL_OSAL_INC}
    ${CHIBIOS_LICENSE_INC}
    ${CHIBIOS_OSLIB_INC}
    ${CHIBIOS_LINKER_INC}
    PARENT_SCOPE
)

# Create the static library
add_library(ChibiOS STATIC
   ${CHIBIOS_SRC}
   ${STARTUP_SRC}
)

# Add header directories (AFTER add_library !!)
target_include_directories(ChibiOS PUBLIC
    ${CHIBIOS_INC})

# Embedded macros(defines)
 target_compile_definitions(ChibiOS PRIVATE
    ${MCU_MODEL}
    ${MCU_FAMILY}
    #USE_STDPERIPH_DRIVER
    #USE_DEFAULT_TIMEOUT_CALLBACK
    #USE_HAL_DRIVER
    #CMSIS_device_header="${CMSIS_DEVICE_HEADER}"
    )


# Compiler and linker options
target_compile_options(ChibiOS PRIVATE
    ${CPU_PARAMETERS}
    -Wall
    -Wextra
    -Wpedantic
    -Wno-unused-parameter
    $<$<COMPILE_LANGUAGE:CXX>:
        -Wno-volatile
        -Wno-old-style-cast
        -Wuseless-cast
        -Wsuggest-override
        -Werror>
    $<$<CONFIG:Debug>:-Og -g3 -ggdb>
    $<$<CONFIG:Release>:-O3 -g0>)       # Maximum optimization on realease

target_link_options(ChibiOS PRIVATE
    -T${MCU_LINKER_SCRIPT}
    ${CPU_PARAMETERS}
    -Wl,-Map=${CMAKE_PROJECT_NAME}.map
    --specs=nosys.specs
    -Wl,--start-group
    -lc
    -lm
    -lstdc++
    -Wl,--end-group
    -Wl,--print-memory-usage
    LINKER:-L${CHIBIOS_DIR}/os/common/startup/ARMCMx/compilers/GCC/ld)