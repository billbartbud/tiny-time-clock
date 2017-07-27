# small-time-clock
Time clock based on Arduino NANO with an RTC and 64x128 OLED
The goal was to make a reliable but small clock and experiment to get it right.
Hardware: 
* Arduino NANO-Clone
* RTC module with battery back up and I2C interface connection
* 64 by 128 OLED screen for nice graphics
Software:
* RTC module (DS3231-Eric Ayars 4/11) and 
* OLED using the U8G2 library Universal 8bit Graphics Library (https://github.com/olikraus/u8g2/)
  Copyright (c) 2016, olikraus@gmail.com   All rights reserved.
* time-slicing task manager (Randall Schmidt).

The Circuit
Using a proto-board the NANO is mounted in the middle and the OLED display on one side and the
RTC module on the flip side with a barrel connector to power the clock with a 9V power adaptor.
Now the NANO has 2 LED that lit up; one for power and one for the OLED SPI interface and the RTC,
but a Heart Beat LED was added just to ensure the software is running. A Watch Dog Timeout could improve this code
to harden the software, so if the hardware acts up the whole unit will reboot.

The coding part for the most part is the managing the time by just incrementing the seconds to minutes, minutes to hours
etc. But the real tick here it to realize the NANO 16 MHz clock is not clocking the one second time-slicing task manager
at one second intervals. So a reference back to the RTC is necessary to move the NANO frequency up or down a bit, by 100,000 clock
cycles to keep the tick counter to tick-a-second. So every couple of minutes the RTC is read and the clock time compared and the
NANO frequency adjusted up or down.

The OLED has an SPI interface which also comes in an I2C interface and share pins with the RTC, which is also I2C. The graphics library
for this OLED takes up a lot of space so this NANO is running low on memory, but managable. Again this is an experiment to see
what can be done with a simple idea.

Additionally a temperature sensor is part of the OLED display, but the RTC has a temperature sensor as well. Just playin'.
