# ESP8266 (ESP-01S) Baud Rate Configuration

The **ESP8266** comes pre-configured with a default `Baud Rate` of `115200`, but in order to use it with the ATMegaZero, we need to change it to `9600`. The following sample code will help you do that automatically. Just copy and paste it to the **Arduino IDE** and run it on the ATMegaZero with the **ESP8266** module connected to it.

> Copy and paste the following code to configure the **ESP8266** to the correct `Baud Rate` of `9600` in order to communicate with the ATMegaZero over **Software Serial**.

```clike
/*
 * This example code is for configuing the ESP8266 module on the ATMegaZero board.
 * 
 * You can purchase one of this ESP-01S compaible WIFI Module from the ATMegaZero Online Store at:
 * https://shop.atmegazero.com
 * 
 * For full documentation please visit https://atmegazero.com
 */
 
#include <SoftwareSerial.h>

#define ESP_RX 8
#define ESP_TX 9

SoftwareSerial espSerial(ESP_TX, ESP_RX); // RX, TX

bool espConfigured = false;

void setup() {
  Serial.begin(115200);
  while (!Serial) {
    ; // wait for serial port to connect.
  }
  
  Serial.println("Initializing");
  
  // set the data rate for the SoftwareSerial port
  espSerial.begin(115200);
  espSerial.println("Connecting to the ESP Module");
}

void loop() {

  // This will run once to configure the ESP8266 to the correct baud rate.
  if (espSerial.available() && !espConfigured) {
    Serial.println("Configuring the ESP8266 module to 9600 Baud Rate");
    
    espSerial.println("AT+UART_DEF=9600,8,1,0,0");
    delay(1000);
    espConfigured = true;

    Serial.println("Done");
  }
}
```

!>Once you run this code, the ESP8266 module will be configured to **9600 Baud Rate**. This only needs to be done once. After a successful run, you can compile different Sketches to use the WIFI module.