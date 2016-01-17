Building the Gitbox
====

* https://github.com/wware/gitbox
* http://willware.blogspot.com/2016/01/graceful-shutdown-for-raspberry-pi.html
* https://github.com/wware/rpi-shutdown

I need one GPIO to watch the shutdown warning signal. Let's use GPIO 18 for that.

Adafruit has figured out
[everything I need](https://learn.adafruit.com/drive-a-16x2-lcd-directly-with-a-raspberry-pi/)
for the LCD, including the IP address, and a nice clock too. Here is their
[code](https://github.com/adafruit/Adafruit-Raspberry-Pi-Python-Code/blob/master/Adafruit_CharLCD/Adafruit_CharLCD_IPclock_example.py).

The Adafruit Python script is a loop that runs every 2 seconds, so it's perfect
for doing both the LCD and checking the shutdown warning. They also include the
/etc/init.d magic for starting it at bootup.

I'm using a Raspberry Pi 2, which is pretty picky about which SD card you use.
If it doesn't like your SD card, the RPi2 gives you a kernel panic. I solved
this problem by buying pre-loaded
[SD cards from Adafruit](https://www.adafruit.com/product/2767).
