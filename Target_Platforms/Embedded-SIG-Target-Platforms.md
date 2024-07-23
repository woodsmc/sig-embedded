# Embedded SIG Target Platforms

## Purpose of this Document

This document defines the minimum hardware and software platforms that all contributions to the Embedded Special Interest Group should address. This document should define what devices and software platforms are in scope, and also what devices and platforms are out of scope.  

## Intended Audience

This document is intended to be read and contributed to by members of the Embedded Special Interest Group. 

## Criteria of Device and Software Selection

The hardware and software targeted in this document should be easily available to anyone who would like to contribute to the Embedded Special Interest Group. This means not just specifying a CPU architecture or model, but specifying a development platform / board which can be easily purchased by anyone wishing to contribute.

## Approach

In order to produce this document and narrow down the platforms selections we will follow the approach outlined below:

1. Select hardware instruction set
2. Define if MMU / MPU support is required
3. Define minimum RAM and storage requirements
4. Select RTOS / Operating Systems which need to be supported on the target hardware as defined in steps 1,2 and 3.
5. Select publicly available platforms which provide the best coverage for the selected hardware requirements.
6. Define the WebAssembly Runtimes that should be considered on the chosen platforms

## 1. Hardware Instruction Set Requirements (ISA)
The following hardware instructions sets should be supported:

1. Xtensa (32 bit)
2. RISC-V 32-bit + 64-bit
3. ARM (Thumb2) 32-bit + 64-bit
4. X86-64 bit

## 2. Hardware Memory Protection
Is recommended when possible, should select board and MMC which have this available. Software protection should be put in place, but comes with performance hit. TODO: Cleanup.
MPU should be compulsory. MMU should optional.
MMU / MPU support is optional. It should be possible to run on devices which do not have an MMU / MPU is not present. 

**NB:** This may mean that some features like shared memory, or the forth coming `mmap` support from core-wasm may not be possible to support without a large performance penalty. 



## 3. Minimum RAM and Storage Requirements

*TODO: This has not been discussed*

340kb - 512kb (half a meg) 

Storage : 1 meg.

## 4. Required RTOS / Operating System Requirements
The following RTOS / Operating Systems should be supported:

1. Zephyr (7 votes)
2. FreeRTOS (7 votes)
3. Linux (Optional, does this really have an impact? -> RT Patch) (7 votes)
4. RT-Thread (2 votes)
5. Android (2 votes)
6. NuttX (1 vote)
7. Windows (1 vote)
8. Eclipse Thread-X (1 vote)
9. ESP-IDF
10. iOS
13. MacOS


## 5. Publicly Available Hardware Platforms


- Nucleo U575ZI-Q: STM32U575ZI@160MHz (Cortex-M33), 786KB RAM, 2MB Flash (https://www.st.com/en/evaluation-tools/nucleo-u575zi-q.html and https://www.st.com/en/microcontrollers-microprocessors/stm32u575zi.html)
- Nucleo F412ZG: STM32F412ZG@100MHz (Cortex-M4), 256KB RAM, 1MB Flash (https://www.st.com/en/evaluation-tools/nucleo-f412zg.html and https://www.st.com/en/microcontrollers-microprocessors/stm32f412zg.html).
- NUCLEO-F429ZI or STM32F429I-DISC1: STM32F429ZI@180MHz (Cortex-M4), 256KB RAM, <=2MB Flash (https://www.st.com/en/evaluation-tools/nucleo-f429zi.html, https://www.st.com/en/evaluation-tools/32f429idiscovery.html and https://www.st.com/en/microcontrollers-microprocessors/stm32f429zi.html)
- Nordic nrf5340
- STM32 Nucleo-H563ZI
- Raspberry Pi 4/5
- ESP32 Devkit  8MB RAM 8MB flash
ESP32S3 Devkit 8MB RAM 16MB flash
ESP32 family has the kind of MMU to map SPIRAM to virtual memory, but no MPU
- https://docs.zephyrproject.org/latest/boards/index.html
- Atom E3940
- Xbox Series X as a dev kit

Questions around / peripherial support and connectivity, NB-IoT, etc.

The following table maps the ISA, memory protection support, RAM and Storage requirements with a reference implementation. This table will also highlight the platforms, or combination of platform requirements, which are not supported, e.g. an x86-64 bit processor without an MMU as this doesn't exist in the market place, or running Linux on a device without an MMU.

*NB: This might be better in an excel / spreadsheet*

| ISA       | MMU / MPU | RAM  | Storage | OS   | Board    |
| --------- | --------- | ---- | ------- | ---- | -------- |
| Xtensa    | None      | ?    | ?       |      |          |
| Xtensa    | MPU       | ?    | ?       |      |          |
| Xtensa    | MMU       | ?    | ?       |      |          |
| RISC-V 32 | None      | ?    | ?       |      |          |
| RISC-V 32 | MPU       | ?    | ?       |      |          |
| RISC-V 32 | MMU       | ?    | ?       |      |          |
| RISC-V 64 | None      | ?    | ?       |      |          |
| RISC-V 64 | MPU       | ?    | ?       |      |          |
| RISC-V 64 | MMU       | ?    | ?       |      |          |
| ARM 32    | None      | ?    | ?       |      |          |
| ARM 32    | MPU       | ?    | ?       |      |          |
| ARM 32    | MMU       | ?    | ?       |      |          |
| ARM 64    | None      | ?    | ?       |      |          |
| ARM 64    | MPU       | ?    | ?       |      |          |
| ARM 64    | MMU       | ?    | ?       |      |          |
| x86-64    | None      | ?    | ?       |      | Excluded |
| x86-64    | MPU       | ?    | ?       |      | Excluded |
| x86-64    | MMU       | ?    | ?       |      |          |

 

## 6. Runtime Support

The following runtimes should be supported:

1. WAMR
2. Wasmtime
3. Wazero
