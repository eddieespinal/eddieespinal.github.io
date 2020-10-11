# Finding i2c devices connected to the ATMegaZero board

!> If you don't know the i2c address of a component connected to the ATMegaZero, you can use this simple code to scan for i2c devices connected to the board. Copy and paste this code to the Arduino IDE and run it on the **ATMegaZero**.

Please install the `I2CScanner` library by `Luis Llamas` from the **Library Manager** on the Arduino IDE.

```clike
/***************************************************
Copyright (c) 2018 Luis Llamas
(www.luisllamas.es)
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/

LICENSE-2.0
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License
****************************************************/
 
#include "I2CScanner.h"

I2CScanner scanner;

void setup() 
{
	Serial.begin(9600);
	while (!Serial) {};

	scanner.Init();
}

void loop() 
{
	scanner.Scan();
	delay(5000);
}
```