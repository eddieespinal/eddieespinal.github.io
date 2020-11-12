# ATMegaZero Learning Shield Demo

> This example code is for testing all of the features of the ATMegaZero Learning Shield.

# LED Demo

```clike
/*
 * This example code is for testing all of LEDs on the ATMegaZero Learning Shield.
 * 
 * You can purchase one of the ATMegaZero Learning Shield from the ATMegaZero Online Store at:
 * https://shop.atmegazero.com/products/atmegazero-learning-shield
 * 
 * For full documentation please visit https://atmegazero.com
 */
 
// Learning Shield Pins
const int GREEN_LED_PIN = A2;
const int YELLOW_LED_PIN = A1;
const int RED_LED_PIN = A0;

void setup()
{
  //Setup pin modes
  pinMode(GREEN_LED_PIN, OUTPUT);
  pinMode(YELLOW_LED_PIN, OUTPUT);
  pinMode(RED_LED_PIN, OUTPUT);
}

void loop() {
  // Turn LED ON
  digitalWrite(GREEN_LED_PIN, HIGH);
  delay(1000);
  digitalWrite(YELLOW_LED_PIN, HIGH);
  delay(1000);
  digitalWrite(RED_LED_PIN, HIGH);
  delay(1000);

  // Turn LED OFF
  digitalWrite(GREEN_LED_PIN, LOW);
  delay(1000);
  digitalWrite(YELLOW_LED_PIN, LOW);
  delay(1000);
  digitalWrite(RED_LED_PIN, LOW);
  delay(1000);
}

```

# Buzzer Demo

> You can find more sample songs here: https://github.com/robsoncouto/arduino-songs, make sure to update the buzzer pin number to pin #6 when you use these examples as they are using pin 11 and the Learning Shield is connected to pin #6.

```clike
/*
 * This example code is for testing all of the features of the ATMegaZero Learning Shield.
 * This demo requires the JC_Button library to be installed. Please add it from "Manage Libraries" page.
 * https://github.com/JChristensen/JC_Button
 * 
 * You can purchase one of the ATMegaZero Learning Shield from the ATMegaZero Online Store at:
 * https://shop.atmegazero.com/products/atmegazero-learning-shield
 * 
 * For full documentation please visit https://atmegazero.com
 */

#include <JC_Button.h>

// Melody notes
const int c = 261;
const int d = 294;
const int e = 329;
const int f = 349;
const int g = 391;
const int gS = 415;
const int a = 440;
const int aS = 455;
const int b = 466;
const int cH = 523;
const int cSH = 554;
const int dH = 587;
const int dSH = 622;
const int eH = 659;
const int fH = 698;
const int fSH = 740;
const int gH = 784;
const int gSH = 830;
const int aH = 880;

// Learning Shield Pins
const int BUZZER_PIN = 6;
const int GREEN_LED_PIN = A2;
const int YELLOW_LED_PIN = A1;
const int RED_LED_PIN = A0;
const int BUTTON_PIN = 7;

Button pushButton(BUTTON_PIN, 25, true, true);

int counter = 0;
 
void setup()
{
  //Setup pin modes
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(GREEN_LED_PIN, OUTPUT);
  pinMode(YELLOW_LED_PIN, OUTPUT);
  pinMode(RED_LED_PIN, OUTPUT);
}

void playBuzzer() {
  //Play first section
  firstSection();
 
  //Play second section
  secondSection();
 
  //Variant 1
  beep(f, 250);  
  beep(gS, 500);  
  beep(f, 350);  
  beep(a, 125);
  beep(cH, 500);
  beep(a, 375);  
  beep(cH, 125);
  beep(eH, 650);
 
  delay(500);
 
  //Repeat second section
  secondSection();
 
  //Variant 2
  beep(f, 250);  
  beep(gS, 500);  
  beep(f, 375);  
  beep(cH, 125);
  beep(a, 500);  
  beep(f, 375);  
  beep(cH, 125);
  beep(a, 650);  
 
  delay(650);
}
 
void loop()
{
  pushButton.read();

  if(pushButton.isPressed()){
    playBuzzer();
  }
}
 
void beep(int note, int duration)
{
  //Play tone on buzzerPin
  tone(BUZZER_PIN, note, duration);
 
  //Play different LED depending on value of 'counter'
  if(counter % 2 == 0)
  {
    digitalWrite(GREEN_LED_PIN, HIGH);
    delay(duration);
    digitalWrite(GREEN_LED_PIN, LOW);
  } else if(counter % 3 == 0)
  {
    digitalWrite(YELLOW_LED_PIN, HIGH);
    delay(duration);
    digitalWrite(YELLOW_LED_PIN, LOW);
  } else
  {
    digitalWrite(RED_LED_PIN, HIGH);
    delay(duration);
    digitalWrite(RED_LED_PIN, LOW);
  }
 
  //Stop tone on buzzerPin
  noTone(BUZZER_PIN);
 
  delay(50);
 
  //Increment counter
  counter++;
}
 
void firstSection()
{
  beep(a, 500);
  beep(a, 500);    
  beep(a, 500);
  beep(f, 350);
  beep(cH, 150);  
  beep(a, 500);
  beep(f, 350);
  beep(cH, 150);
  beep(a, 650);
 
  delay(500);
 
  beep(eH, 500);
  beep(eH, 500);
  beep(eH, 500);  
  beep(fH, 350);
  beep(cH, 150);
  beep(gS, 500);
  beep(f, 350);
  beep(cH, 150);
  beep(a, 650);
 
  delay(500);
}
 
void secondSection()
{
  beep(aH, 500);
  beep(a, 300);
  beep(a, 150);
  beep(aH, 500);
  beep(gSH, 325);
  beep(gH, 175);
  beep(fSH, 125);
  beep(fH, 125);    
  beep(fSH, 250);
 
  delay(325);
 
  beep(aS, 250);
  beep(dSH, 500);
  beep(dH, 325);  
  beep(cSH, 175);  
  beep(cH, 125);  
  beep(b, 125);  
  beep(cH, 250);  
 
  delay(350);
}

```

# Push Button Demo

```clike
/*
 * This example code is for testing the push button on the ATMegaZero Learning Shield.
 * 
 * You can purchase one of the ATMegaZero Learning Shield from the ATMegaZero Online Store at:
 * https://shop.atmegazero.com/products/atmegazero-learning-shield
 * 
 * For full documentation please visit https://atmegazero.com
 */
 
// Learning Shield Pins
const int BUTTON_PIN = 7; //D7
const int GREEN_LED_PIN = A2;

// Variables will change:
int lastState = LOW;
int currentState;

void setup()
{
  // The pull-up input pin will be HIGH when the switch is open and LOW when the switch is closed.
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  pinMode(GREEN_LED_PIN, OUTPUT);
}

void loop() {
  int currentState = digitalRead(BUTTON_PIN);

  if (lastState == LOW && currentState == HIGH) {
    digitalWrite(GREEN_LED_PIN, LOW);
  } else if (lastState == HIGH && currentState == LOW)  {
    digitalWrite(GREEN_LED_PIN, HIGH);
  }

  // save the the last state
  lastState = currentState;
}
```