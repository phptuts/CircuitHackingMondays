# Arduino Basketball Scoreboard

A simple Arduino project that uses an IR sensor to detect when a ping pong ball passes through the hoop and automatically updates the score on a 4-digit TM1637 display.

**Date:** July 13, 2026

## Group Photo

TODO

## Memories

TODO

---

## Photos

![Project](./assets/basketball-arduino/project.png)

---

## Video
<video controls src="https://storage.googleapis.com/noah-education-videos/circuithackingmondays/arduino_basketball.mov" ></video>
---

## What it Does

When a ping pong ball passes through the hoop, the IR sensor detects it and the Arduino increases the score by 2 points. The current score is shown on the TM1637 display. Sending `RESTART` through the Serial Monitor resets the score back to zero.

---

## Components

* Arduino Uno
* TM1637 4-Digit Display
* IR Obstacle Sensor
* Jumper wires
* USB cable

---

## Wiring

| Arduino Pin | Component      | Component Pin |
| ----------- | -------------- | ------------- |
| 5V          | TM1637 Display | VCC           |
| GND         | TM1637 Display | GND           |
| D2          | TM1637 Display | CLK           |
| D3          | TM1637 Display | DIO           |
| 3.3V        | IR Sensor      | VCC           |
| GND         | IR Sensor      | GND           |
| D8          | IR Sensor      | OUT           |

![digital display Wires](./assets/basketball-arduino/digital_display.png)

![sensor wires](./assets/basketball-arduino/sensor_wires.png)


---

## Libraries

```cpp
#include <TM1637Display.h>
```

Library used:

* **TM1637Display**

---

## How it Works

1. The Arduino waits for the IR sensor to detect a ball.
2. When a ball is detected, the score increases by 2. 
3. The updated score is shown on the 4-digit display.
4. Typing `RESTART` into the Serial Monitor resets the score to zero.

---

## Possible Improvements

* Add a countdown timer.
* Add sound effects with a buzzer.
* Track the highest score.
* Add RGB lighting.
* Make the point value configurable.

---

## Lessons Learned

* Position the IR sensor carefully for reliable scoring.
* Allow enough space so the ball doesn't repeatedly trigger the sensor.
* The TM1637 display is simple to wire and only requires two digital pins.

---

## Code

```c++
#include <TM1637Display.h>

TM1637Display display(2, 3);
int score = 0;
void setup() {
    Serial.begin(115200);
    display.setBrightness(7);
    pinMode(8, INPUT);
    display.clear();
}

void loop() {
    if (Serial.available()) {
        String restart = Serial.readStringUntil('\n');
        if (restart == "RESTART") {
            score = 0;
            display.clear();
        }
    }

    if (!digitalRead(8)) {
        score += 2;
        display.showNumberDec(score);
        delay(1900);
    }  
}
```



