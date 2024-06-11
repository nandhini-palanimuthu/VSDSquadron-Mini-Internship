                                                        PUSH BUTTON PRESS - LED PATTERNS USING VSD SQUADRON MINI RISC-V


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
