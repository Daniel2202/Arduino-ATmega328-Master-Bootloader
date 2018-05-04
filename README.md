Arduino-ATmega328-Master-Bootloader

An Arduino-Bootloader for the Atmega328 with different Clock frequencies and BOD-Levels

Created by Daniel Ulrich

-----------------------------------

With this bootloader you can use the ATmega328 with various clock frequencies. Baudrate-specialized frequencies as well as the "normal" ones. Internal and external.

Internal:
1 MHz, 8 MHz

External:
7.3728 MHz, 8 MHz, 12 MHz, 14.7456 MHz, 16 MHz, 18.432 MHz, 20 MHz

Further you can choose the BOD-Level (Brown-out Detection Level) if you want the microcontroller to shut down once the supply-voltage falls under a certain level.

-----------------------------------

Installation:

-Put the whole "ATmega328-Master" folder into the documents > arduino > hardware folder.

-That's it! You can now find the new board-versions under "tools" in your Arduino IDE.
