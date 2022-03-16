# Intermediate-Arduino
## LCD Backpack
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
> All in all I enjoyed this assignment and look forward to more like it in the future.
