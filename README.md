# LPS22HH Pico Driver

Micropython library for the ST LPS22HH pressure sensor

## Overview
The LPS22HH sensor is a high-resolution digital output pressure sensor manufactured by STMicroelectronics.
This driver enables seamless integration of the LPS22HH sensor with the Raspberry Pi Pico.

## Features
- Interface to communicate with the LPS22HH pressure sensor.
- Reading of pressure and temperature values
- Configuration of registers via dedicated functions
- Communication via SPI (I2C not implemented yet)
- Designed to be compatible with the Raspberry Pi Pico running on Micropython. Other boards not tested

## Installation
```bash
pip install lps22hh
```

## Getting Started
```python
from machine import SPI, Pin
from lps22hh import Lps22hh

# Create a new SPI device, and assign the pins corresponding to your device
cs_pin = Pin(1, Pin.OUT)
spi = SPI(0, baudrate=1000000, firstbit=SPI.MSB, sck=Pin(2), mosi=Pin(3), miso=Pin(0))

# Create a new instance of the Lps22hh sensor
sensor = Lps22hh(spi, cs_pin)

# By default, the device is in power-down mode and the ODR need to be changed
# for the device to take continuous measurements
sensor.data_rate = 200

# The Block Data Update (BDU) is used to inhibit the update of the output
# registers until all output registers parts are read, to avoids reading values
# from different sample times
sensor.block_data_update = 1

while True:
    if sensor.new_pressure_data:
        print(sensor.pressure)
```

## TODO
- [ ] FIFO functionalities
- [ ] Interrupts
- [ ] I2C, I3C communications

## Contributing
Contributions to this project are welcome. If you find any issues, have suggestions for improvements, or want to add new features, feel free to open an issue or submit a pull request.

## License
This project is licensed under the [MIT License](LICENSE). Feel free to use, modify, and distribute the code in accordance with the terms of the license.
