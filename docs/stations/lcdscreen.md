# 📺 Secret Messages (LCD Screen)

Write your own messages on a 16×2 LCD screen! Press the button to switch between two different screens and create your own fun messages.

Coming Soon (TODO)

## Instructions

1. Change the four messages below and upload your code.
2. Press the button to switch between your two screens.

```cpp
String message1Line1 = "HELLO!";
String message1Line2 = "PRESS BUTTON";

String message2Line1 = "YOU FOUND";
String message2Line2 = "SECRET MODE";
```

## Challenges

### ⭐ Easy

Write:

- 👋 Your name
- 😊 Hello World

---

### ⭐⭐ Medium

Create:

- 😂 A funny joke
- 🎂 A birthday message
- 🎮 A game start screen
- ❤️ A message for a friend

---

### ⭐⭐⭐ Design Challenge

Create your own two-screen story!

Ideas:

- 🚀 Countdown → Blast Off!
- 👻 Knock Knock → Boo!
- 🐉 Dragon → Beware!
- 💎 Treasure → You Found It!
- 🎉 Ready? → Let's Go!

**Story Name:** _______________________

## Wiring

| Component | Arduino Pin |
|-----------|-------------|
| LCD SDA | A4 |
| LCD SCL | A5 |
| Push Button | 2 |
| LCD VCC | 5V |
| LCD GND | GND |

## Setup

This uses the [standard setup instructions](index.md).

This does use the libraries: LiquidCrystal_I2C

### Starter Code

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

const int BUTTON_PIN = 2;

String message1Line1 = "HELLO!";
String message1Line2 = "PRESS BUTTON";

String message2Line1 = "YOU FOUND";
String message2Line2 = "SECRET MODE";

bool lastButtonPressed = false;

void printLine(int row, String text)
{
    lcd.setCursor(0, row);

    while (text.length() < 16)
    {
        text += " ";
    }

    lcd.print(text.substring(0, 16));
}

void showMessage(String top, String bottom)
{
    lcd.clear();
    printLine(0, top);
    printLine(1, bottom);
}

void setup()
{
    lcd.init();
    lcd.backlight();

    pinMode(BUTTON_PIN, INPUT_PULLUP);

    showMessage(message1Line1, message1Line2);
}

void loop()
{
    bool buttonPressed = digitalRead(BUTTON_PIN) == LOW;

    if (buttonPressed != lastButtonPressed)
    {
        if (buttonPressed)
        {
            showMessage(message2Line1, message2Line2);
        }
        else
        {
            showMessage(message1Line1, message1Line2);
        }

        lastButtonPressed = buttonPressed;
    }
}
```