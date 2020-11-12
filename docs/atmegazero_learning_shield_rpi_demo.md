
# ATMegaZero Learning Shield Demo

> This example code is for testing all of the features of the ATMegaZero Learning Shield on the Raspberry Pi.

# LED Demo

```python
 # This example code is for testing all of the features of the ATMegaZero Learning Shield on the Raspbery Pi.
 #
 # You can purchase one of the ATMegaZero Learning Shield from the ATMegaZero Online Store at:
 # https://shop.atmegazero.com/products/atmegazero-learning-shield
 #
 # For full documentation please visit https://atmegazero.com

import RPi.GPIO as GPIO
import time

red_led_pin = 20
yellow_led_pin = 26
green_led_pin = 16

all_leds = [red_led_pin, yellow_led_pin, green_led_pin]

def setup():
    GPIO.setmode(GPIO.BCM)
    GPIO.setwarnings(False)
    # Set all the LED as output
    GPIO.setup(all_leds,GPIO.OUT)
	
def destroy():
    # Release resource
    GPIO.cleanup()

# Program start from here
if __name__ == '__main__':
	try:
		setup()
		for led in all_leds:
            print("turning LED on")
            GPIO.output(led, GPIO.HIGH)
            time.sleep(1)

        for led in all_leds:
            print("turning LED off")
            GPIO.output(led,GPIO.LOW)
            time.sleep(1)
        
        # Clean up
        destroy()
	except KeyboardInterrupt:  	# When 'Ctrl+C' is pressed, the child program destroy() will be  executed.
		destroy()

```

# Buzzer Demo

> You can find more sample songs here: https://github.com/gumslone/raspi_buzzer_player

```python
 # This example code is for testing all of the features of the ATMegaZero Learning Shield on the Raspbery Pi.
 #
 # You can purchase one of the ATMegaZero Learning Shield from the ATMegaZero Online Store at:
 # https://shop.atmegazero.com/products/atmegazero-learning-shield
 #
 # For full documentation please visit https://atmegazero.com

import RPi.GPIO as GPIO
import time

buzzer_pin_pin = 24

notes = {
	'B0' : 31,
	'C1' : 33, 'CS1' : 35,
	'D1' : 37, 'DS1' : 39,
	'EB1' : 39,
	'E1' : 41,
	'F1' : 44, 'FS1' : 46,
	'G1' : 49, 'GS1' : 52,
	'A1' : 55, 'AS1' : 58,
	'BB1' : 58,
	'B1' : 62,
	'C2' : 65, 'CS2' : 69,
	'D2' : 73, 'DS2' : 78,
	'EB2' : 78,
	'E2' : 82,
	'F2' : 87, 'FS2' : 93,
	'G2' : 98, 'GS2' : 104,
	'A2' : 110, 'AS2' : 117,
	'BB2' : 123,
	'B2' : 123,
	'C3' : 131, 'CS3' : 139,
	'D3' : 147, 'DS3' : 156,
	'EB3' : 156,
	'E3' : 165,
	'F3' : 175, 'FS3' : 185,
	'G3' : 196, 'GS3' : 208,
	'A3' : 220, 'AS3' : 233,
	'BB3' : 233,
	'B3' : 247,
	'C4' : 262, 'CS4' : 277,
	'D4' : 294, 'DS4' : 311,
	'EB4' : 311,
	'E4' : 330,
	'F4' : 349, 'FS4' : 370,
	'G4' : 392, 'GS4' : 415,
	'A4' : 440, 'AS4' : 466,
	'BB4' : 466,
	'B4' : 494,
	'C5' : 523, 'CS5' : 554,
	'D5' : 587, 'DS5' : 622,
	'EB5' : 622,
	'E5' : 659,
	'F5' : 698, 'FS5' : 740,
	'G5' : 784, 'GS5' : 831,
	'A5' : 880, 'AS5' : 932,
	'BB5' : 932,
	'B5' : 988,
	'C6' : 1047, 'CS6' : 1109,
	'D6' : 1175, 'DS6' : 1245,
	'EB6' : 1245,
	'E6' : 1319,
	'F6' : 1397, 'FS6' : 1480,
	'G6' : 1568, 'GS6' : 1661,
	'A6' : 1760, 'AS6' : 1865,
	'BB6' : 1865,
	'B6' : 1976,
	'C7' : 2093, 'CS7' : 2217,
	'D7' : 2349, 'DS7' : 2489,
	'EB7' : 2489,
	'E7' : 2637,
	'F7' : 2794, 'FS7' : 2960,
	'G7' : 3136, 'GS7' : 3322,
	'A7' : 3520, 'AS7' : 3729,
	'BB7' : 3729,
	'B7' : 3951,
	'C8' : 4186, 'CS8' : 4435,
	'D8' : 4699, 'DS8' : 4978
}

melody = [
  notes['E7'], notes['E7'], 0, notes['E7'],
  0, notes['C7'], notes['E7'], 0,
  notes['G7'], 0, 0,  0,
  notes['G6'], 0, 0, 0,
 
  notes['C7'], 0, 0, notes['G6'],
  0, 0, notes['E6'], 0,
  0, notes['A6'], 0, notes['B6'],
  0, notes['AS6'], notes['A6'], 0,
 
  notes['G6'], notes['E7'], notes['G7'],
  notes['A7'], 0, notes['F7'], notes['G7'],
  0, notes['E7'], 0, notes['C7'],
  notes['D7'], notes['B6'], 0, 0,
 
  notes['C7'], 0, 0, notes['G6'],
  0, 0, notes['E6'], 0,
  0, notes['A6'], 0, notes['B6'],
  0, notes['AS6'], notes['A6'], 0,
 
  notes['G6'], notes['E7'], notes['G7'],
  notes['A7'], 0, notes['F7'], notes['G7'],
  0, notes['E7'], 0, notes['C7'],
  notes['D7'], notes['B6'], 0, 0
]
tempo = [
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
 
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
 
  9, 9, 9,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
 
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
 
  9, 9, 9,
  12, 12, 12, 12,
  12, 12, 12, 12,
  12, 12, 12, 12,
]

def buzz(frequency, length):	 #create the function "buzz" and feed it the pitch and duration)

	if(frequency==0):
		time.sleep(length)
		return
	period = 1.0 / frequency 		 #in physics, the period (sec/cyc) is the inverse of the frequency (cyc/sec)
	delayValue = period / 2		 #calcuate the time for half of the wave
	numCycles = int(length * frequency)	 #the number of waves to produce is the duration times the frequency
	
	for i in range(numCycles):		#start a loop from 0 to the variable "cycles" calculated above
		GPIO.output(buzzer_pin, True)	 #set pin 27 to high
		time.sleep(delayValue)		#wait with pin 27 high
		GPIO.output(buzzer_pin, False)		#set pin 27 to low
		time.sleep(delayValue)		#wait with pin 27 low
	


def setup():
	GPIO.setmode(GPIO.BCM)
    GPIO.setwarnings(False)
	GPIO.setup(buzzer_pin, GPIO.OUT)
	
def destroy():
    # Release resource
	GPIO.cleanup()
	

def play(melody,tempo,pause,pace=0.800):
	
	for i in range(0, len(melody)):		# Play song
		
		noteDuration = pace/tempo[i]
		buzz(melody[i],noteDuration)	# Change the frequency along the song note
		
		pauseBetweenNotes = noteDuration * pause
		time.sleep(pauseBetweenNotes)

# Program start from here
if __name__ == '__main__':
	try:
		setup()
		print("Super Mario Theme")
		play(melody, tempo, 1.3, 0.800)
		time.sleep(2)		
		destroy()
	except KeyboardInterrupt:  	# When 'Ctrl+C' is pressed, the child program destroy() will be  executed.
		destroy()

```

# Push Button Demo

```python
 # This example code is for testing all of the features of the ATMegaZero Learning Shield on the Raspbery Pi.
 #
 # You can purchase one of the ATMegaZero Learning Shield from the ATMegaZero Online Store at:
 # https://shop.atmegazero.com/products/atmegazero-learning-shield
 #
 # For full documentation please visit https://atmegazero.com

import RPi.GPIO as GPIO
import time

push_button_pin = 23

def setup():
    GPIO.setmode(GPIO.BCM)
    GPIO.setwarnings(False)
    # Set all the LED as output
    GPIO.setup(push_button_pin, GPIO.IN, pull_up_down=GPIO.PUD_UP)
	
def destroy():
    # Release resource
    GPIO.cleanup()

# Program start from here
if __name__ == '__main__':
	try:
	    setup()

        print("Press the push button")
	    while True:
        input_state = GPIO.input(push_button_pin)
        if input_state == False:
            print("Button Pressed")
            time.sleep(0.2)
	except KeyboardInterrupt:  	# When 'Ctrl+C' is pressed, the child program destroy() will be  executed.
		destroy()
```