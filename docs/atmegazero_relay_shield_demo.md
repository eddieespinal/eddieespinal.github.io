# ATMegaZero Relay Shield Demo

> This sample code is for testing the ATMegaZero Relay Shield with the Arduino IDE

!> Important: Relay #4 uses pin 13, which is the same pin as the internal LED on the ATMegaZero board.  Try not to use the internal LED when using this board. Also, you might want to program your ATMegaZero board before connecting it to the relay shield to prevent switching relay #4 On & Off during sketch upload.

```clike
/*
 * This example code is for controlling the relays on the ATMegaZero Relay Shield using the Arduino IDE.
 * 
 * You can purchase one of the ATMegaZero Relay Shield from the ATMegaZero Online Store at:
 * https://shop.atmegazero.com/products/atmegazero-relay-shield
 * 
 * For full documentation please visit https://atmegazero.com
 */

const int relay1 = A4;
const int relay2 = 8;
const int relay3 = 12;
const int relay4 = 13;

void setup() {
  pinMode(relay1, OUTPUT);
  pinMode(relay2, OUTPUT);
  pinMode(relay3, OUTPUT);
  pinMode(relay4, OUTPUT);
}

void loop() {
  digitalWrite(relay1, HIGH);
  delay(500);
  digitalWrite(relay1, LOW);
  delay(1000);
  
  digitalWrite(relay2, HIGH);
  delay(500);
  digitalWrite(relay2, LOW);
  delay(1000);

  digitalWrite(relay3, HIGH);
  delay(500);
  digitalWrite(relay3, LOW);
  delay(1000);

  digitalWrite(relay4, HIGH);
  delay(500);
  digitalWrite(relay4, LOW);
  delay(1000);
}
```