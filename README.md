# arduino-input-output
Libaries, wiring, and example code for various inputs / outputs for Arduino and other microprocessors

When you need more inputs/outputs for your Arduino project, the response in some forums is "Use a MEGA" instead.
While the Arduino MEGA does have more built-in GPIO pins (70 digital input/output pins, of which 14 can be used as PWM outputs and 16 can be used as analog inputs), it's pretty old tech now, and if the only reason for choosing it is because you need more inputs/outputs, there are plenty of other options available rather than be forced to change to a particular microprocessor board.

## Multiplexers
Multiplexers are multi-way electronic switches, with multiple selectable inputs leading to a single output (a "demultiplexer" has a single input that can be connected to one of multiple outputs, although in practice the term "multiplexer" typically describes both). The selected channel is chosen by setting the state of a set of control lines. A multiplexer with _n_ control lines can select between _2<sup>n</sup>_ channels.

Common components:
 - **74HC4051** - 8 channel (3 control lines)
 - **74HC4067** - 16 channels (4 control lines)

Pros:
+ Multiplexers are faster than shift registers
+ They can carry analog or digital signals, as input or output
Cons:
- You can only send/receive data to one component at a time
- It requires more pins than other solutions

```Multiplexers are a good choice when you want to send or receive many analog signals.```

## Shift Registers
Shift registers come in two common basic types:
 - Serial-In-Parallel-Out (SIPO), e.g. **74HC595** used for controlling a large number of outputs (e.g. LEDs).
 - Parallel-In-Serial-Out (PISO), e.g.  **74HC165** or **CD4021** used for gathering a large number of inputs (e.g. buttons).

Pros:
+ Daisy-chained infinitely to create a limitless number of outputs/inputs (although would take more time to clock data in/out)
+ Only ever requires 3 control pins
Cons:
- A given shift register can only operate as input _or_ output
- A little slower than other methods
- Only digital (1 bit per sensor)

```Shift registers are a good choice when you want a simple, cheap way to interface with _many_ (i.e  hundreds of) "dumb" inputs (buttons) or outputs (LEDs) that don't require complex protocols, timings etc.```

As an example implementation, this is what the Kincony <a href="https://www.kincony.com/download/KC868-A256-schematic.pdf">KC868-A256</a> board uses:
 - 256 outputs via 32xchained 74HC595 registers (GPIO5=Data, GPIO16=Clock, GPIO4=Latch) sent to ULN2803 transistor array.
 - 256 inputs via 32xchained 74HC165 registers (GPIO15=Data, GPIO32=Clock, GPIO33=Load) received via PS2801 optocoupler array.


## GPIO Expanders
GPIO expanders provide additional input/output pins that behave almost exactly the same way as built-in GPIO pins - with interrupt capability, built-in pull-up resistors, can accommodate a range of input voltages etc.
 - **MCP23017** (16 GPIOs from I2C interface, with 3 address pins, you can have up to 8 on a single bus for a total of 8 x 16 = 128 GPIO)
 - **MCP23S17** (as above, but using SPI interface. Somewhat faster, but requires more pins)
 - **PCF8574** (8 GPIOs from I2C interface, with 3 address pins, you can have up to 8 on a single bus for a total of 8 x 8 = 64 GPIO)
 - **PCF8575** (16 GPIOs from I2C interface, with 3 address pins, you can have up to 8 on a single bus for a total of 8 x 16 = 128 GPIO)

Pros:
+ Each channel can be digital input/output, just like a regular GPIO pin complete with pull-up resistors, interrupts etc.
+ Uses I2C interface which requires only 2 pins, or 3 pin SPI interface
Cons:
- Only works with digital inputs/outputs

```GPIO expanders are a good choice when you want to add more general purpose digital pins, that behave almost exactly the same as the built-in GPIO pins.```

As an example implementation, this is what the Kincony <a href="https://www.kincony.com/download/KC868-A64-schematic.pdf">KC868-A64</a> board uses:
 - 64 outputs via 4x PCF8575 expanders on I2C bus A(GPIO5=SDA, GPIO16=SCL).
 - 64 inputs via 4x PCF8575 expanders on I2C bus B(GPIO15=SDA, GPIO4=SCL).

The <a href="https://www.kincony.com/download/KC868-A128-schematic.pdf">KC868-A128</a> board uses exactly the same approach but uses twice as many expanders for both inputs and outputs:
 - 128 outputs via 8x PCF8575 expanders on I2C bus A(GPIO5=SDA, GPIO16=SCL).
 - 128 inputs via 8x PCF8575 expanders on I2C bus B(GPIO15=SDA, GPIO4=SCL).

## I2C Multiplexers
TCA9548A

```I2C multiplexers are a good choice when you want to add several devices to the same I2C bus that all use the same address.```


| Image | Chipset  | Type | Resolution  | Interface | Code  | Purchase |
| -------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| ![](Images/TM1637.jpg) | TM1637 | 7-segment | 4-digit | <a href="https://green-possum-today.blogspot.com/2018/10/a-comparison-of-tm1637-protocol-with.html">Custom Serial (I2C variant)</a> | https://github.com/RobTillaart/TM1637_RT | https://www.banggood.com/custlink/GDD3zSq2qk |
