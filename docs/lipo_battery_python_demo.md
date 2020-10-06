### ATMegaZero LIPO Battery Shield Raspberry Pi Demo

!> This is a demo for getting the battery level from the ATMegaZero Battery Shield connected to the Raspberry Pi using Python.

```python
import smbus
import time
import struct

bus = smbus.SMBus(1)
address = 0x55 # This is the i2c fuel gauge address on the ATMegaZero LIPO Battery Shield

fac = bus.read_i2c_block_data(address,0x0a,2)
(full_available_cap,) = struct.unpack('H', bytearray(fac)[0:2])
print "Full Available Capacity:", full_available_cap, 'mA'

soc = bus.read_i2c_block_data(address,0x1C,2)
(state_of_charge,) = struct.unpack('H', bytearray(soc)[0:2])
print "State of charge:", state_of_charge,"%"

```

> You can find more commands that you can use on page 11 of the > [Texas Instruments Documentation PDF](https://www.ti.com/lit/ds/symlink/bq27441-g1.pdf?ts=1601995908764&ref_url=https%253A%252F%252Fwww.google.com%252F)
