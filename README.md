# msp430fr-bsl

## Rationale

I had grand plans this weekend, to start some hobby project work using the MSP430FR2433 Launchpad as a platform to test some ideas out on.
My dreams were sadly crushed when code composer studio (CCS) seemingly 'bricked' the on-board eZ-FET debug probe. (Who knew a debug probe needed so many updates?!)

Despite following the warning not to power off the device during the update, the process failed.  Even after installing a newer CCS version, the probe remained unresponsive, with two static LEDs on the eZ-FET MCU and no sign of it enumerating.

After wasting a bit of time on this, I figured why not start looking into the ROM BSL on the MSP430FR series - getting around the need to use the launchpad debugger for loading code (on or off board). Precious project time often gets burned on the stuff not directly related to the task at hand.

## Python BSL

A python serial boot loader CLI for MSP430FR series microcontrollers. This has also been converted to a graphical interface.

## Serial Debug Adaptor

Includes a 'debug adaptor' - which can be any +3.3V development board.
- A Raspberry Pi Pico used as a serial bridge between the host and target boards
- The Pico communicates to the host over fast serial (native USB serial)
- The Pico forwards bytes to/from the target at it's less common 9600/8E1 serial port config
- Since the BSL has specific host-to-target message headers/framing - we can use in-band signalling to control the MSP430 target hardware.

https://github.com/peteEH/pico-msp430-debug
