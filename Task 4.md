                                                                 RISC PROCESSOR WITH UART INTERFACING


Overview:

A simple RISC processor with a UART interface is ideal for embedded systems and educational projects.
The RISC architecture, known for its reduced instruction set, offers simplicity and efficiency, making it suitable for low-power and high-performance applications.
The UART interface facilitates serial communication, enabling data exchange between the processor and other devices, such as sensors or computers.
The key components used are RISC Processor Core: Includes ALU, registers, instruction fetch and decode units, and memory interface and UART Interface: Comprises TX and RX lines, baud rate generator, and buffers for serial communication.
Mainly used in applications like,
Embedded Systems: Microcontrollers and IoT devices for home automation, sensors, and robotics.
Education: Learning platforms and prototyping.
Industrial: Real-time control systems and data acquisition.


Components:

1. VSDSquadron Mini Board:
   - Based on the RISC-V architecture.
   - Features multiple I/O options, including digital I/O pins, analog inputs, PWM outputs, and communication interfaces like USART, I2C, and SPI.
   - Includes an onboard programmer/debugger and supports open-source tools.

2. UART Interface:
   - TX (Transmit) Line: Sends serial data.
   - RX (Receive) Line: Receives serial data.
   - Baud Rate Generator: Controls the timing for data transmission and reception.
   - Buffers: Temporary storage for data being transmitted and received.

3. Peripheral Interfaces:
   - GPIO (General Purpose Input/Output): For connecting LEDs, buttons, and other peripherals.
   - LEDs and Buttons: For user interaction and status indication.

Circuit Connections:

![WhatsApp Image 2024-06-04 at 12 39 27 PM (1)](https://github.com/nandhini-palanimuthu/VSDSquadron-Mini-Internship/assets/170846569/b8d6502b-dae4-4041-ad94-080c8030a370)



Pin Connections:

#### Power Supply

VSDSquadron Mini
----------------
VCC  --> VCC (3.3V or 5V)
GND  --> GND


#### UART Connections

VSDSquadron Mini         UART-to-USB Converter
----------------         ---------------------
PD5 (TX)   ---------->   RX (Receive)
PD6 (RX)  <----------    TX (Transmit)


#### LED Connections

VSDSquadron Mini
----------------
PD0  --> 220Ω Resistor --> Anode of LED1
                       --> Cathode of LED1 --> GND
PD1  --> 220Ω Resistor --> Anode of LED2
                       --> Cathode of LED2 --> GND
PD2  --> 220Ω Resistor --> Anode of LED3
                       --> Cathode of LED3 --> GND
PD3  --> 220Ω Resistor --> Anode of LED4
                       --> Cathode of LED4 --> GND


#### Button Connections

VSDSquadron Mini
----------------
PD4  --> One terminal of Button1
      --> 10kΩ Resistor --> GND
Other terminal of Button1 --> GND

PD7  --> One terminal of Button2
      --> 10kΩ Resistor --> GND
Other terminal of Button2 --> GND


Circuit Explanation:

1. **Power Supply:**
     VCC and GND: These pins provide power to the processor. The VCC pin should be connected to a 3.3V or 5V power supply, and the GND pin to ground.

2. **UART Interface:**
    PD5 (TX): This pin is used to transmit data. It should be connected to the RX (Receive) pin of a UART-to-USB converter.
    PD6 (RX): This pin is used to receive data. It should be connected to the TX (Transmit) pin of a UART-to-USB converter.

3. **LED Connections:**
    PD0 - PD3: Each of these GPIO pins is connected to an LED through a 220Ω resistor to limit current. The anode of each LED connects to the resistor, and the cathode connects to ground.

4. **Button Connections:**
    PD4 and PD7: Each GPIO pin is connected to one terminal of a button. A 10kΩ pull-down resistor is used to connect the same terminal to ground, ensuring the pin reads LOW when the button is not pressed. The other terminal of each button is connected to ground.

Specific Functions:

*Instruction Execution:The RISC processor fetches, decodes, and executes instructions, using its ALU for computations and registers for temporary storage.
*UART Communication:The UART interface handles serial data transmission and reception, allowing the processor to communicate with external devices.
*LED Control:The processor can turn LEDs on or off by setting the corresponding GPIO pins HIGH or LOW.
*Button Input: The processor reads the state of the buttons via GPIO pins, which can be used to trigger specific actions.

