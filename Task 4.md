                                                        PUSH BUTTON - LED PATTERNS USING VSD SQUADRON MINI RISC-V


Overview:

The "Push Button LED Patterns" project uses a VSD Squadron Mini board to control three LEDs based on push button inputs, creating different lighting patterns with each press. The system increments a counter with each button press, cycling through various predefined LED sequences connected to pins PD0, PD1, and PD2. Starting with all LEDs off, the patterns range from simple blinking to more complex sequences, providing visual feedback. Once the counter reaches a certain number (e.g., 5), it resets, starting the cycle anew. This project serves as an  introduction to microcontroller programming, digital input reading, and output control, offering hands-on experience in electronics and coding.


Components:

1. VSDSquadron Mini Board:
   - Based on the RISC-V architecture.
   - Features multiple I/O options, including digital I/O pins, analog inputs, PWM outputs, and communication interfaces like USART, I2C, and SPI.
   - Includes an onboard programmer/debugger and supports open-source tools.

2. Push Button:
   - A momentary push button is connected to the board to act as the input device.
   - It's used to increment the LED patterns.
     
3. LEDs (Light Emitting Diodes):
   - Three LEDs are connected to the board to visually represent different patterns.
   - They serve as the output indicators.
     
     
Circuit Connections & Explanation:

1. Push Button:

Pin Connection: One terminal of the push button is connected to a digital input pin on the VSD Squadron Mini board (e.g., pin 8).

2. Pull-up Resistor: Internal or external pull-up resistor is enabled for the input pin to ensure proper signal detection. (PlatformIO's INPUT_PULLUP mode can be used for this purpose.)

3. LEDs:
   
Pin Connections: Each LED is connected to a separate digital output pin on the VSD Squadron Mini board.
 LED 1: Connected to pin PD1 ;
 LED 2: Connected to pin PD2 ;
 LED 3: Connected to pin PD3 . 

Working Pattern:

- 1st pressed button: change into LED pattern 1: Walking LEDs.
- 2nd pressed button: change into LED pattern 2: Red 100ms - Yellow 100ms - Green 1 second.
- 3th pressed button: change into LED pattern 3: Traffic LEDs.
- 4th pressed button: change into LED pattern 4: Green 1 second - yellow 100ms - red 100ms.
- 5th pressed button: change into LED pattern 5: three times each LEDs blink in an order.
- 6th pressed button gives random blink of random selected LEDs in random duration and delay.


Circuit Connections:


![WhatsApp Image 2024-06-11 at 3 49 40 PM](https://github.com/nandhini-palanimuthu/VSDSquadron-Mini-Internship/assets/170846569/03b95721-d581-468d-947a-982df435a788)


Pin Connections:

     VSD Squadron Mini Board
     ----------------------
    |                      |
    |                      |
    | PA12  --------> LED1 |----->|----> (R) ---> GND
    |                      |
    | PA11  --------> LED2 |----->|----> (R) ---> GND
    |                      |
    | PA10  --------> LED3 |----->|----> (R) ---> GND
    |                      |
    | PA0   --------> Push


Code:


#include "ch32v30x.h"
#include <stdio.h>

#define LED_1_PIN GPIO_Pin_12
#define LED_2_PIN GPIO_Pin_11
#define LED_3_PIN GPIO_Pin_10
#define BUTTON_PIN GPIO_Pin_8

#define LED_PORT GPIOA
#define BUTTON_PORT GPIOA

volatile int count = 0;

void delay(uint32_t count) {
    for (uint32_t i = 0; i < count; i++);
}

void setup() {
    // Enable clock for GPIOA
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOA, ENABLE);

    // Configure LED pins as output push-pull
    GPIO_InitTypeDef GPIO_InitStructure;
    GPIO_InitStructure.GPIO_Pin = LED_1_PIN | LED_2_PIN | LED_3_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(LED_PORT, &GPIO_InitStructure);

    // Configure BUTTON pin as input pull-up
    GPIO_InitStructure.GPIO_Pin = BUTTON_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIO_Init(BUTTON_PORT, &GPIO_InitStructure);

    // Initialize UART for serial communication
    USART_InitTypeDef USART_InitStructure;
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_USART1, ENABLE);
    USART_InitStructure.USART_BaudRate = 9600;
    USART_InitStructure.USART_WordLength = USART_WordLength_8b;
    USART_InitStructure.USART_StopBits = USART_StopBits_1;
    USART_InitStructure.USART_Parity = USART_Parity_No;
    USART_InitStructure.USART_HardwareFlowControl = USART_HardwareFlowControl_None;
    USART_InitStructure.USART_Mode = USART_Mode_Rx | USART_Mode_Tx;
    USART_Init(USART1, &USART_InitStructure);
    USART_Cmd(USART1, ENABLE);
}

void USART_SendString(char* str) {
    while (*str) {
        while (USART_GetFlagStatus(USART1, USART_FLAG_TXE) == RESET);
        USART_SendData(USART1, *str++);
    }
}

void loop() {
    GPIO_ResetBits(LED_PORT, LED_1_PIN | LED_2_PIN | LED_3_PIN);

    if (GPIO_ReadInputDataBit(BUTTON_PORT, BUTTON_PIN) == Bit_RESET) {
        delay(300000); // Debounce delay
        if (GPIO_ReadInputDataBit(BUTTON_PORT, BUTTON_PIN) == Bit_RESET) {
            count++;
            delay(1000000); // Delay to avoid multiple increments
            char buffer[10];
            sprintf(buffer, "%d\n", count);
            USART_SendString(buffer);
        }
    }

    switch (count) {
        case 0:
            GPIO_SetBits(LED_PORT, LED_1_PIN);
            delay(2000000);
            GPIO_ResetBits(LED_PORT, LED_1_PIN);
            GPIO_SetBits(LED_PORT, LED_2_PIN);
            delay(2000000);
            GPIO_ResetBits(LED_PORT, LED_2_PIN);
            GPIO_SetBits(LED_PORT, LED_3_PIN);
            delay(2000000);
            GPIO_ResetBits(LED_PORT, LED_3_PIN);
            GPIO_SetBits(LED_PORT, LED_2_PIN);
            delay(2000000);
            GPIO_ResetBits(LED_PORT, LED_2_PIN);
            break;

        case 1:
            GPIO_SetBits(LED_PORT, LED_1_PIN);
            delay(1000000);
            GPIO_ResetBits(LED_PORT, LED_1_PIN);
            GPIO_SetBits(LED_PORT, LED_2_PIN);
            delay(1000000);
            GPIO_ResetBits(LED_PORT, LED_2_PIN);
            GPIO_SetBits(LED_PORT, LED_3_PIN);
            delay(1000000);
            GPIO_ResetBits(LED_PORT, LED_3_PIN);
            break;

        case 2:
            GPIO_SetBits(LED_PORT, LED_1_PIN);
            delay(10000000);
            GPIO_ResetBits(LED_PORT, LED_1_PIN);
            GPIO_SetBits(LED_PORT, LED_2_PIN);
            delay(3000000);
            GPIO_ResetBits(LED_PORT, LED_2_PIN);
            GPIO_SetBits(LED_PORT, LED_3_PIN);
            delay(10000000);
            GPIO_ResetBits(LED_PORT, LED_3_PIN);
            break;

        case 3:
            GPIO_ResetBits(LED_PORT, LED_1_PIN);
            GPIO_ResetBits(LED_PORT, LED_2_PIN);
            GPIO_SetBits(LED_PORT, LED_3_PIN);
            delay(1000000);
            GPIO_ResetBits(LED_PORT, LED_3_PIN);
            GPIO_SetBits(LED_PORT, LED_2_PIN);
            delay(100000);
            GPIO_ResetBits(LED_PORT, LED_2_PIN);
            GPIO_SetBits(LED_PORT, LED_1_PIN);
            delay(100000);
            GPIO_ResetBits(LED_PORT, LED_1_PIN);
            break;

        case 4:
            for (int i = 0; i < 3; i++) {
                GPIO_SetBits(LED_PORT, LED_1_PIN);
                delay(250000);
                GPIO_ResetBits(LED_PORT, LED_1_PIN);
                delay(250000);
                GPIO_SetBits(LED_PORT, LED_2_PIN);
                delay(250000);
                GPIO_ResetBits(LED_PORT, LED_2_PIN);
                delay(250000);
                GPIO_SetBits(LED_PORT, LED_3_PIN);
                delay(250000);
                GPIO_ResetBits(LED_PORT, LED_3_PIN);
                delay(250000);
            }
            break;

        case 5:
            GPIO_SetBits(LED_PORT, GPIO_Pin_10 + (rand() % 3));
            delay(250000);
            GPIO_ResetBits(LED_PORT, GPIO_Pin_10 + (rand() % 3));
            delay(250000);
            break;

        case 6:
            count = 0;
            break;
    }
}

int main(void) {
    setup();
    while (1) {
        loop();
    }
}



