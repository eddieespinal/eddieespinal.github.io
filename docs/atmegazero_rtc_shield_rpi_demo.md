
# ATMegaZero Realtime Clock (RTC) Shield Demo

> This example code is for testing the ATMegaZero RTC Shield on the Raspbery Pi.

!> This demo requires the following library to be downloaded first https://github.com/switchdoclabs/RTC_SDL_DS3231

## Raspberry Pi - Realtime Clock (RTC) Python Demo

```python
 # This example code is for testing the ATMegaZero RTC Shield on the Raspbery Pi.
 # This demo requires the following library to be downloaded first.
 # https://github.com/switchdoclabs/RTC_SDL_DS3231
 #
 # You can purchase one of the ATMegaZero RTC Shield from the ATMegaZero Online Store at:
 # https://shop.atmegazero.com/products/atmegazero-rtc-shield-ds3231
 #
 # For full documentation please visit https://atmegazero.com

import sys
import time
import datetime

import SDL_DS3231

print  "Testing the ATMegaZero RTC Shield"

ds3231 = SDL_DS3231.SDL_DS3231(1, 0x68)
ds3231.write_now()

# To make the DS3231 hardware clock different from the Pi’s clock, we can use the write_all() command. e.g.
# ds3231.write_all(seconds,minutes,hours,day,date,month,year,save_as_24h=True)

# Main Loop, reads and prints values of the clock

while True:
    print "Raspberry Pi =\t" + time.strftime("%Y-%m-%d %H:%M:%S")
    print "DS3231 =\t\t%s" % ds3231.read_datetime()
    print "DS3231 Temp =", ds3231.getTemp()
    time.sleep(10.0)

```
## Result

```python
$ python rtc_demo.py
Testing the ATMegaZero RTC Shield
Raspberry Pi =	2020-12-08 17:36:28
DS3231 =		2020-12-08 17:36:28
DS3231 Temp = 30.0
```