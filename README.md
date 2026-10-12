# STM32 FreeRTOS Button Press Counter

## 1. Introduction
This project demonstrates a **Button Press Counter using STM32 and FreeRTOS**. It uses two FreeRTOS tasks to detect button presses and display the total count through UART communication.

A mutex is used to protect the shared counter variable and ensure safe communication between tasks.

## 2. Objectives
- Understand multitasking using FreeRTOS.
- Detect button presses using GPIO.
- Count the number of button presses.
- Display the counter value using UART.
- Implement mutex synchronization between tasks.

## 3. Software Requirements
- STM32CubeIDE
- STM32CubeMX (integrated with STM32CubeIDE)
- FreeRTOS with CMSIS-RTOS2
- Serial Terminal (PuTTY, Tera Term, or equivalent)

## 4. Hardware Requirements
- STM32 Microcontroller
- Push Button
- USB-to-UART Converter
- Connecting Wires
- Power Supply

## 5. Working Principle

The project uses two main FreeRTOS tasks:

**Task 1: ButtonTask**
- Continuously monitors the push button connected to PC13.
- Detects a valid button press.
- Uses a debounce delay of 30 ms.
- Increments the counter when the button is pressed.
- Uses a mutex to safely update the shared counter.
- Waits for the button to be released before detecting another press.

**Task 2: PrintTask**
- Reads the button press count.
- Uses the same mutex to safely access the counter.
- Checks whether the counter value has changed.
- Sends the updated count through USART2.
- Repeats the process every 50 ms.

## 6. FreeRTOS Concepts Used

**1. Task Management**

FreeRTOS allows multiple tasks to execute independently under the control of the RTOS scheduler.

**2. Mutex**

A mutex protects the shared `pressCount` variable so that only one task accesses it at a time.

**3. Task Delay**

`osDelay()` is used to introduce delays without continuously occupying the CPU.

**4. Task Priority**

- ButtonTask: Normal Priority
- PrintTask: Below Normal Priority
- DefaultTask: Normal Priority

## 7. Pin Configuration

| Component | STM32 Pin |
|---|---|
| Push Button | PC13 |
| USART2 TX | PA2 (default mapping on supported STM32 devices) |
| USART2 RX | PA3 (default mapping on supported STM32 devices) |

**UART Settings:**
- Baud Rate: 115200
- Data Bits: 8
- Stop Bits: 1
- Parity: None

The push button must provide a valid HIGH signal when pressed and a LOW signal when released, as expected by the code.

## 8. Implementation Steps

**Step 1:** Create a new STM32 project in STM32CubeIDE.

**Step 2:** Configure PC13 as a GPIO input.

**Step 3:** Enable USART2 with a baud rate of 115200.

**Step 4:** Enable FreeRTOS using the CMSIS-RTOS2 interface.

**Step 5:** Create two tasks: `ButtonTask` and `PrintTask`.

**Step 6:** Create a mutex to protect the shared counter variable.

**Step 7:** Write the button detection and UART printing logic.

**Step 8:** Build the project and flash the program to the STM32 board.

**Step 9:** Open a serial terminal and select the correct UART port.

**Step 10:** Press the button and observe the updated counter value.

## 9. Expected Output

```text
Button press count: 1
Button press count: 2
Button press count: 3
Button press count: 4
Button press count: 5
```

The count increases by one for each valid button press.

## 10. Applications
- Embedded systems multitasking demonstration
- Digital event counting
- FreeRTOS task synchronization
- GPIO input monitoring
- UART-based debugging

## 11. Conclusion

This project demonstrates the implementation of multitasking using FreeRTOS on an STM32 microcontroller. It uses two tasks to count button presses and display the result through UART. Mutex synchronization ensures safe access to the shared counter variable.
