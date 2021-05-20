# GPIO Pinouts

?> The ATMegaZero comes with 40 GPIO pins that can be used as input or output for interfacing devices and can be programmed using the Arduino IDE software.

|| Left Pins        |                      |                     | Right Pins                 ||
|-| ----------:     |:--------------------:|--------------------:|:---------------------------||
|| 3.3v             | :red_circle:         | :red_circle:        | 5v                         ||
|SDA| GPIO8         | :large_blue_circle:  | :red_circle:        | 5V                         ||
|SCL| GPIO9         | :large_blue_circle:  | :black_circle:      | GND                        ||
|| GPIO5            | :white_circle:       | :large_blue_circle: | GPIO43                     |TX|
|| GND              | :black_circle:       | :large_blue_circle: | GPIO44                     |RX|
|| GPIO33           | :white_circle:       | :white_circle:      | GPIO1                      ||
|| GPIO34           | :white_circle:       | :black_circle:      | GND                        ||
|| GPIO14           | :white_circle:       | :white_circle:      | GPIO4                      ||
|| 3.3v             | :red_circle:         | :white_circle:      | GPIO2                      ||
|SPI-MOSI| GPIO37   | :large_blue_circle:  | :black_circle:      | GND                        ||
|SPI-MISO| GPIO35   | :large_blue_circle:  | :white_circle:      | GPIO7                      ||
|SPI-SCLK| GPIO36   | :large_blue_circle:  | :large_blue_circle: | GPIO38                     |SPI-CS0|
|| GND              | :black_circle:       | :white_circle:      | GPIO21                     ||
|| RESET            | :x:                  | :x:                 |                            ||
|| GPIO11           | :white_circle:       | :black_circle:      | GND                        ||
|| GPIO10           | :white_circle:       | :white_circle:      | GPIO3                      ||
|| GPIO6            | :white_circle:       | :black_circle:      | GND                        ||
|| GPIO12           | :white_circle:       | :white_circle:      | GPIO13                     ||
|DAC_2| GPIO18      | :white_circle:       | :white_circle:      | GPIO17                     |DAC_1|
|| GND              | :black_circle:       | :white_circle:      | GPIO0                      ||