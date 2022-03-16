# Intermediate-Arduino
## LCD Backpack
#### Description:
> Fist, dsiplay "Hello World" on a Liquid Crystal.  Next add additioanl wiring and a button display a counter which increaases as a button is clicked, showing the amount of clicks.  This assigment will further develop and expand our knowledge and increase our capability in arduino.
#### Wriring 
> Very straight forward, simply connect the liquid crystal dysplay to a breadboard, **and attatch a button** so that they are connected and the display can incremint counter.
<img src="https://github.com/dcaffer07/Intermediate-Arduino/blob/main/media/How-to-use-Arduino-with-LCD1602-I2C-display-module.jpg?raw=true" alt="wiring2" style="width:500px;">

Image credit goes to [einstronic.com](https://einstronic.com/how-to-use-backlit-lcd-display-with-arduino-and-i2c-backpack-module/)

#### Code

```C++
 
int buttonpin = 12; //set pin for button to 12
int buttonstate = 0;
int previousbuttonstate = 0;
int counter = 0; 
#include <Wire.h>
#include <LiquidCrystal_I2C.h> 
LiquidCrystal_I2C lcd(0x27,16,2);  // set the LCD address to 0x27 for a 16 chars and 2 line display.  
// If 0x27 doesn't work, try 0x3F.

void setup() {
  pinMode(buttonpin, INPUT); //set button as input
  lcd.init();
  lcd.backlight();
}

void loop() {
  lcd.setCursor(0, 0); //set the lcd cursor to first column and first row respectively
  lcd.print("Hello World"); //lcd displays "hello world" on first line
  buttonstate = digitalRead(buttonpin); //read state of button
  lcd.setCursor(0, 1); //set cursor to column 1, row 2
  lcd.print("btn press#: "); //lcd displays "btn press#: " then the number of button presses
  if (buttonstate == HIGH && previousbuttonstate == LOW) { //if you press the button
    counter +=1; //counter goes up by 1
    lcd.print(counter); //lcd displays the counter value
  } 
  buttonstate = previousbuttonstate; //set the button to off after it is released
  delay(200); //delay so it doesn't count more than one value per press
}
```
#### Reflection:
> Easy. simple, but was great to get back into it!!!!!!!!!!!!!!!!!
