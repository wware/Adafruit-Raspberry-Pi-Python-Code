Building the Gitbox
====

* https://github.com/wware/gitbox
* http://willware.blogspot.com/2016/01/graceful-shutdown-for-raspberry-pi.html

I need one GPIO to watch the shutdown warning signal. Let's use GPIO 18 for that.

Adafruit has figured out
[everything I need](https://learn.adafruit.com/drive-a-16x2-lcd-directly-with-a-raspberry-pi/)
for the LCD, including the IP address, and a nice clock too. Here is their
[code](https://github.com/adafruit/Adafruit-Raspberry-Pi-Python-Code/blob/master/Adafruit_CharLCD/Adafruit_CharLCD_IPclock_example.py).

The initializer on line 8 will have different arguments because the GPIOs will be a little different for an RPi 2.
```python
pins_db=[23, 17, 21, 22]
```
will need to become
```python
pins_db=[23, 27, 21, 22]
```

The Adafruit Python script is a loop that runs every 2 seconds, so it's perfect
for doing both the LCD and checking the shutdown warning. They also include the
/etc/init.d magic for starting it at bootup.

Ouch, kernel panic
----

This can happen for many different reasons.
[1](http://raspberrypi.stackexchange.com/questions/40854/kernel-panic-not-syncing-vfs-unable-to-mount-root-fs-on-unknown-block179-6)
[2](http://raspberrypi.stackexchange.com/questions/34872/kernel-panic-not-syncing-vfs-unknown-block-179-6-after-cloning-sd)
[3](http://raspberrypi.stackexchange.com/questions/4331/kernel-panic-unable-to-mount-root-fs-on-unknown-block-after-restart)
[4](http://raspberrypi.stackexchange.com/questions/1411/wont-boot-after-removing-and-inserting-the-sd-card)

I considered several possible causes.
* Maybe the RPi 2 requires different software because of the four cores? So I downloaded
  Ubuntu Mate specifically for the RPi 2 and got the same result. Nope.
* Maybe the power supply voltage is outside the 4.75 to 5.25 volt range? Nope, it is
  steady at 4.98 volts.
* Maybe I'm buying crappy micro SD cards? Apparently the board is
  [very picky](http://elinux.org/RPi_SD_cards) about these, so that's my best bet right now.
* Maybe the SD card really wants to be prepared in
  [a Linux VM](https://discourse.osmc.tv/t/kernel-panic-vfs-unable-to-mount-root-fs-on-unknown-block-179-2/2098/6#post_7).

As the bad SD card theory now looks likeliest, I [ordered a few](https://www.adafruit.com/products/2767)
from Adafruit that I hope will work better. How annoying.


APPARENTLY the RPi 2 needs different software distros than the RPi because of the
four cores or whatever. So I'm trying Ubuntu 15, we'll see how that goes. Well,
that didn't work.

