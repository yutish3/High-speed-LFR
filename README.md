# LFR - 2026
STM32 line follower robot on a custom 2-layer PCB. Black Pill (STM32F411) as a brain, TB6612FNG motor driver, 16-channel ARC16 line sensor, MPU6050 , and 3S LiPo through a 5V buck converter.

<img width="1142" height="1000" alt="image" src="https://github.com/user-attachments/assets/0dc4e321-502a-4621-adf9-07c3b2b369ba" />

## VISION
I wanted to make a LFR that will be really good for competitions and i didt wanted it to fail mid run or during travel so i decided to make a pcb for it

<img width="884" height="940" alt="image" src="https://github.com/user-attachments/assets/f7ee4824-9c05-484e-a60a-2d60cec8b8c5" />

Main goals:
- everything on a single PCB: power, motor driver, sensor connector, IMU
- run straight from a 3S LiPo with a power switch
- battery voltage monitoring so the robot knows when the pack is getting low (used 2 resistors for it connected to blackpill)
- status LEDs, a RESET button and a SAVE button for calibration
- test points for power pins

## what makes it special (main components)

&#9679; STM32F411CEU6 (Black Pill) :- main microcontroller, 100 MHz Cortex-M4 with hardware FPU

&#9679; TB6612FNG :- dual H-bridge motor driver for two N20 gear motors

&#9679; ARC16 :- 16-channel IR line sensor array on a single 8-pin header

&#9679; MPU6050 :- 6-axis IMU for gyro-assisted turning and stabilisation

&#9679; 3S LiPo + buck converter :- 11.1V battery, with the 5V rail for the sensor and the MCU

&#9679; N20 600 RPM motors :- small, light and fast for the size

## Images

<img src="images/schematic.png" alt="Schematic" width="600">

<img src="images/pcb-layout.png" alt="PCB Layout" width="600">

<img src="images/pcb-3d.png" alt="3D View" width="600">

<img src="images/robot.png" alt="Assembled Robot" width="600">

## How it works

**Power**

```
3S LiPo -> XT60 (J1) -> rocker switch (Jw2) -> VSW
VSW -> buck converter -> +5V  (Black Pill 5V pin, ARC16 sensor)
VSW -> TB6612FNG VM           (motor supply)
VSW -> 33k / 10k divider      (battery voltage sense on PA2)
Black Pill 3V3 -> MPU6050, TB6612FNG logic
```

- Bulk capacitors: 2 x 100 uF on VSW and 2 x 220 uF on +5V.
- The sensor's analog output is divided down (10k / 15k) so the 5V signal is safe for the 3.3V ADC.
- Test points: TP1 (+3V3), TP2 (+5V), TP3 (VSW) and TP4 (GND).

**Pin mapping (as drawn in the schematic)**

| MCU pin | Connected to | Function |
| --- | --- | --- |
| PB3 | TB6612FNG PWMA | Left motor speed (PWM) |
| PB4 | TB6612FNG AIN2 | Left motor direction |
| PA15 | TB6612FNG AIN1 | Left motor direction |
| PA8 | TB6612FNG PWMB | Right motor speed (PWM) |
| PA10 | TB6612FNG BIN1 | Right motor direction |
| PA9 | TB6612FNG BIN2 | Right motor direction |
| PA1 | ARC16 analog output (via divider) | Sensor reading |
| PA4 - PA7 | ARC16 header pins 5 to 2 | Sensor channel lines |
| PA2 | VSW divider (33k / 10k) | Battery voltage |
| PA3 | SAVE button | Calibration / save |
| NRST | RESET button | Reset |
| PB8 | MPU6050 SCL | I2C1 clock |
| PB7 | MPU6050 SDA | I2C1 data |
| PB5 | Red LED | Status |
| PB10 | Green LED | Status |

TB6612FNG STBY is tied to 3V3, so the driver is always enabled.

## Bill of Materials

| Component | Purpose | Qty | Cost (INR) | Distributor |
| --- | --- | --- | --- | --- |
| N20 12V 600 RPM Micro Metal Gear Motor | Drive motors (the PCB has two motor outputs, J4 and J5) | 4 | ₹916 | Online |
| Pro-Range 11.1V 850mAh 30C 3S LiPo Battery Pack | Main power | 1 | ₹1,159 | Online |
| ARC16 Line Sensor | 16-channel IR line sensor array (J7) | 1 | ₹1,499 | Online (order 9 Oct 2026) |
| N20 Wheels (pack of 2) | Drive wheels | 1 | ₹349 | Online (order 9 Oct 2026) |
| Mini 3Pi N20 Caster Ball Wheel | Third support point | 1 | ₹39 | Online |
| Tactile Push Button 6x6x5 (pack of 10) | RESET and SAVE buttons (SW2, SW3) | 1 | ₹19 | Online |
| 100 uF 35V Electrolytic Capacitor | VSW bulk decoupling (C1, C3) | 2 | ₹24 | Online |
| 220 uF 25V Electrolytic Capacitor | +5V bulk decoupling (C2, C4) | 4 | ₹28 | Online |
| XT60 Female to Nylon T-Connector Adapter (14AWG, 15 cm) | Battery plug adapter | 1 | ₹131 | Online |
| Amass XT60PW Male Connector | Battery connector on the PCB (J1) | 1 | ₹70 | Online |
| SPST Rocker Switch | Main power switch (Jw2) | 1 | ₹12 | Online |
| 2mm Pitch Male Berg Strip 40x1 | Pin headers | 1 | ₹13 | Online |
| M3 x 10mm Bolt and Nut Set (25 pcs) | Mounting hardware | 1 | ₹78 | Online |
| M3 x 6mm Bolt and Nut Set (25 pcs) | Mounting hardware | 1 | ₹67 | Online |
| M3 x 10mm Male to Female Nylon Hex Spacer (10 pcs) | Standoffs | 1 | ₹82 | Online |
| Shipping / fees (sensor and wheels order) | Order total ₹1,948 vs items ₹1,848 | 1 | ₹100 | Online |
| Custom 2-layer PCB (KiCad) | Main board | 1 | - | Bought separately |
| WeAct Black Pill (STM32F411CEU6) | Main microcontroller (BLACK-PILL1) | 1 | - | Bought offline |
| TB6612FNG Motor Driver Module | Dual motor driver (U2) | 1 | - | Bought offline |
| MPU6050 (GY-521) Module | 6-axis IMU (J9) | 1 | - | Bought offline |
| 5V Buck Converter Module | Battery to 5V (BUCK1) | 1 | - | Bought offline |
| Resistors (through-hole): 330 ohm x2, 10k x2, 15k x1, 33k x1 | LED current limiting, voltage dividers (R1 to R6) | 6 | - | Bought offline |
| LEDs: 1 green, 1 red | Status indicators (D1, D2) | 2 | - | Bought offline |
| Female Header Sockets | Sockets for Black Pill, TB6612FNG and MPU6050 | 1 set | - | Bought offline |

Items marked "Bought offline" came from a local shop. Their cost is not included in the totals below.

| Summary | Cost (INR) |
| --- | --- |
| Parts order (motors, battery, connectors, hardware) | ₹2,638 |
| Sensor + wheels order (9 Oct 2026, incl. ₹100 shipping / fees) | ₹1,948 |
| **Online total** | **₹4,586** |
