# Hardware and Wiring Notes

This document records the pin assignments currently defined in `src/BatteryMonitoringSystem.ino`. Confirm every connection against the actual modules before powering the circuit.

## Arduino pin assignments

| Module / signal | Arduino pin | Notes |
|---|---:|---|
| Voltage sensor output | A0 | Check divider ratio and maximum input voltage |
| ACS712 analog output | A1 | Confirm sensor variant and sensitivity |
| DS18B20 data | D3 | A suitable pull-up resistor is normally required on the OneWire data line |
| L298N enable | D6 | Enable control |
| L298N input 1 | D7 | Motor direction |
| L298N input 2 | D8 | Motor direction |
| SD card chip select | D10 | SPI pins depend on the selected Arduino board |
| LCD / RTC I²C | SDA/SCL | I²C bus; address configured as `0x27` for LCD |

## Shared interfaces

- LCD and RTC use I²C.
- SD card uses SPI.
- The firmware uses the DS3231 RTC library interface.
- The firmware uses Arduino `Serial` at 9600 baud for diagnostic output and single-character motor commands.

## Calibration values in the sketch

- ADC reference voltage: `5.0 V`
- Voltage scale factor: `5.0`
- ACS712 sensitivity: `0.066 V/A`
- LCD I²C address: `0x27`

These are starting values from the supplied firmware, not universal values. Calibrate them for your exact board and modules.

## Safety

Do not connect a battery voltage directly to an Arduino analog input unless it is safely scaled within the board's input range. Do not power motors from the Arduino's 5 V pin. Use an appropriate motor supply and follow the module's grounding and current requirements.
