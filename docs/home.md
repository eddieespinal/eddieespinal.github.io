# What's an ATMegaZero?

The ATMegaZero is a microcontroller board based on the Atmel ATMega32U4 microchip, the same chip used in the Arduino Leonardo and Arduino Micro. It was modeled after the Raspberry PI Zero to take advantage of its sleek design and form factor but in the form of a microcontroller board.
Similar to the Raspberry Pi Zero the ATMegaZero comes with 40 GPIO pins that can be used as input or output for interfacing devices and can be programmed using the Arduino IDE software. The ATMegaZero comes with a built-in USB which makes the ATMegaZero recognizable as a mouse or keyboard.

!> [Buy it from our Online Store](https://shop.atmegazero.com)

![ATMegaZero](./media/atmegazero_on_the_rock.jpg)

# :fas fa-people-arrows: - What is the difference between the Raspberry Pi and the ATMegaZero?

The Raspberry Pi is a linux computer which you can use to browse the web, word processing, gaming, etc.. It's perfect for many projects that requries a lot of power.  On the other hand, the ATMegaZero is a microcontroller similar to the Arduino board which you can use for simpler tasks that doesn't necessarely requires a lot of processing power but that is reliable. e.g. Home Automations, Robotics, DIY projects, control relays, servo, read sensor data, and also log data to the integrated SD card.

# :fas fa-question: - What can you do with an ATMegaZero that you can't do with a Raspberry Pi? 

* Very easy to get started.
* The ATMegaZero comes with a built-in USB which makes the ATMegaZero recognizable as a mouse or keyboard * on your computer.
* The ATMegaZero is best used for deterministic real-time operations, is fully predictable as to when it will do something and exactly how long it will take. The Raspberry Pi can't do such real-time tasks.
* Directly connect analog sensors, the Pi lacks an inbuilt analog to digital converter and relies on an external analog to digital converter (ADC).
* Raspberry Pi is good at software applications, while Arduino makes hardware projects simple.

# :fas fa-layer-group: - Can I combine them together? Use the ATMegaZero as a HAT?

You can, but you have to be very cautious as this can burn your Raspberry Pi since it runs on 3.3v logic and the ATMegaZero runs on 5v logic. The way we got it to work successfully was via i2c by setting the Raspberry Pi as the Master and the ATMegaZero as the slave. That helped ensure that the communication between the Pi and the ATMegaZero was done at 3.3v and not 5v.

We are working on a shield that will be sandwich between the Raspberry Pi and the ATMegaZero that will have bi-directional level shifters and allow you to communicate via i2c and serial connection.

# :fas fa-dollar-sign: - Why does the ATMegaZero cost more than the Raspberry Pi Zero?

The low price on the Raspberry Pi Zero is mainly because of volume. They order hundreds of thousands at a time bringing the production cost down, the more units they manufacture the cheaper the product will be. Unfortunately, I don't have the ability to produce thousands of units as they do and thus the cost to produce them is very high at the moment. My goal is to get there one day but it takes supporters like you to help me accomplish that :far fa-smile-wink:.