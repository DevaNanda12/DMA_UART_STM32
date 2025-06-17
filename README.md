# UART DMA Echo with IDLE Detection

## Overview
This project demonstrates how to receive UART data using DMA and handle reception termination using the UART IDLE line detection feature on the STM32F4 (Nucleo-F446RE) board. Received data is echoed back through the same UART interface.

## Features
- UART2 communication at 115200 baud
- DMA-based UART reception
- Uses IDLE line interrupt to detect end of message
- Echoes received data back to sender
- Circular buffer implementation for continuous reception

## Hardware Requirements
- STM32 Nucleo-F446RE (or similar STM32F4 series board)
- USB-to-Serial connection to USART2 (typically via ST-Link virtual COM port)
- Serial terminal (e.g., CoolTerm, PuTTY)

## Pin Configuration
- **USART2_TX**: PA2  
- **USART2_RX**: PA3  
- **LED Output (Optional)**: PA5

## How It Works
1. DMA is initialized to receive data into a circular buffer.
2. The IDLE line interrupt triggers when no data is received for 1 frame duration.
3. In the interrupt handler, the number of bytes received is calculated.
4. The received bytes are processed and echoed back via UART.

## File Structure
- `main.c` – Main application logic, UART + DMA setup, IDLE interrupt, data echo
- `stm32f4xx_it.c` – Contains IRQ handler for UART IDLE detection (to be implemented)
- `main.h` – Header declarations for peripherals
- `system_stm32f4xx.c` – System initialization and clock config

## Notes
- Ensure `USART2` and `DMA1_Stream5` are properly configured in STM32CubeMX.
- The project assumes a fixed RX buffer size of 64 bytes.
- This project does not parse or process commands — it simply echoes back input.

## TODO
- Add proper IDLE line interrupt handler in `stm32f4xx_it.c`
- Optional: Implement newline-based message termination

## Author
Deva Nanda S

