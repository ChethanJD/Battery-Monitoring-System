# Project Overview

## Aim

Build a low-cost prototype that monitors selected battery parameters during operation and stores measurements locally for later inspection.

## Working principle

1. The voltage and current sensors provide analog readings to the microcontroller.
2. The DS18B20 supplies a temperature reading.
3. The DS3231 provides date and time.
4. The Arduino calculates/display values on the LCD and sends a readable status line over Serial.
5. When the SD card is available, the sketch appends the readings to a CSV log.
6. The motor driver and DC motors provide a simple load for observing readings during operation.

## Main measured parameters

- Battery voltage (V)
- Current (A)
- Temperature (°C)
- A rough voltage-based battery percentage estimate
- Date and time for each record

## Current limitations

- The percentage calculation is a simplified estimate based on voltage and must be calibrated for the battery chemistry and discharge curve.
- Sensor calibration and measurement accuracy depend on the actual modules and wiring.
- The supplied code treats a disconnected temperature sensor as `0 °C`, which can be mistaken for a valid reading.
- Motor commands arrive through the serial interface; Bluetooth operation requires compatible physical wiring.
- This prototype is for demonstration and logging, not a replacement for a safety-rated BMS.
