
# ATMegaZero Relay Shield Raspberry Pi Demo

> This example code is for controlling the ATMegaZero Relay Shield with the Raspberry Pi Zero.

![ATMegaZero OLED Display](https://cdn.shopify.com/s/files/1/0489/4720/0154/files/DSC_6771_01_2_600x600.jpg?v=1622828763)

!> Please make sure to set the green jumper to 3.3v when using this board with the Raspberry Pi Zero.

```python
 # This example code is for controlling the ATMegaZero Relay Shield with the Raspberry Pi Zero.
 #
 # You can purchase one of the ATMegaZero Relay Shield from the ATMegaZero Online Store at:
 # https://shop.atmegazero.com/products/atmegazero-relay-shield
 #
 # For full documentation please visit https://atmegazero.com

import RPi.GPIO as GPIO
import time

relay1_pin = 7
relay2_pin = 13
relay3_pin = 31
relay4_pin = 29

all_relays = [relay1_pin, relay2_pin, relay3_pin, relay4_pin]

def setup():
    GPIO.setmode(GPIO.BOARD)
    GPIO.setwarnings(False)
    # Set all the relays as output
    GPIO.setup(all_relays, GPIO.OUT)
	
def destroy():
    # Release resource
    GPIO.cleanup()

# Program start from here
if __name__ == '__main__':
	try:
		setup()
		while True:
			for relay in all_relays:
				GPIO.output(relay, True)
				time.sleep(0.5)
				GPIO.output(relay, False)
				time.sleep(1)
	except KeyboardInterrupt:
		destroy()

```