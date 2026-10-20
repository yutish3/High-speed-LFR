<img width="1486" height="1036" alt="image" src="https://github.com/user-attachments/assets/f9ed6cef-e9ad-4e17-9222-77a8fc26aafd" /># LFR - 2026
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

<img width="936" height="1012" alt="image" src="https://github.com/user-attachments/assets/75298efc-8484-46b7-b83a-0c427e0bad20" />

<img width="1068" height="1028" alt="image" src="https://github.com/user-attachments/assets/80695ac8-cf52-49e4-b055-22052f6cf045" />

<img width="1486" height="1036" alt="image" src="https://github.com/user-attachments/assets/db2adbfd-8701-4c09-8dc8-a9e912f989f5" />

## Bill of Materials

| Component | Purpose | Qty | Cost (INR) | Distributor |
| --- | --- | --- | --- | --- |
| N20 12V 600 RPM motor | main motor | 4 | ₹916 | Online |
| 11.1V 850mAh 30C 3S LiPo Battery Pack | Main power | 1 | ₹1,159 | Online |
| ARC16 Line Sensor | 16-channel IR line sensor array | 1 | ₹1,499 | Online |
| N20 Wheels | wheels | 1 | ₹349 | Online |
| N20 Caster Ball Wheel | Third support point | 1 | ₹39 | Online |
| Push Button 6x6x5 (pack of 10) | RESET and SAVE buttons | 1 | ₹19 | Online |
| 100 uF 35V cap | VSW bulk decoupling | 2 | ₹24 | Online |
| 220 uF 25V cap | +5V bulk decoupling | 4 | ₹28 | Online |
| XT60 Female to Nylon T-Connector | Battery plug adapter | 1 | ₹131 | Online |
| XT60PW Male Connector | Battery connector | 1 | ₹70 | Online |
| Rocker Switch | Main power switch | 1 | ₹12 | Online |
| Custom 2-layer PCB (KiCad) | Main board | 1 | - | Bought separately |
| Black Pill (STM32F411CEU6) | Main microcontroller | 1 | - | Bought offline |
| TB6612FNG Motor Driver | Dual motor driver | 1 | - | Bought offline |
| MPU6050 Module | 6-axis IMU | 1 | - | Bought offline |
| 5V Buck Converter Module | Battery to 5V (BUCK1) | 1 | - | Bought offline |
| Custom PCB | PCB | 1 | 1500 | whypcb |

