# BrightEyes-MCSLL
The BrightEyes Microscope Control Software Low-Level is a collections of firmwares for NI FPGA in order to be used with BrightEyes-MCS.
Documentation and usage you can find in [BrightEyes-MCS repository](https://github.com/VicidominiLab/BrightEyes-MCS).

**Copyright** (C) 2023 Istituto Italiano di Tecnologia

**Author:** Mattia Donato

**Credits to:** Marco Castello, Giorgio Tortarolo, Simonluca Piazza, Eli Slenders

**Closed-Source Firmware License Agreement:** This license grants you a non-exclusive, non-transferable permission to download and utilize our proprietary firmware free of charge. However, you are required to use this firmware exclusively in conjunction with open-source software, such as [BrightEyes-MCS](https://github.com/VicidominiLab/BrightEyes-MCS). Modifying, distributing, or employing it with closed-source software is strictly prohibited. We actively endorse and support the use of this firmware in educational institutions, including schools, universities, as well as in both public and private research organizations. All rights to the firmware are retained by us. The firmware is provided "as is" with absolutely no warranty. We disclaim all liability for any damages. This license may be terminated at your discretion or by us. Your use of the firmware signifies your agreement to this Agreement.

If you have bugs to report or you have requests for adding or modifying firmware functionalities, please feel free to contact us. We are open to collaborations!





# BrightEyes-MCS-LowLevel Firmwares

## I/O Tables

Important: The DIO number does not correspond to the breakout-board pin number. Always check the pin-mapping table before making any connection.

- [NI PCIe-7820R](#ni-pcie-7820r)
- [NI PXIe-7820R](#ni-pxie-7820r)
- [NI USB-7856R](#ni-usb-7856r)
- [NI PXIe-7856R](#ni-pxie-7856r)
- [GI-BOX (PRISM)](#gi-box-prism)
- [GI-DAC](#gi-dac)



### NI PCIe-7820R

| NI Connector | DIO    | Firmware Naming        | GI-BOX              |
| ------------ | ------ | ---------------------- | ------------------- |
| 0            | 0      | SPAD0                  | SPAD Conn.          |
| 0            | \.\.\. |                        |                     |
| 0            | 24     | SPAD24                 | SPAD Conn.          |
| 0            | 25     | SPAD\_ENABLE           | SPAD Conn. (ENABLE) |
| 0            | 26     | SPAD\_VR0              | SPAD Conn. (VR0)    |
| 0            | 27     | SPAD\_VR1              | SPAD Conn. (VR1)    |
| 0            | 28     | LASER\_0               | AUX0                |
| 0            | 29     | LASER\_1               | AUX1                |
| 0            | 30     | LASER\_2               | AUX2                |
| 0            | 31     | LASER\_3               | AUX3                |
|              |        |                        |                     |
| 1            | 0      | SPAD25                 | SPAD Conn.          |
| 1            | \.\.\. |                        |                     |
| 1            | 23     | SPAD48                 | SPAD Conn.          |
| 1            | 24     | SPAD\_SDATA            | SPAD Conn. (SDA)    |
| 1            | 25     | SPAD\_SCLK             | SPAD Conn. (SCL)    |
| 1            | 26     | DET\_EXTRA\_0          | AUX4                |
| 1            | 27     | DET\_EXTRA\_1          | AUX5                |
| 1            | 28     |                        | AUX6                |
| 1            | 29     | PIXEL\_SYNC            | AUX7                |
| 1            | 30     | LINE\_SYNC             | AUX8                |
| 1            | 31     | FRAME\_SYNC            | AUX9                |
|              |        |                        |                     |
| 2            | 8      | AO\_TRIGGER\_TEST      |                     |
| 2            | 26     | AD5764\_SDATA          |                     |
| 2            | 27     | AD5764\_SCLK           |                     |
| 2            | 28     | AD5764\_SSYNC          |                     |
|              |        |                        |                     |
| 3            | 0      | GI\_DAC\_SCLK0         |                     |
| 3            | 1      | GI\_DAC\_SDIN0         |                     |
| 3            | 2      | GI\_DAC\_SSYNC0        |                     |
| 3            | 3      | GI\_DAC\_SCLK1         |                     |
| 3            | 4      | GI\_DAC\_SDIN1         |                     |
| 3            | 5      | GI\_DAC\_SSYNC1        |                     |
| 3            | 6      | GI\_DAC\_SCLK2         |                     |
| 3            | 7      | GI\_DAC\_SDIN2         |                     |
| 3            | 8      | GI\_DAC\_SSYNC2        |                     |
| 3            | 9      | GI\_DAC\_SCLK3         |                     |
| 3            | 10     | GI\_DAC\_SDIN3         |                     |
| 3            | 11     | GI\_DAC\_SSYNC3        |                     |
| 3            | 12     | GI\_DAC\_SCLK4         |                     |
| 3            | 13     | GI\_DAC\_SDIN4         |                     |
| 3            | 14     | GI\_DAC\_SSYNC4        |                     |
| 3            | 15     | GI\_DAC\_GI\_DIO0\_OUT |                     |
| 3            | 16     | GI\_DAC\_GI\_DIO1\_OUT |                     |
| 3            | 17     | GI\_DAC\_GI\_DIO2\_OUT |                     |
| 3            | 18     | GI\_DAC\_GI\_DIO3\_OUT |                     |
| 3            | 19     | GI\_DAC\_GI\_DIO4\_OUT |                     |
| 3            | 20     | GI\_DAC\_SCLK5         |                     |
| 3            | 21     | GI\_DAC\_DOUT5         |                     |
| 3            | 22     | GI\_DAC\_CONVST5       |                     |
| 3            | 23     | GI\_DAC\_SCLK6         |                     |
| 3            | 24     | GI\_DAC\_DOUT6         |                     |
| 3            | 25     | GI\_DAC\_CONVST6       |                     |
| 3            | 26     | GI\_DAC\_DIO5\_IN      |                     |
| 3            | 27     | GI\_DAC\_DIO6\_IN      |                     |


### NI PXIe-7820R


| NI Connector | DIO    | Firmware Naming        | GI-BOX              |
| ------------ | ------ | ---------------------- | ------------------- |
| 0            | 0      | SPAD0                  | SPAD Conn.          |
| 0            | \.\.\. |                        |                     |
| 0            | 24     | SPAD24                 | SPAD Conn.          |
| 0            | 25     | SPAD\_ENABLE           | SPAD Conn. (ENABLE) |
| 0            | 26     | SPAD\_VR0              | SPAD Conn. (VR0)    |
| 0            | 27     | SPAD\_VR1              | SPAD Conn. (VR1)    |
| 0            | 28     | LASER\_0               | AUX0                |
| 0            | 29     | LASER\_1               | AUX1                |
| 0            | 30     | LASER\_2               | AUX2                |
| 0            | 31     | LASER\_3               | AUX3                |
|              |        |                        |                     |
| 1            | 0      | SPAD25                 |                     |
| 1            | \.\.\. |                        |                     |
| 1            | 23     | SPAD48                 |                     |
| 1            | 24     | SPAD\_SDATA            | SPAD Conn. (SDA)    |
| 1            | 25     | SPAD\_SCLK             | SPAD Conn. (SCL)    |
| 1            | 26     | DET\_EXTRA\_0          | AUX4                |
| 1            | 27     | DET\_EXTRA\_1          | AUX5                |
| 1            | 28     |                        | AUX6                |
| 1            | 29     | PIXEL\_SYNC            | AUX7                |
| 1            | 30     | LINE\_SYNC             | AUX8                |
| 1            | 31     | FRAME\_SYNC            | AUX9                |
|              |        |                        |                     |
| 2            | 8      | AO\_TRIGGER\_TEST      |                     |
| 2            | 26     | AD5764\_SDATA          |                     |
| 2            | 27     | AD5764\_SCLK           |                     |
| 2            | 28     | AD5764\_SSYNC          |                     |
|              |        |                        |                     |
| 3            | 0      | GI\_DAC\_SCLK0         |                     |
| 3            | 1      | GI\_DAC\_SDIN0         |                     |
| 3            | 2      | GI\_DAC\_SSYNC0        |                     |
| 3            | 3      | GI\_DAC\_SCLK1         |                     |
| 3            | 4      | GI\_DAC\_SDIN1         |                     |
| 3            | 5      | GI\_DAC\_SSYNC1        |                     |
| 3            | 6      | GI\_DAC\_SCLK2         |                     |
| 3            | 7      | GI\_DAC\_SDIN2         |                     |
| 3            | 8      | GI\_DAC\_SSYNC2        |                     |
| 3            | 9      | GI\_DAC\_SCLK3         |                     |
| 3            | 10     | GI\_DAC\_SDIN3         |                     |
| 3            | 11     | GI\_DAC\_SSYNC3        |                     |
| 3            | 12     | GI\_DAC\_SCLK4         |                     |
| 3            | 13     | GI\_DAC\_SDIN4         |                     |
| 3            | 14     | GI\_DAC\_SSYNC4        |                     |
| 3            | 15     | GI\_DAC\_GI\_DIO0\_OUT |                     |
| 3            | 16     | GI\_DAC\_GI\_DIO1\_OUT |                     |
| 3            | 17     | GI\_DAC\_GI\_DIO2\_OUT |                     |
| 3            | 18     | GI\_DAC\_GI\_DIO3\_OUT |                     |
| 3            | 19     | GI\_DAC\_GI\_DIO4\_OUT |                     |
| 3            | 20     | GI\_DAC\_SCLK5         |                     |
| 3            | 21     | GI\_DAC\_DOUT5         |                     |
| 3            | 22     | GI\_DAC\_CONVST5       |                     |
| 3            | 23     | GI\_DAC\_SCLK6         |                     |
| 3            | 24     | GI\_DAC\_DOUT6         |                     |
| 3            | 25     | GI\_DAC\_CONVST6       |                     |
| 3            | 26     | GI\_DAC\_DIO5\_IN      |                     |
| 3            | 27     | GI\_DAC\_DIO6\_IN      |                     |



### NI USB-7856R

| NI Connector          | NI DIO | BRIGHTEYES-MCS USB | GI-BOX              |
| --------------------- | ------ | ------------------ | ------------------- |
| 0 \(DIGITAL\)         | 0      | SPAD0              | SPAD Conn.          |
| 0 \(DIGITAL\)         | …      | \.\.               | \.\.\.              |
| 0 \(DIGITAL\)         | 24     | SPAD24             | SPAD Conn.          |
| 0 \(DIGITAL\)         | 25     | SPAD\_ENABLE       | SPAD Conn. (ENABLE) |
| 0 \(DIGITAL\)         | 26     | SPAD\_SCLK         | SPAD Conn. (VR0)    |
| 0 \(DIGITAL\)         | 27     | SPAD\_SDATA        | SPAD Conn. (VR1)    |
| 0 \(DIGITAL\)         | 28     | LASER\_0           | AUX0                |
| 0 \(DIGITAL\)         | 29     | LASER\_1           | AUX1                |
| 0 \(DIGITAL\)         | 30     | LASER\_2           | AUX2                |
| 0 \(DIGITAL\)         | 31     | LASER\_3           | AUX3                |
|                       |        |                    |                     |
| 1 \(ANALOG \+ DIG\.\) | AI 0   | ANALOG\_IN0        |                     |
| 1 \(ANALOG \+ DIG\.\) | \.\.\. | \.\.\.             |                     |
| 1 \(ANALOG \+ DIG\.\) | AO 0   | ANALOG\_OUT0       |                     |
| 1 \(ANALOG \+ DIG\.\) | \.\.\. |                    |                     |
| 1 \(ANALOG \+ DIG\.\) | 5      | PIXEL\_SYNC        |                     |
| 1 \(ANALOG \+ DIG\.\) | 6      | LINE\_SYNC         |                     |
| 1 \(ANALOG \+ DIG\.\) | 7      | FRAME\_SYNC        |                     |
| 1 \(ANALOG \+ DIG\.\) | 8      | AO\_TRIGGER\_TEST  |                     |
| 1 \(ANALOG \+ DIG\.\) | 0      | DET\_EXTRA\_0      |                     |
| 1 \(ANALOG \+ DIG\.\) | 1      | DET\_EXTRA\_1      |                     |
| 1 \(ANALOG \+ DIG\.\) | 10     | PIXEL\_IN          |                     |
| 1 \(ANALOG \+ DIG\.\) | 11     | LASER\_DEBUG       |                     |
| 1 \(ANALOG \+ DIG\.\) | 12     | LASER\_0\_BIS      |                     |
| 1 \(ANALOG \+ DIG\.\) | 13     | LASER\_1\_BIS      |                     |
| 1 \(ANALOG \+ DIG\.\) | 14     | LASER\_2\_BIS      |                     |
| 1 \(ANALOG \+ DIG\.\) | 15     | LASER\_3\_BIS      |                     |


### NI PXIe-7856R

| NI Connector          | NI DIO | BRIGHTEYES-MCS USB | GI-BOX              |
| --------------------- | ------ | ------------------ | ------------------- |
| 1 \(DIGITAL\)         | 0      | SPAD0              | SPAD Conn.          |
| 1 \(DIGITAL\)         | \.\.\. | \.\.               | \.\.\.              |
| 1 \(DIGITAL\)         | 24     | SPAD24             | SPAD Conn.          |
| 1 \(DIGITAL\)         | 25     | SPAD\_ENABLE       | SPAD Conn. (ENABLE) |
| 1 \(DIGITAL\)         | 26     | SPAD\_SCLK         | SPAD Conn. (VR0)    |
| 1 \(DIGITAL\)         | 27     | SPAD\_SDATA        | SPAD Conn. (VR1)    |
| 1 \(DIGITAL\)         | 28     | LASER\_0           | AUX0                |
| 1 \(DIGITAL\)         | 29     | LASER\_1           | AUX1                |
| 1 \(DIGITAL\)         | 30     | LASER\_2           | AUX2                |
| 1 \(DIGITAL\)         | 31     | LASER\_3           | AUX3                |
|                       |        |                    |                     |
| 0 \(ANALOG \+ DIG\.\) | AI 0   | ANALOG\_IN0        |                     |
| 0 \(ANALOG \+ DIG\.\) | \.\.\. | \.\.\.             |                     |
| 0 \(ANALOG \+ DIG\.\) | AO 0   | ANALOG\_OUT0       |                     |
| 0 \(ANALOG \+ DIG\.\) | \.\.\. |                    |                     |
| 0 \(ANALOG \+ DIG\.\) | 5      | PIXEL\_SYNC        |                     |
| 0 \(ANALOG \+ DIG\.\) | 6      | LINE\_SYNC         |                     |
| 0 \(ANALOG \+ DIG\.\) | 7      | FRAME\_SYNC        |                     |
| 0 \(ANALOG \+ DIG\.\) | 8      | AO\_TRIGGER\_TEST  |                     |
| 0 \(ANALOG \+ DIG\.\) | 0      | DET\_EXTRA\_0      |                     |
| 0 \(ANALOG \+ DIG\.\) | 1      | DET\_EXTRA\_1      |                     |
| 0 \(ANALOG \+ DIG\.\) | 10     | PIXEL\_IN          |                     |
| 0 \(ANALOG \+ DIG\.\) | 11     | LASER\_DEBUG       |                     |
| 0 \(ANALOG \+ DIG\.\) | 12     | LASER\_0\_BIS      |                     |
| 0 \(ANALOG \+ DIG\.\) | 13     | LASER\_1\_BIS      |                     |
| 0 \(ANALOG \+ DIG\.\) | 14     | LASER\_2\_BIS      |                     |
| 0 \(ANALOG \+ DIG\.\) | 15     | LASER\_3\_BIS      |                     |


### GENOA INSTRUMENt
#### GI-BOX \(PRISM\)

| Connector    | DIO    | LABEL  |     |
| ------------ | ------ | ------ | --- |
| C0 \(Left\)  | 28     | AUX0   |     |
| C0 \(Left\)  | 29     | AUX1   |     |
| C0 \(Left\)  | 30     | AUX2   |     |
| C0 \(Left\)  | 31     | AUX3   |     |
| C1 \(Right\) | 26     | AUX4   |     |
| C1 \(Right\) | 27     | AUX5   |     |
| C1 \(Right\) | 28     | AUX6   |     |
| C1 \(Right\) | 29     | AUX7   |     |
| C1 \(Right\) | 30     | AUX8   |     |
| C1 \(Right\) | 31     | AUX9   |     |
| C0 \(Left\)  | 26     | VR0    |     |
| C0 \(Left\)  | 27     | VR1    |     |
| C0 \(Left\)  | 25     | ENABLE |     |
| C1 \(Right\) | 24     | SDA    |     |
| C1 \(Right\) | 25     | SCL    |     |
| C1 \(Right\) | ExtCLK | EXTCLK |     |

#### GI-DAC

| Label  | DIO | Firmware Naming   |     |
| ------ | --- | ----------------- | --- |
| AO 0   | 0   | GI\_DAC\_SCLK0    |     |
|        | 1   | GI\_DAC\_SDIN0    |     |
|        | 2   | GI\_DAC\_SSYNC0   |     |
| AO 1   | 3   | GI\_DAC\_SCLK1    |     |
|        | 4   | GI\_DAC\_SDIN1    |     |
|        | 5   | GI\_DAC\_SSYNC1   |     |
| AO 2   | 6   | GI\_DAC\_SCLK2    |     |
|        | 7   | GI\_DAC\_SDIN2    |     |
|        | 8   | GI\_DAC\_SSYNC2   |     |
| AO 3   | 9   | GI\_DAC\_SCLK3    |     |
|        | 10  | GI\_DAC\_SDIN3    |     |
|        | 11  | GI\_DAC\_SSYNC3   |     |
| AO 4   | 12  | GI\_DAC\_SCLK4    |     |
|        | 13  | GI\_DAC\_SDIN4    |     |
|        | 14  | GI\_DAC\_SSYNC4   |     |
| DOUT   | 15  | GI\_DAC\_GI\_DIO0 |     |
|        | 16  | GI\_DAC\_GI\_DIO1 |     |
|        | 17  | GI\_DAC\_GI\_DIO2 |     |
|        | 18  | GI\_DAC\_GI\_DIO3 |     |
|        | 19  | GI\_DAC\_GI\_DIO4 |     |
| AI 0   | 20  | GI\_DAC\_SCLK5    |     |
|        | 21  | GI\_DAC\_DOUT5    |     |
|        | 22  | GI\_DAC\_CONVST5  |     |
| AI 1   | 23  | GI\_DAC\_SCLK6    |     |
|        | 24  | GI\_DAC\_DOUT6    |     |
|        | 25  | GI\_DAC\_CONVST6  |     |
| DIN    | 26  | GI\_DAC\_DIO5     |     |
|        | 27  | GI\_DAC\_DIO6     |     |
| N\.C\. | 28  | GI\_DAC\_30       |     |
|        | 29  | GI\_DAC\_31       |     |
|        | 30  | GI\_DAC\_28       |     |
|        | 31  | GI\_DAC\_29       |     |


# Registers

| Name                           | Type       | Read/Write | Description                                                                                                                                      |
| ------------------------------ | ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Main**                       |            |            |                                                                                                                                                  |
| Run                            | Bool       | RW         | Start the scanning                                                                                                                               |
| stop                           | Bool       | RW         | Stop the scanning                                                                                                                                |
| FSM Status                     | I16        | R          | Status of the FSM                                                                                                                                |
|                                |            |            |                                                                                                                                                  |
| **Scan Settings**              |            |            |                                                                                                                                                  |
| Cx                             | I32        | RW         | Wait Cycles per bin in 40MHz clk units (default: 40)                                                                                             |
| #timebinsPerPixel              | I32        | RW         | Number of timebins per pixel                                                                                                                     |
| #pixels                        | I32        | RW         | Number of pixel (X)                                                                                                                              |
| #lines                         | I32        | RW         | Number of lines (Y)                                                                                                                              |
| #frames                        | I32        | RW         | Number of frames (Z)                                                                                                                             |
| #repetition                    | I32        | RW         | Number of repetition (REP)                                                                                                                       |
| Offset/StartValue (V)          | Fxp-Array  | RW         | Array [x,y,z] offset in V                                                                                                                        |
| CalibrationFactors(V/step)     | Fxp-Array  | RW         | Array [x,y,z] calibration in V/step                                                                                                              |
| snake                          | Bool       | RW         | If enabled the scanning is performed as "snake-scanning" else use the normal "raster scanning" (default: False)                                  |
|                                |            |            |                                                                                                                                                  |
| **Analog Output**              |            |            |                                                                                                                                                  |
| (for all channels from 0 to 7) |            |            |                                                                                                                                                  |
| AnalogOUT7                     | Fxp        | R          | Current Voltage on AnalogOUT                                                                                                                     |
| AnalogSelector_7               | U8         | RW         | 0 => X, 1 => Y, 2 => Z, else constant DC value                                                                                                   |
| AnalogOutDC_7                  | Fxp        | RW         | Constant value for Analog Output                                                                                                                 |
|                                |            |            |                                                                                                                                                  |
| **Scanning Status**            |            |            |                                                                                                                                                  |
| cur_parity                     | Bool       | R          | Current Parity Line (for snake)                                                                                                                  |
| cur_cycle                      | I32        | R          | Current Cycle                                                                                                                                    |
| cur_t                          | I32        | R          | Current timebin                                                                                                                                  |
| cur_x                          | I32        | R          | Current X                                                                                                                                        |
| cur_y                          | I32        | R          | Current Y                                                                                                                                        |
| cur_z                          | I32        | R          | Current Z                                                                                                                                        |
| cur_rep                        | I32        | R          | Current Rep                                                                                                                                      |
|                                |            |            |                                                                                                                                                  |
| **Detection Configuration**    |            |            |                                                                                                                                                  |
| initializationTime             | U32        | RW         | SPAD configuration - time to wait before start acquisition                                                                                       |
| msgOut                         | U64        | RW         | SPAD configuration message cmd send                                                                                                              |
| msgLen                         | U8         | RW         | SPAD configuration message length                                                                                                                |
| Invert SDATA                   | Bool       | RW         | SPAD configuration invert the cmd logic (useful for some SPAD prototype)                                                                         |
| ClockDur                       | I64        | RW         | SPAD configuration - sync output duration (40 MHz units)                                                                                         |
| holdOff                        | U16        | RW         | holdOff time (FPGA based) in 120 MHz units                                                                                                       |
| DummyData                      | Bool       | RW         | If enable produces dummy data instead of using data from the detector                                                                            |
|                                |            |            |                                                                                                                                                  |
| **Laser Control**              |            |            |                                                                                                                                                  |
| WaitForLaser                   | I64        | RW         | Wait after turning on laser (in 40 MHz units)                                                                                                    |
| WaitAfterFrame                 | I64        | RW         | Wait after frame completation (in 40 MHz units)                                                                                                  |
| WaitOnlyFirstTime              | Bool       | RW         | Wait after turning on laser only the first time                                                                                                  |
| LaserOffAfterMeasurement       | Bool       | RW         | If active turn off the laser after a measurement                                                                                                 |
|                                |            |            |                                                                                                                                                  |
| **Circular Scanning Settings** |            |            |                                                                                                                                                  |
| ScanXVoltages                  | Fxp-Array  | RW         | Array of Voltages X for circular scanning                                                                                                        |
| ScanYVoltages                  | Fxp-Array  | RW         | Array of Voltages Y for circular scanning                                                                                                        |
| ScanZVoltages                  | Fxp-Array  | RW         | Array of Voltages Z for circular scanning                                                                                                        |
| CircularMotionActivate         | Bool       | RW         | If activate instead of scanning will use the ScanXVoltages or the data as set via FIFOIn                                                         |
|                                |            |            |                                                                                                                                                  |
| **Scanning LImits**            |            |            |                                                                                                                                                  |
| MaxXVoltages                   | Fxp        | RW         | Set Voltages Limits Max X Voltage                                                                                                                |
| MaxYVoltages                   | Fxp        | RW         | Set Voltages Limits Max Y Voltage                                                                                                                |
| MaxZVoltages                   | Fxp        | RW         | Set Voltages Limits Max Z Voltage                                                                                                                |
| MinXVoltages                   | Fxp        | RW         | Set Voltages Limits Min X Voltage                                                                                                                |
| MinYVoltages                   | Fxp        | RW         | Set Voltages Limits Min Y Voltage                                                                                                                |
| MinZVoltages                   | Fxp        | RW         | Set Voltages Limits Min Z Voltage                                                                                                                |
|                                |            |            |                                                                                                                                                  |
| **FIFO Settings**              |            |            |                                                                                                                                                  |
| activateFIFOAnalog             | Bool       | RW         | Activate the FIFO Analog                                                                                                                         |
| activateFIFODigital            | Bool       | RW         | Activate the FIFO Digital                                                                                                                        |
| FIFOAnalog_Overflow            | Bool       | R          | True when at least once the FIFOAnalog failed during the scan                                                                                    |
| FIFO_Overflow                  | Bool       | R          | True when at least once the FIFO failed during the scan                                                                                          |
| FIFO Failed                    | U64        | R          | Counter of cycles when the FIFOAnalog failed during the scan                                                                                     |
| FIFOAnalog Failed              | U64        | R          | Counter of cycles when the FIFO failed during the scan                                                                                           |
|                                |            |            |                                                                                                                                                  |
| **Laser Enable**               |            |            |                                                                                                                                                  |
| LaserEnable0                   | Bool       | RW         | Laser Enable 1                                                                                                                                   |
| LaserEnable1                   | Bool       | RW         | Laser Enable 2                                                                                                                                   |
| LaserEnable2                   | Bool       | RW         | Laser Enable 3                                                                                                                                   |
| LaserEnable3                   | Bool       | RW         | Laser Enable 4                                                                                                                                   |
|                                |            |            |                                                                                                                                                  |
| **Analog Input**               |            |            |                                                                                                                                                  |
| AnalogInputA                   | U8         | RW         | Select the Analog input for Analog A channel                                                                                                     |
| AnalogInputB                   | U8         | RW         | Select the Analog input for Analog B channel                                                                                                     |
|                                |            |            |                                                                                                                                                  |
| AnalogA differential           | Bool       | RW         | True: signal derivative during within the timebin; False: signal direct                                                                          |
| AnalogB differential           | Bool       | RW         | True: signal derivative during within the timebin; False: signal direct                                                                          |
|                                |            |            |                                                                                                                                                  |
| (for all channels from 0 to 7) |            |            |                                                                                                                                                  |
| AnalogA7 invert                | Bool       | RW         | True: signal inverted; False: signal not inverted                                                                                                |
| AnalogA7 integrate             | Bool       | RW         | True: signal integrated; False: signal not integrated. The integration is performed at the max ADC readout speed                                 |
| AnalogIN7                      | Fxp        | R          | Current Voltage on AnalogIN                                                                                                                      |
|                                |            |            |                                                                                                                                                  |
| **Digital Frequency Domain**   |            |            |                                                                                                                                                  |
| L1                             | U8         | RW         | A state of laser sync for DFD - AAA_AAA_BBB_BBB                                                                                                  |
| L2                             | U8         | RW         | B state of laser sync for DFD - AAA_000_BBB_000                                                                                                  |
| L3                             | U8         | RW         | C state of laser sync for DFD - AA0_0BB_00C_C00                                                                                                  |
| L4                             | U8         | RW         | D state of laser sync for DFD - A00_B00_C00_D00                                                                                                  |
| DFD_Activate                   | Bool       | RW         | Activate the DFD                                                                                                                                 |
| DFD Dwell time (120MHz)        | U32        | RW         | Time interval for the transmission of full histogram (in 120MHz units) (Default: 1e6)  <= USUALLY NOT USED                                       |
| DFD_Uses_Own_Dwelltime         | Bool       | RW         | False: use the pixel index parity for triggering the transmission of the DFD histogram; True: use the Dwell time set (Default: False)            |
| DFD_LaserSyncDebug             | Bool       | RW         | True: the channel 26 become the laser time reference (needed for a proper phasor analysis); False: channel 26 is connected to the channel_extra1 |
| DFD_px_Current                 | Fxp        | R          | Status of the DFD current pixel                                                                                                                  |
| DFD_px_Transmitted             | Fxp        | R          | Status of the DFD current pixel transmitted                                                                                                      |
| DFD_FSM_Acquisition            | Bool       | R          | Status of the DFD module if activated or not                                                                                                     |
| DFD_FIFO_Overflow              | Bool       | R          | Status of the overflow of the internal DFD FIFO                                                                                                  |
|                                |            |            |                                                                                                                                                  |
| **Costum Scanning Position**   |            |            |                                                                                                                                                  |
| LastAddrPixelwise              | U32        | R          | Internal use / Debug                                                                                                                             |
| LastAddrFramewise              | U32        | R          | Internal use / Debug                                                                                                                             |
| FIFOPositionReady              | Bool       | R          | Internal use / Debug                                                                                                                             |
| position_curr_addr             | U32        | R          | Internal use / Debug                                                                                                                             |
| position_X                     | Fxp        | R          | Internal use / Debug                                                                                                                             |
| position_Y                     | Fxp        | R          | Internal use / Debug                                                                                                                             |
| position_Z                     | Fxp        | R          | Internal use / Debug                                                                                                                             |
| position_begin_tx              | Bool       | R          | Internal use / Debug                                                                                                                             |
| position_extra                 | Bool       | R          | Internal use / Debug                                                                                                                             |
| position_pixelwise-framewise   | Bool       | R          | Internal use / Debug                                                                                                                             |
| position_end_tx                | Bool       | R          | Internal use / Debug                                                                                                                             |
| offset_curr_addr               | U32        | R          | Internal use / Debug                                                                                                                             |
| offset_X                       | Fxp        | R          | Internal use / Debug                                                                                                                             |
| offset_Y                       | Fxp        | R          | Internal use / Debug                                                                                                                             |
| offset_Z                       | Fxp        | R          | Internal use / Debug                                                                                                                             |
| offset_begin_tx                | Bool       | R          | Internal use / Debug                                                                                                                             |
| offset_extra                   | Bool       | R          | Internal use / Debug                                                                                                                             |
| offset_pixelwise-framewise     | Bool       | R          | Internal use / Debug                                                                                                                             |
| offset_end_tx                  | Bool       | R          | Internal use / Debug                                                                                                                             |
|                                |            |            |                                                                                                                                                  |
| **Internal / Debug**           |            |            |                                                                                                                                                  |
| shutters                       | Bool-Array | RW         | Internal use / Debug                                                                                                                             |
| Pixel tag                      | Bool       | RW         | Internal use / Debug                                                                                                                             |
| Line tag                       | Bool       | RW         | Internal use / Debug                                                                                                                             |
| Frame tag                      | Bool       | RW         | Internal use / Debug                                                                                                                             |
| Repetition tag                 | Bool       | RW         | Internal use / Debug                                                                                                                             |
| End of frame                   | Bool       | RW         | Internal use / Debug                                                                                                                             |
| LC                             | I64        | RW         | Internal use / Debug                                                                                                                             |
| turnOffPC                      | I64        | R          | Internal use / Debug                                                                                                                             |
| turnOffLC                      | I64        | R          | Internal use / Debug                                                                                                                             |
| turnOffFC                      | I64        | R          | Internal use / Debug                                                                                                                             |
| t                              | I32        | RW         | Internal use / Debug                                                                                                                             |
| rx                             | I32        | RW         | Internal use / Debug                                                                                                                             |
| ry                             | I32        | RW         | Internal use / Debug                                                                                                                             |
| rz                             | I32        | RW         | Internal use / Debug                                                                                                                             |
| rx2                            | I32        | RW         | Internal use / Debug                                                                                                                             |
| ry2                            | I32        | RW         | Internal use / Debug                                                                                                                             |
| rz2                            | I32        | RW         | Internal use / Debug                                                                                                                             |
| rrep                           | I32        | RW         | Internal use / Debug                                                                                                                             |

## FIFOs:

| Type | Board      | Type | Read/Write                     | Tested                                             |
| ---- | ---------- | ---- | ------------------------------ | -------------------------------------------------- |
| 1    | FIFO In    | U64  | Write <br> \(from PC to FPGA\) | Used only for the special case "custom positions"  |
| 2    | FIFO       | U64  | Read <br> \(from FPGA to PC\)  | Data from SPAD acquired from Digital Channels 25+2 |
| 3    | FIFOAnalog | U64  | Read <br> \(from FPGA to PC\)  | Data from selected Analog input A and B            |

### Data format:

#### Channels
Channels position on SPAD array 5x5.

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| 0   | 1   | 2   | 3   | 4   |
| 5   | 6   | 7   | 8   | 9   |
| 10  | 11  | 12  | 13  | 14  |
| 15  | 16  | 17  | 18  | 19  |
| 20  | 21  | 22  | 23  | 24  |

Moreover there are two extra channels called 25 and 26.

#### FIFO Digital

**25 channels**


The micro-image is transmitted in a specific format made of two U64 words.

Due to the physics of the system it has been assigned to the central elements more bits than the external ones. Here the table representing the number of bits for each channels.

Number of bit a channel:

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| 4   | 4   | 4   | 4   | 4   |
| 4   | 5   | 6   | 5   | 4   |
| 4   | 6   | 10  | 6   | 4   |
| 4   | 5   | 6   | 5   | 4   |
| 4   | 4   | 4   | 4   | 4   |



The micro-image is transmitted is trasmitted with the follwoing channels order:
- 1st word U64: 0, 1, 2, 3, 4, 5, 17, 18, 19, 20, 21, 22, 23, 24, 25.
- 2nd word U64: 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 26.


**49 channels**

Number of bit a channel:

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| 7   | 7   | 8   | 8   | 8   | 7   | 7   |
| 7   | 8   | 8   | 14  | 8   | 8   | 7   |
| 8   | 8   | 16  | 16  | 16  | 8   | 8   |
| 8   | 14  | 16  | 16  | 16  | 14  | 8   |
| 8   | 8   | 16  | 16  | 16  | 8   | 8   |
| 7   | 8   | 8   | 14  | 8   | 8   | 7   |
| 7   | 7   | 8   | 8   | 8   | 7   | 7   |





#### FIFO Analog
A word of U64 the first U32 bits are corresponding to the Analog A, and the other U32 bits are corresponding to the Analog B.


