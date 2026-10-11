# Battery Monitoring System

An Arduino-based battery monitoring prototype that measures battery voltage, current, and temperature, displays readings on a 16×2 I²C LCD, and records timestamped measurements to an SD card.

## Features

- Measures battery voltage using an analog voltage-sensor module.
- Measures current using an ACS712 current sensor.
- Measures temperature using a DS18B20 sensor.
- Uses a DS3231 real-time clock (RTC) for timestamps.
- Displays readings on a 16×2 I²C LCD.
- Logs readings to `log.csv` on an SD card.
- Includes basic forward, backward, and stop motor-control functions through serial commands.
- Demonstrates monitoring under a motor load using a small wheeled prototype.

## Repository structure

```text
Battery-Monitoring-System/
├── src/
│   └── BatteryMonitoringSystem.ino
├── docs/
│   ├── hardware-and-wiring.md
│   └── project-overview.md
├── images/
│   ├── prototype-front-view.jpeg
│   └── prototype-rear-view.jpeg
├── examples/
│   └── sample-log.csv
├── .gitignore
├── LICENSE
└── README.md
```

## Hardware used

- Arduino Uno-compatible board
- Voltage sensor module (up to 25 V, subject to module specifications)
- ACS712 current sensor (check the exact current-range variant)
- DS18B20 temperature sensor
- DS3231 RTC module
- MicroSD card module and formatted microSD card
- 16×2 LCD with I²C backpack (configured at address `0x27`)
- L298N motor driver and DC motors
- Breadboard, jumper wires, and suitable power supply

The firmware uses `RTC_DS3231`; use a DS3231 module unless you adapt the code for a different RTC model.

## Software requirements

Install the Arduino IDE and these libraries through **Tools → Manage Libraries** (library names may vary slightly by publisher):

- RTClib
- OneWire
- DallasTemperature
- LiquidCrystal_I2C

`SPI`, `SD`, and `Wire` are included with the Arduino AVR board package.

## Setup

1. Open `src/BatteryMonitoringSystem.ino` in Arduino IDE.
2. Select the correct board and COM port.
3. Install the libraries listed above.
4. Wire the modules according to `docs/hardware-and-wiring.md`.
5. Insert a FAT16/FAT32-compatible microSD card into the SD module.
6. Check the sensor calibration constants and LCD I²C address before powering the circuit.
7. Upload the sketch and open Serial Monitor at **9600 baud**.
8. Read the displayed values and check the SD card for `log.csv`.

## Serial motor commands

The sketch reads single-character commands from the serial interface:

| Command | Action |
|---|---|
| `f` | Move forward |
| `b` | Move backward |
| `w` | Stop |
| `q` | Stop and halt the program loop |

These commands are received over the Arduino serial port. A separate Bluetooth module is only usable if it is physically connected to the same serial interface with appropriate wiring and baud-rate configuration.

## Data logging

The firmware appends measurements to `log.csv`. The sample file in `examples/` shows the intended columns:

`Date,Time,Voltage(V),Current(A),Temperature(C),Battery(%)`

The battery percentage calculation in this prototype is a simple voltage-based estimate, not a chemistry-specific state-of-charge measurement. Calibrate it for the actual battery before relying on it.

## Important notes

- This is an educational prototype, not a certified battery protection system.
- It does not implement cell balancing or comprehensive over-charge, over-discharge, over-current, or thermal cut-off protection.
- Verify all sensor readings against a multimeter/reference instrument before use.
- Check the exact ACS712 variant and its sensitivity. The source currently uses `0.066 V/A`, which corresponds to a particular variant and may not match your module.
- Confirm the voltage-divider ratio and ensure no Arduino analog input exceeds its permitted voltage.
- Use a common ground where required and keep motor power wiring appropriately separated from sensitive sensor wiring.
- The RTC type and code should match: this sketch uses DS3231.
- The source has been organized for publication, but the physical wiring and firmware should be validated on your exact hardware before deployment.

## Prototype photos

See the `images/` directory for front and rear views of the assembled prototype.

## License

Released under the MIT License; see `LICENSE`.
