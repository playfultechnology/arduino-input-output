# arduino-input-output
Libaries, wiring, and example code for various inputs / outputs for Arduino and other microprocessors

When you need more inputs/outputs for your Arduino project, the response in some forums is "Use a MEGA" instead.
While the Arduino MEGA does have more built-in GPIO pins (70 digital input/output pins, of which 14 can be used as PWM outputs and 16 can be used as analog inputs), it's pretty old tech now, and if the only reason for choosing it is because you need more inputs/outputs, there are plenty of other options available rather than be forced to change to a particular microprocessor board.

## Multiplexers
Multiplexers are multi-way electronic switches, with multiple selectable inputs leading to a single output (a "demultiplexer" has a single input that can be connected to one of multiple outputs, although in practice the term "multiplexer" typically describes both). The selected channel is chosen by setting the state of a set of control lines. A multiplexer with _n_ control lines can select between _2<sup>n</sup>_ channels.

Common components:
74HC4051 - 8 channel (3 control lines)
74HC4067 - 16 channels (4 control lines)

+ Multiplexers are faster than shift registers
+ They can carry analog or digital signals, as input or output
- You can only send/receive data to one component at a time
- It requires more pins than other solutions

## Shift Registers

Shift registers come in two basic types, either SIPO, Serial-In-Parallel-Out, or PISO, Parallel-In-Serial-Out. SIPO is useful for controlling a large number of outputs, including LEDs, while the latter type, PISO, is good for gathering a large number of inputs, like buttons.

+ Daisy-chained infinitely to create a limitless number of outputs/inputs
+ Only ever requires 3 control pins
- Can only operate as input _or_ output
- A little slower than other methods
- Only digital (1 bit per sensor)

SIPO Shift Registers - 74HC595
PISO Shift Registers - 74HC165, CD4021


## GPIO Expanders
MCP23017 (16 GPIOs from I2C interface, with 3 address pins, you can have up to 8 on a single bus for a total of 8 x 16 = 128 GPIO)
PCF8574 (8 GPIOs from I2C interface, with 3 address pins, you can have up to 8 on a single bus for a total of 8 x 8 = 64 GPIO)


# I2C Multiplexers
TCA9548A



| Image | Chipset  | Type | Resolution  | Interface | Code  | Purchase |
| -------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| ![](Images/TM1637.jpg) | TM1637 | 7-segment | 4-digit | <a href="https://green-possum-today.blogspot.com/2018/10/a-comparison-of-tm1637-protocol-with.html">Custom Serial (I2C variant)</a> | https://github.com/RobTillaart/TM1637_RT | https://www.banggood.com/custlink/GDD3zSq2qk |
