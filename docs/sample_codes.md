# Sample Code
> Here are some sample code you can run on the ATMegaZero.

### Blink LED
> Copy and paste this code to blink the internal LED connected to pin 13 on the ATMegaZero board.

```clike
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

### Store data to the SD Card

> This sample code will create a file on the SD card and will write the word "testing 1, 2, 3.". Please make sure to insert an SD card before running the code. 

```clike
#include <SPI.h>
#include <SD.h>

File myFile;

void setup() {
  // Open serial communications and wait for port to open:
  Serial.begin(9600);
  while (!Serial) {
    ; // wait for serial port to connect. Needed for native USB port only
  }

  Serial.print("Initializing SD card...");

  if (!SD.begin(4)) {
    Serial.println("initialization failed!");
    while (1);
  }
  Serial.println("initialization done.");

  // open the file. note that only one file can be open at a time,
  // so you have to close this one before opening another.
  myFile = SD.open("test.txt", FILE_WRITE);

  // if the file opened okay, write to it:
  if (myFile) {
    Serial.print("Writing to test.txt...");
    myFile.println("testing 1, 2, 3.");
    // close the file:
    myFile.close();
    Serial.println("done.");
  } else {
    // if the file didn't open, print an error:
    Serial.println("error opening test.txt");
  }

  // re-open the file for reading:
  myFile = SD.open("test.txt");
  if (myFile) {
    Serial.println("test.txt:");

    // read from the file until there's nothing else in it:
    while (myFile.available()) {
      Serial.write(myFile.read());
    }
    // close the file:
    myFile.close();
  } else {
    // if the file didn't open, print an error:
    Serial.println("error opening test.txt");
  }
}

void loop() {
  // nothing happens after setup
}
```

# Connect ESP-01 to the ATMegaZero
> Coming Soon!
```clike
/*
 *
 * Once connect to target Access Point
 *
 */
 #include <ESP8266_TCP.h>;
 
// ESP8266 Class
 ESP8266_TCP wifi;
 
// Target Access Point
 #define ssid "myWiFissid";
 #define pass "myWiFipassword";
 
 #define PIN_RESET 6
 
void setup()
 {
 delay(3000);
 
// and use Serial to debugging
 Serial.begin(115200);
 wifi.begin(Serial, PIN_RESET);
 
// Check that ESP8266 is available
 if(wifi.test())
 {
 // Connect to Access Point
 wifi.connectAccessPoint(ssid, pass);
 Serial.println("Connected to WiFi.")
 }
 else
 {
 // ESP8266 isn't available
 Serial.println("Check module connection and restart to try again...");
 }
 }
 
void loop()
{
}
```

# OLED Sample Code
> Coming Soon!