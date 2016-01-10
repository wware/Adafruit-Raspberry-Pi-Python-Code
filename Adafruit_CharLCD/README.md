APPARENTLY the RPi 2 needs different software distros than the RPi because of the four cores or whatever. So I'm trying Ubuntu 15, we'll see how that goes.

http://willware.blogspot.com/2016/01/graceful-shutdown-for-raspberry-pi.html

I need one GPIO to watch the shutdown warning signal. Let's use GPIO 18 for that.

Adafruit has figured out everything I need for the LCD, including IP address.
* https://learn.adafruit.com/drive-a-16x2-lcd-directly-with-a-raspberry-pi/
* https://github.com/adafruit/Adafruit-Raspberry-Pi-Python-Code/blob/master/Adafruit_CharLCD/Adafruit_CharLCD_IPclock_example.py

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
