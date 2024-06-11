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
