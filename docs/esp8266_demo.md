# ESP8266 Demo

> This example code is for connecting the ESP8266 module to the WiFi using the ATMegaZero board.
This demo requires the [WiFiEsp](https://github.com/bportaluri/WiFiEsp) library to be installed. Please add it from "Manage Libraries" page in the Arduino IDE.


```clike
/*
 * This example code is for connecting the ESP8266 module to the WiFi using the ATMegaZero board.
 * This demo requires the WiFiEsp library to be installed. Please add it from "Manage Libraries" page.
 * https://github.com/bportaluri/WiFiEsp
 * 
 * You can purchase one of this ESP-01S compaible WIFI Module from the ATMegaZero Online Store at:
 * https://shop.atmegazero.com
 * 
 * For full documentation please visit https://atmegazero.com
 */
 
#include <WiFiEspClient.h>
#include <WiFiEsp.h>
#include "SoftwareSerial.h"

#define WIFI_AP "YOUR_WIFI_NAME"
#define WIFI_PASSWORD "YOUR_WIFI_PASSWORD"


// Initialize the Wifi client object
WiFiEspClient client;

#define ESP_RX 8
#define ESP_TX 9

SoftwareSerial softwareSerial(ESP_TX, ESP_RX); // ATMegaZero_RX, ATMegaZero_TX

int status = WL_IDLE_STATUS;

void setup() {
  // initialize serial for debugging
  Serial.begin(9600);
  InitWiFi();
}

void loop() {
  delay(1000);
}

void InitWiFi()
{
  // initialize serial for ESP module
  softwareSerial.begin(9600);
  
  // initialize ESP module
  WiFi.init(&softwareSerial);
  
  // check for the presence of the module
  if (WiFi.status() == WL_NO_SHIELD) {
    Serial.println("WiFi module not present");
    // don't continue
    while (true);
  }

  Serial.println("Connecting to AP ...");
  // attempt to connect to WiFi network
  while ( status != WL_CONNECTED) {
    Serial.print("Attempting to connect to WPA SSID: ");
    Serial.println(WIFI_AP);
    // Connect to WPA/WPA2 network
    status = WiFi.begin(WIFI_AP, WIFI_PASSWORD);
    delay(500);
  }
  Serial.println("Connected to AP");

  printWifiStatus();
}

void printWifiStatus()
{
  // print the SSID of the network you're connected to
  Serial.print("SSID: ");
  Serial.println(WiFi.SSID());

  // print your WiFi module's IP address
  IPAddress ip = WiFi.localIP();
  Serial.print("IP Address: ");
  Serial.println(ip);

  // print the received signal strength
  long rssi = WiFi.RSSI();
  Serial.print("Signal strength (RSSI):");
  Serial.print(rssi);
  Serial.println(" dBm");
}
```

# Troubleshooting
!>Please Note: it may take a few tries before the ESP8266 module returns the correct IP Address. Compile the project again if it's not connencting properly. Also, make sure you follow the setup instructions that configures the WiFi module to communicate at `9600 baud rate` which is required for Software Serial communication.