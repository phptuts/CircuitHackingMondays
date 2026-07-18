# Basketball Machine 

Build your own Arduino basketball game and see how many baskets you can score before time runs out. Change the game rules by adjusting the points per basket, game length, and winning score.


![Project](../assets/basketball-arduino/project.png)


## Video
<video controls src="https://storage.googleapis.com/noah-education-videos/circuithackingmondays/arduino_basketball.mov" ></video>


## Instructions

1. Change the two numbers in the code and upload to see what it does.

```ccp
int pointsPerShot = 2;
int gameLength = 30;
int winningScore = 20;
```

### Challenges


### ⭐ Easy

- Make each basket worth 1 point.
- Make each basket worth 5 points.

---

### ⭐⭐ Medium

Can you create:

- ⚡ Speed Round (15 seconds)
- 🏀 Long Game (60 seconds)
- 💯 Mega Points (10 points per basket)

---

### ⭐⭐⭐ Design Challenge

Design your own basketball game!

Give it a fun name.

Ideas:

- 🏀 Slam Dunk Challenge
- ⚡ Lightning Round
- 👑 King's Court
- 🚀 Space Basketball
- 🎯 Super Shooter

**Game Name:** _______________________

**Points Per Shot:** _______________________

**Game Length:** _______________________ seconds

## Wiring

| Arduino Pin | Component      | Component Pin |
| ----------- | -------------- | ------------- |
| 5V          | TM1637 Display | VCC           |
| GND         | TM1637 Display | GND           |
| 2           | TM1637 Display | CLK           |
| 3           | TM1637 Display | DIO           |
| 3.3V        | IR Sensor      | VCC           |
| GND         | IR Sensor      | GND           |
| 8           | IR Sensor      | OUT           |


![digital display Wires](../assets/basketball-arduino/digital_display.png)

![sensor wires](../assets/basketball-arduino/sensor_wires.png)

## Setup

This uses the [standard setup instructions](index.md).

### Starter Code

```cpp
#include <TM1637Display.h>

// ==========================================
// PLAY AREA
// ==========================================

int pointsPerShot = 2;
int gameLength = 30;   // Seconds
int winningScore = 20;

// ==========================================
// PINS
// ==========================================

const int DISPLAY_CLK_PIN = 2;
const int DISPLAY_DIO_PIN = 3;
const int RESET_BUTTON_PIN = 4;
const int BUZZER_PIN = 5;
const int SENSOR_PIN = 8;

TM1637Display display(DISPLAY_CLK_PIN, DISPLAY_DIO_PIN);

int score = 0;
unsigned long gameStartTime = 0;

bool gameRunning = false;
bool sensorWasBlocked = false;

void setup() {
  pinMode(SENSOR_PIN, INPUT);
  pinMode(RESET_BUTTON_PIN, INPUT_PULLUP);
  pinMode(BUZZER_PIN, OUTPUT);

  display.setBrightness(7);
  display.showNumberDec(0, true);

  startGame();
}

void loop() {
  if (digitalRead(RESET_BUTTON_PIN) == LOW) {
    startGame();
    delay(300);
  }

  if (!gameRunning) {
    return;
  }

  unsigned long elapsedTime = (millis() - gameStartTime) / 1000;

  if (elapsedTime >= gameLength) {
    endGame();
    return;
  }

  bool sensorBlocked = digitalRead(SENSOR_PIN) == LOW;

  // Count only once when the ball enters the sensor.
  if (sensorBlocked && !sensorWasBlocked) {
    score += pointsPerShot;

    display.showNumberDec(score, true);
    playBasketSound();

    if (score >= winningScore) {
      winGame();
    }
  }

  sensorWasBlocked = sensorBlocked;
}

void startGame() {
  score = 0;
  gameRunning = true;
  sensorWasBlocked = false;
  gameStartTime = millis();

  display.showNumberDec(score, true);
  playStartSound();
}

void endGame() {
  gameRunning = false;

  // Keep the final score on the display.
  display.showNumberDec(score, true);
  playEndSound();
}

void winGame() {
  gameRunning = false;

  for (int i = 0; i < 3; i++) {
    display.clear();
    tone(BUZZER_PIN, 900, 150);
    delay(200);

    display.showNumberDec(score, true);
    tone(BUZZER_PIN, 1300, 150);
    delay(200);
  }

  noTone(BUZZER_PIN);
}

void playBasketSound() {
  tone(BUZZER_PIN, 1000, 100);
  delay(120);
  tone(BUZZER_PIN, 1400, 100);
}

void playStartSound() {
  tone(BUZZER_PIN, 600, 100);
  delay(120);
  tone(BUZZER_PIN, 900, 100);
}

void playEndSound() {
  tone(BUZZER_PIN, 700, 250);
  delay(300);
  tone(BUZZER_PIN, 400, 400);
}
```