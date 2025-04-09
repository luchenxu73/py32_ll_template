cmake_minimum_required(VERSION 3.22)

project(stm32cubemx)
add_library(stm32cubemx STATIC)

# Enable CMake support for ASM and C languages
enable_language(C ASM)

target_compile_definitions(stm32cubemx PUBLIC
        USE_FULL_LL_DRIVER
        HSE_VALUE=8000000
        LSE_VALUE=32768
        HSI_VALUE=16000000
        LSI_VALUE=32000
        PY32F003x8
        $<$<CONFIG:Debug>:DEBUG>
)

target_include_directories(stm32cubemx PUBLIC
        ../../Drivers/PY32F0xx_HAL_Driver/Inc
        ../../Drivers/CMSIS/Device/PY32F0xx/Include
        ../../Drivers/CMSIS/Include
)

target_sources(stm32cubemx PRIVATE
        ../../Drivers/PY32F0xx_HAL_Driver/Src/py32f0xx_ll_utils.c
        ../../Drivers/PY32F0xx_HAL_Driver/Src/py32f0xx_ll_exti.c
        ../../Drivers/PY32F0xx_HAL_Driver/Src/py32f0xx_ll_pwr.c
        ../../Drivers/PY32F0xx_HAL_Driver/Src/py32f0xx_ll_gpio.c
        ../../Drivers/PY32F0xx_HAL_Driver/Src/py32f0xx_ll_rcc.c
)

target_link_directories(stm32cubemx PRIVATE
)

target_link_libraries(stm32cubemx PRIVATE
)

# Validate that STM32CubeMX code is compatible with C standard
if (CMAKE_C_STANDARD LESS 11)
    message(ERROR "Generated code requires C11 or higher")
endif ()


