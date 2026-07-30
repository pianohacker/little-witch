# Little WitCH

The Little WitCH is a tiny but capable dev board for the WCH32V307, boasting:

- The WCH32V307 itself, with a single RISC-V RV32IMACF core
- Gigabit Ethernet via the MXL86110C PHY
- Raspberry-Pi-compatible I/O (with caveats), exposing:
  - Two SPI buses
  - Two I2C buses
  - PCM audio out
  - SDIO/eMMC
  - and/or 28 3.3V GPIO pins
- USB-C 2.0
- USB-1.1 via Raspberry-Pi-Zero-compatible test points
- Tag-Connect TC2030 SWD debugging

## Raspberry Pi compatibility

The WCH32V307's pin remapping can't make it a perfect match for the Raspberry Pi's peripherals. The
biggest caveat is the SPI and PCM outputs, which are all multiplexed together and overlapping:

- SPI3 is exposed on the same pins as the Pi's SPI0 bus.
- PCM is exposed on the same pins as the Pi, but only supports output.
- SPI2 can be exposed on the same pins as the Pi's SPI1 bus, _but_ these pins overlap with the MDIO bus
  of the Ethernet PHY. Also, as these pins overlap with the PCM pins, SPI2 must be switched to by
  cutting and resoldering three solder jumpers below the USB-C port.

That said, this should still allow compatibility with a wide number of Pi Zero / Pi 4 HATs. Will
mention specific examples here as they are tested.

## Solder jumper reconfiguration

There are three sets of solder jumpers that can modify the behavior of this board:

- The jumpers mentioned above, which collectively switch pins 12, 35, and 40 between SPI2 and PCM
  (via I2S3). These default to PCM. **Note:** to be explicit, to switch to SPI2 on these pins, the
  bridge between the first two pads of all three jumpers must be cut and the 2nd and 3rd jumpers
  solder-bridged.
- A jumper to set the value of BOOT1. This defaults to 0.
- A jumper to enable the power LED, which defaults to lit.

## Authors

This is a collaboration between Jesse Weaver (pianohacker) and [Pikkolo Assembly](https://www.pikkoloassembly.com/).

## License

Little WitCH © 2026 by Jesse Weaver is licensed under CC BY-NC-SA 4.0. To view a copy of this license, visit https://creativecommons.org/licenses/by-nc-sa/4.0/
