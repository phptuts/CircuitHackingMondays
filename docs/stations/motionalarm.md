# 🚨 Motion Alarm

## Overview

Build your own motion alarm using an Arduino, motion sensor, LED, and buzzer.

When motion is detected:

- 🚨 The LED flashes.
- 🔊 The buzzer sounds.

Students customize the alarm by changing only **two variables**:

- **Alarm Delay** – How quickly the alarm flashes.
- **Alarm Sound** – The pitch of the buzzer.
<video controls src="https://storage.googleapis.com/noah-education-videos/circuithackingmondays/motion-alarm.mp4" ></video>


![project](../assets/stations/motion-alarm/project.png)

## Components

| Qty | Part |
|-----|------|
| 1 | Arduino Uno |
| 1 | Breadboard |
| 1 | Motion Sensor |
| 1 | Red LED |
| 1 |  Resistor |
| 1 | Passive Buzzer |
| 1 | USB Cable |
| — | Jumper Wires |

---

## Circuit

> 📷 *Insert circuit photo here.*


## Wiring

| Component | Arduino Pin |
|-----------|-------------|
| Motion Sensor OUT | 4 |
| Passive Buzzer | 5 |
| LED | 7 |
| Motion Sensor VCC | 5V |
| Motion Sensor GND | GND |
| LED GND | GND (through 220Ω resistor) |
| Buzzer GND | GND |


## Code

```cpp
int alarmDelay = 100;
int alarmSound = 300;

int SENSOR_PIN = 4;
int BUZZER_PIN = 5;
int LED_PIN = 7;

void setup() {
  Serial.begin(115200);

  pinMode(SENSOR_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  if (!digitalRead(SENSOR_PIN)) {

    tone(BUZZER_PIN, alarmSound);

    digitalWrite(LED_PIN, HIGH);

    delay(alarmDelay);

    noTone(BUZZER_PIN);

    digitalWrite(LED_PIN, LOW);

    delay(alarmDelay);
  }
}
```


## Student Play Area

Students should only edit these two lines:

```cpp
int alarmDelay = 100;
int alarmSound = 300;
```

---

## What the Variables Do

### `alarmDelay`

Controls how quickly the LED flashes and the buzzer beeps.

| Value | Effect |
|-------:|--------|
| 25 | Very Fast |
| 100 | Normal |
| 300 | Slow |
| 700 | Very Slow |

---

### `alarmSound`

Controls the pitch of the buzzer.

| Value | Effect |
|-------:|--------|
| 150 | Low |
| 300 | Medium |
| 600 | High |
| 1000 | Very High |

---

## Student Challenges

### ⭐ Easy

- Make the alarm as fast as possible.
- Make the alarm as slow as possible.

### ⭐⭐ Medium

- Make the lowest sounding alarm.
- Make the highest sounding alarm.

### ⭐⭐⭐ Hard

Invent your own security system!

Ideas:

- 👽 Alien Detector
- 🍪 Cookie Protector
- 🐉 Dragon Alarm
- 🏰 Castle Security
- 💎 Treasure Guard

