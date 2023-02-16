#THIS FILE IS AUTO GENERATED FROM THE TEMPLATE! DO NOT CHANGE!
set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_VERSION 1)
cmake_minimum_required(VERSION 3.16)

# specify cross-compilers and tools
set(CMAKE_C_COMPILER riscv-none-elf-gcc)
set(CMAKE_CXX_COMPILER riscv-none-elf-g++)
set(CMAKE_ASM_COMPILER  riscv-none-elf-gcc)
set(CMAKE_AR riscv-none-elf-ar)
set(CMAKE_OBJCOPY riscv-none-elf-objcopy)
set(CMAKE_OBJDUMP riscv-none-elf-objdump)
set(SIZE riscv-none-elf-size)
set(CMAKE_TRY_COMPILE_TARGET_TYPE STATIC_LIBRARY)

# project settings
project(CH32V307_GPIO_TOGGLE C CXX ASM)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_C_STANDARD 11)


add_compile_options(-march=rv32imac_zicsr_zifencei -mabi=ilp32)
add_compile_options(-O0 -g)
add_compile_options(-msmall-data-limit=8 -mno-save-restore
-fmessage-length=0 -fsigned-char -ffunction-sections -fdata-sections
-Wunused -Wuninitialized -MMD)

# Enable assembler files preprocessing
add_compile_options($<$<COMPILE_LANGUAGE:ASM>:-x$<SEMICOLON>assembler-with-cpp>)

include_directories(Inc RISCV/Core RISCV/Peripheral/inc RISCV/Debug)

#file(GLOB_RECURSE SOURCES "Startup/*.*" "Src/*.*" "RISCV/Core/*.*" "RISCV/Debug/*.*" "RISCV/Peripheral/*.*" "RISCV/Startup/*.*"  "RISCV/stubs/*.*")
file(GLOB_RECURSE SOURCES "Startup/*.*" "Src/*.*" "RISCV/Core/*.*" "RISCV/Debug/*.*" "RISCV/Peripheral/*.*" "RISCV/Startup/*.*")

set(LINKER_SCRIPT ${CMAKE_SOURCE_DIR}/RISCV/Ld/Link.ld)

add_link_options(-msmall-data-limit=8 -mno-save-restore
        -fmessage-length=0 -fsigned-char -ffunction-sections -fdata-sections
        -Wunused -Wuninitialized -MMD)
add_link_options(-Wl,-gc-sections,--print-memory-usage,-Map=${PROJECT_BINARY_DIR}/${PROJECT_NAME}.map)
add_link_options(-T ${LINKER_SCRIPT})
add_link_options(-nostartfiles)
add_link_options(-march=rv32imac_zicsr_zifencei -mabi=ilp32)
add_link_options(-specs=nano.specs)
#add_link_options(-specs=nosys.specs)

add_executable(${PROJECT_NAME}.elf ${SOURCES} ${LINKER_SCRIPT})

set(HEX_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.hex)
set(BIN_FILE ${PROJECT_BINARY_DIR}/${PROJECT_NAME}.bin)

add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} -Oihex $<TARGET_FILE:${PROJECT_NAME}.elf> ${HEX_FILE}
        COMMAND ${CMAKE_OBJCOPY} -Obinary $<TARGET_FILE:${PROJECT_NAME}.elf> ${BIN_FILE}
        COMMENT "Building ${HEX_FILE}
Building ${BIN_FILE}")
