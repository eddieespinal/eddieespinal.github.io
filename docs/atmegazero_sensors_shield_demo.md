# ATMegaZero Sensors Shield Demo

> Sample code is for testing the ATMegaZero Sensors Shield on the Arduino IDE

# Accelerometer
```clike
/*
 * ATMegaZero Sensors Shield Accelerometer Demo
 * This sample code requires the Adafruit Library "Adafruit-MPU6050". Please install it before running this code.
 *
 * This example shows how to read the accelerometer values from the Sensors Shield
 * The i2c accelerometer address is 0x69
 *
 * You can buy this ATMegaZero Sensors Shield from the ATMegaZero Online Store at https://shop.atmegazero.com
 * For full documentation please visit https://atmegazero.com
 * 
*/

#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <Wire.h>

Adafruit_MPU6050 mpu;

void setup(void) {
  Serial.begin(115200);

  // Try to initialize!
  if (!mpu.begin(0x69)) {
    Serial.println("Failed to find MPU6050 chip");
    while (1) {
      delay(10);
    }
  }

  mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
  Serial.print("Accelerometer range set to: ");
  switch (mpu.getAccelerometerRange()) {
  case MPU6050_RANGE_2_G:
    Serial.println("+-2G");
    break;
  case MPU6050_RANGE_4_G:
    Serial.println("+-4G");
    break;
  case MPU6050_RANGE_8_G:
    Serial.println("+-8G");
    break;
  case MPU6050_RANGE_16_G:
    Serial.println("+-16G");
    break;
  }
  
  mpu.setGyroRange(MPU6050_RANGE_500_DEG);
  Serial.print("Gyro range set to: ");
  switch (mpu.getGyroRange()) {
  case MPU6050_RANGE_250_DEG:
    Serial.println("+- 250 deg/s");
    break;
  case MPU6050_RANGE_500_DEG:
    Serial.println("+- 500 deg/s");
    break;
  case MPU6050_RANGE_1000_DEG:
    Serial.println("+- 1000 deg/s");
    break;
  case MPU6050_RANGE_2000_DEG:
    Serial.println("+- 2000 deg/s");
    break;
  }

  mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);
  Serial.print("Filter bandwidth set to: ");
  switch (mpu.getFilterBandwidth()) {
  case MPU6050_BAND_260_HZ:
    Serial.println("260 Hz");
    break;
  case MPU6050_BAND_184_HZ:
    Serial.println("184 Hz");
    break;
  case MPU6050_BAND_94_HZ:
    Serial.println("94 Hz");
    break;
  case MPU6050_BAND_44_HZ:
    Serial.println("44 Hz");
    break;
  case MPU6050_BAND_21_HZ:
    Serial.println("21 Hz");
    break;
  case MPU6050_BAND_10_HZ:
    Serial.println("10 Hz");
    break;
  case MPU6050_BAND_5_HZ:
    Serial.println("5 Hz");
    break;
  }

  Serial.println("");
  delay(100);
}

void loop() {
  /* Get new sensor events with the readings */
  sensors_event_t a, g, temp;
  mpu.getEvent(&a, &g, &temp);

  /* Print out the values */
  Serial.print("Acceleration X: ");
  Serial.print(a.acceleration.x);
  Serial.print(", Y: ");
  Serial.print(a.acceleration.y);
  Serial.print(", Z: ");
  Serial.print(a.acceleration.z);
  Serial.println(" m/s^2");

  Serial.print("Rotation X: ");
  Serial.print(g.gyro.x);
  Serial.print(", Y: ");
  Serial.print(g.gyro.y);
  Serial.print(", Z: ");
  Serial.print(g.gyro.z);
  Serial.println(" rad/s");

  Serial.print("Temperature: ");
  Serial.print(temp.temperature);
  Serial.println(" degC");

  Serial.println("");
  delay(500);
}
```

# Real-Time Clock (RTC) DS1307
```clike

/*
 * ATMegaZero Sensors Shield Real-time Clock (RTC) DS1307 Demo
 *
 * This example shows how to read the values from the RTC DS1307 on the Sensors Shield
 * The i2c rtc address is 0x68
 *
 * You can buy this ATMegaZero Sensors Shield from the ATMegaZero Online Store at https://shop.atmegazero.com
 * For full documentation please visit https://atmegazero.com
 * 
*/

#include <Wire.h>
#include <RTC.h>

static DS1307 RTC;

void setup()
{
	Serial.begin(115200);
	RTC.begin();

	Serial.print("Is Clock Running: ");
	if (RTC.isRunning())
	{
		Serial.println("Yes");
		Serial.print(RTC.getDay());
		Serial.print("-");
		Serial.print(RTC.getMonth());
		Serial.print("-");
		Serial.print(RTC.getYear());
		Serial.print(" ");
		Serial.print(RTC.getHours());
		Serial.print(":");
		Serial.print(RTC.getMinutes());
		Serial.print(":");
		Serial.print(RTC.getSeconds());
		Serial.print("");
		if (RTC.getHourMode() == CLOCK_H12)
		{
			switch (RTC.getMeridiem()) {
			case HOUR_AM:
				Serial.print(" AM");
				break;
			case HOUR_PM:
				Serial.print(" PM");
				break;
			}
		}
		Serial.println("");
		delay(1000);
	}
	else
	{
		delay(1500);

		Serial.println("No");
		Serial.println("Setting Time");
		RTC.setHourMode(CLOCK_H12);
    //RTC.setHourMode(CLOCK_H24);
		RTC.setDateTime(__DATE__, __TIME__);
		Serial.println("New Time Set");
		Serial.print(__DATE__);
		Serial.print(" ");
		Serial.println(__TIME__);
		RTC.startClock();
	}
}

void loop()
{
  if (RTC.isRunning())
  {    
    Serial.print(RTC.getMonth());
    Serial.print("-");
    Serial.print(RTC.getDay());
    Serial.print("-");
    Serial.print(RTC.getYear());
    Serial.print(" ");
    Serial.print(RTC.getHours());
    Serial.print(":");
    Serial.print(RTC.getMinutes());
    Serial.print(":");
    Serial.print(RTC.getSeconds());
    Serial.print("");
    if (RTC.getHourMode() == CLOCK_H12)
    {
      switch (RTC.getMeridiem()) {
      case HOUR_AM:
        Serial.print(" AM");
        break;
      case HOUR_PM:
        Serial.print(" PM");
        break;
      }
    }
    Serial.println("");
    delay(1000);
  }
}
```

# Temperature, Humidity & Barometric Pressure
```clike
/*
 * ATMegaZero Sensors Shield BME280 humidity, temperature & pressure sensor demo
 * This sample code requires the Adafruit Library "Adafruit-BME280". Please install it before running this code.
 *
 * This example shows how to read the humidity, temperature & pressure values from the Sensors Shield
 * The i2c BME280 address is 0x77
 *
 * You can buy this ATMegaZero Sensors Shield from the ATMegaZero Online Store at https://shop.atmegazero.com
 * For full documentation please visit https://atmegazero.com
 * 
*/

#include <Wire.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_BME280.h>

#define SEALEVELPRESSURE_HPA (1013.25)

Adafruit_BME280 bme;

unsigned long delayTime;

void setup() {
    Serial.begin(9600);
    while(!Serial);    // time to get serial running

    unsigned status;
    
    // default settings
    status = bme.begin();  
    
    if (!status) {
        Serial.println("Could not find a valid BME280 sensor, check wiring, address, sensor ID!");
        Serial.print("SensorID was: 0x"); Serial.println(bme.sensorID(),16);
        while (1) delay(10);
    }
}

void loop() { 
    printValues();
    delay(1000);
}

void printValues() {
    Serial.print("Temperature = ");
    Serial.print(bme.readTemperature());
    Serial.println(" *C");

    float tempValue = bme.readTemperature() *9/5 + 32; //convert to Fahrenheit
    Serial.print("Temperature = ");
    Serial.print(tempValue);
    Serial.println(" *F");

    Serial.print("Pressure = ");

    Serial.print(bme.readPressure() / 100.0F);
    Serial.println(" hPa");

    Serial.print("Approx. Altitude = ");
    Serial.print(bme.readAltitude(SEALEVELPRESSURE_HPA));
    Serial.println(" m");

    Serial.print("Humidity = ");
    Serial.print(bme.readHumidity());
    Serial.println(" %");

    Serial.println();
}
```

# VOC SGP40 Sensor
```clike
/*
 * ATMegaZero Sensors Shield VOC index demo
 * This sample code requires the Adafruit Library "Adafruit-BME280" & "Adafruit_SGP40". Please install them before running this code.
 *
 * This example shows how to read the humidity, temperature & pressure values from the Sensors Shield
 * The i2c BME280 address is 0x77 & SGP40 address is 0x59
 *
 * You can buy this ATMegaZero Sensors Shield from the ATMegaZero Online Store at https://shop.atmegazero.com
 * For full documentation please visit https://atmegazero.com
 * 
*/

#include "Adafruit_SGP40.h"
#include <Adafruit_BME280.h>

#define SEALEVELPRESSURE_HPA (1013.25)
Adafruit_BME280 bme;
Adafruit_SGP40 sgp;

void setup() {
  Serial.begin(115200);

  if (!sgp.begin()) {
    Serial.println("SGP40 sensor not found :(");
    while (1);
  }

  Serial.print("Found SGP40 serial #");
  Serial.print(sgp.serialnumber[0], HEX);
  Serial.print(sgp.serialnumber[1], HEX);
  Serial.println(sgp.serialnumber[2], HEX);

  unsigned status;
  
  // default settings
  status = bme.begin();  
  if (!status) {
      Serial.println("Could not find a valid BME280 sensor, check wiring, address, sensor ID!");
      Serial.print("SensorID was: 0x"); Serial.println(bme.sensorID(),16);
      while (1) delay(10);
  }
}

int counter = 0;
void loop() {
  uint16_t sraw;
  int32_t voc_index;
  
  float t = bme.readTemperature();
  float tempValue = t *9/5 + 32;//convert to Fahrenheit
  Serial.print("Temp *F = "); Serial.print(tempValue); Serial.print("\t\t");
  float h = bme.readHumidity();
  Serial.print("Hum. % = "); Serial.println(h);

  sraw = sgp.measureRaw(t, h);
  Serial.print("Raw measurement: ");
  Serial.println(sraw);

  voc_index = sgp.measureVocIndex(t, h);
  Serial.print("Voc Index: ");
  Serial.println(voc_index);

  delay(1000);
}
```

# Analog Light Sensor - ADS1115
```clike
/*
 * ATMegaZero Sensors Shield ADS1115 Demo
 * This sample code requires the Adafruit Library "Adafruit_ADS1015". Please install it before running this code.
 *
 * This example shows how to read the accelerometer values from the Sensors Shield
 * The i2c ads1115 address is 0x48
 *
 * You can buy this ATMegaZero Sensors Shield from the ATMegaZero Online Store at https://shop.atmegazero.com
 * For full documentation please visit https://atmegazero.com
 * 
*/

#include <Wire.h>
#include <Adafruit_ADS1015.h>

 Adafruit_ADS1115 ads;

void setup(void) 
{
  Serial.begin(9600);  
  Serial.println("Getting single-ended readings from AIN0..3");
  Serial.println("ADC Range: +/- 6.144V (1 bit = 3mV/ADS1015, 0.1875mV/ADS1115)");
  
  // The ADC input range (or gain) can be changed via the following
  // functions, but be careful never to exceed VDD +0.3V max, or to
  // exceed the upper and lower limits if you adjust the input range!
  // Setting these values incorrectly may destroy your ADC!
  //                                                                ADS1015  ADS1115
  //                                                                -------  -------
  // ads.setGain(GAIN_TWOTHIRDS);  // 2/3x gain +/- 6.144V  1 bit = 3mV      0.1875mV (default)
  // ads.setGain(GAIN_ONE);        // 1x gain   +/- 4.096V  1 bit = 2mV      0.125mV
  // ads.setGain(GAIN_TWO);        // 2x gain   +/- 2.048V  1 bit = 1mV      0.0625mV
  // ads.setGain(GAIN_FOUR);       // 4x gain   +/- 1.024V  1 bit = 0.5mV    0.03125mV
  // ads.setGain(GAIN_EIGHT);      // 8x gain   +/- 0.512V  1 bit = 0.25mV   0.015625mV
  // ads.setGain(GAIN_SIXTEEN);    // 16x gain  +/- 0.256V  1 bit = 0.125mV  0.0078125mV
  
  ads.begin();
}

void loop(void) 
{
  int16_t adc0, adc1, adc2, adc3;

  adc0 = ads.readADC_SingleEnded(0);
  adc1 = ads.readADC_SingleEnded(1);
  adc2 = ads.readADC_SingleEnded(2);
  adc3 = ads.readADC_SingleEnded(3);

  // Light sensor is connected to adc0
  Serial.print("AIN0: "); Serial.println(adc0);
  
  Serial.print("AIN1: "); Serial.println(adc1);
  Serial.print("AIN2: "); Serial.println(adc2);
  Serial.print("AIN3: "); Serial.println(adc3);
  Serial.println(" ");
  
  delay(1000);
}
```