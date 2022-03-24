# Intermediate-Arduino
### Table of Contents
[LCD Backpack](https://github.com/dcaffer07/Intermediate-Arduino/blob/main/README.md#intermediate-arduino)

[Photointerrupter](https://github.com/dcaffer07/Intermediate-Arduino/blob/main/README.md#photointerrupters)



### LCD Backpack
#### Description:
> Fist, dsiplay "Hello World" on a Liquid Crystal.  Next add additioanl wiring and a button display a counter which increaases as a button is clicked, showing the amount of clicks.  This assigment will further develop and expand our knowledge and increase our capability in arduino.
#### Wriring 
> Very straight forward, simply connect the liquid crystal dysplay to a breadboard, **and attatch a button** so that they are connected and the display can incremint counter.
<img src="https://github.com/dcaffer07/Intermediate-Arduino/blob/main/media/How-to-use-Arduino-with-LCD1602-I2C-display-module.jpg?raw=true" alt="wiring2" style="width:500px;">

Image credit goes to [einstronic.com](https://einstronic.com/how-to-use-backlit-lcd-display-with-arduino-and-i2c-backpack-module/)

#### Code ([Credit goes to Cooper Moreland](https://sites.google.com/charlottesvilleschools.org/coopermoreland/intermediate-arduino/lcd-backpack-2)) *Comments are my own*

```C++
 
int buttonpin = 12; //initiallize pin
int buttonstate = 0;
int previousbuttonstate = 0;
int counter = 0; 
#include <Wire.h>
#include <LiquidCrystal_I2C.h> //set up LCD
LiquidCrystal_I2C lcd(0x27,16,2);  // set the LCD address to 0x27 for a 16 chars and 2 line display.  
//0x3F if 0x27 doesn't function.

void setup() {
  pinMode(buttonpin, INPUT); //initiallize button pin
  lcd.init();
  lcd.backlight();
}

void loop() {
  lcd.setCursor(0, 0); //set to fit
  lcd.print("Hello World"); //"hello world" displayed on line one.
  buttonstate = digitalRead(buttonpin); //button state
  lcd.setCursor(0, 1); //provide seperate lines for display 
  lcd.print("btn press#: "); //"btn press#: " displayed before count.
  if (buttonstate == HIGH && previousbuttonstate == LOW) { //when button pressed
    counter +=1; //counter number + 1 per press
    lcd.print(counter); //count displayed on LCD
  } 
  buttonstate = previousbuttonstate; //on event no press reset button state
  delay(200); //so that it doesn't move too fast, provide a delay.
}
```
#### Reflection:
> This assignemnt was very productive as it allowed for the introduction of new things with the incorporation of old things.  With that being said, some takaways...
> - Set LCD to correct brightness so that it looks clean when displayed.
> - Post projects, don't waste time on making wiring diagrams find someone elses.
> 
> All in all I enjoyed this assignment and look forward to more like it in the future.


### Photointerrupters
#### Description:
> Fist, make an LED turn on when an object is put between the legs of the photointerupter.  Next, add a counter to the serial moniter so that it tells you the number of times that the LED has been turned on.  Overall we want to expand our coding knowledge and futher our skills.
#### Wriring 
> Very straight forward, simply connect the photointerupter to an LED so that a light is initialized with an interuption.
<img src="https://github.com/dcaffer07/Intermediate-Arduino/blob/main/media/Screenshot%20(19).png" alt="wiring2" style="width:450px;">

Image credit goes to [Physicalcomputing.com](https://uwearduino.wordpress.com/2018/02/13/photo-interrupt-sensor-module-week-1/)

#### Code (worked w/ Cooper Moreland)

```C++
 
int Led = 8;
int photo = 2;
int val;
int photostate = 0;
volatile byte state = LOW;
int counter = 0; //variables

void setup() {
  pinMode(Led, OUTPUT); //set led as output
  pinMode(photo, INPUT_PULLUP);    //output/input pins
  Serial.begin(9600);           //links serial monitor
  attachInterrupt(digitalPinToInterrupt(photo), Read, CHANGE);   //interrupts photo pin, makes state unequal which turns LED on
}

void loop() {
  digitalWrite(Led, state);

  Serial.print(state);
  Serial.print("   ");
  Serial.println(counter/2);
}

void Read() {
  state = !state; //Makes state unequal
  counter++;

}
```
#### Reflection:
> This assignemnt was very productive as it allowed for the introduction of new things with the incorporation of old things.  With that being said, some takaways...
> - Read directions so that you know what to do for the assignemnt.  I found that to be very helpfull.
> - Don't add unnessecary delays because they are stupid and unhelpful.
> - Make sure that code is written periodically and make sure that pins are connectred to the correct places.
> 
> All in all I enjoyed this assignment and look forward to more like it in the future.

### Motor Control
#### Description:
> Make a motor control operate according to the state of a poitentiometer which has been attatched as well to a battery pack and arduino.
#### Wriring 
> Very straight forward, simply connect a potentiometer to a motor and a AA batery pack.
<img src="https://github.com/dcaffer07/Intermediate-Arduino/blob/main/media/Screenshot%20(21).png?raw=true" alt="wiring2" style="width:450px;">

Image credit goes to [Arduino.cc](https://create.arduino.cc/projecthub/ben/motor-controlled-with-arduino-553c11)

#### Code (worked w/ Cooper Moreland (comments are my own))

```C++
 
int pwmPin = 9; // provides pin w connections and destination
int pot = A0; // analog -> A0
int c1 = 0;   // variable c1
int c2 = 0;   // variable c2

void setup() { // generate loop
  Serial.begin(9600);
  pinMode(pwmPin, OUTPUT); 
  pinMode(pot, INPUT);  
}

void loop() {
  c2 = analogRead(pot); 
  c1 = 1024-c2;         // 1000 - c2 = c1
  digitalWrite(pwmPin, HIGH); 
  delayMicroseconds(c1);   
  digitalWrite(pwmPin, LOW);  
  delayMicroseconds(c2);  
    Serial.println (c2); print this sucker
}
```
#### Reflection:
> This assignemnt was very productive as it allowed for the introduction of new things with the incorporation of old things.  With that being said, some takaways...
> - Read directions so that you know what to do for the assignemnt.  I found that to be very helpfull.
> - Don't add unnessecary delays because they are stupid and unhelpful.
> - Make sure that code is written periodically and make sure that pins are connectred to the correct places.
> 
> All in all I enjoyed this assignment and look forward to more like it in the future.
