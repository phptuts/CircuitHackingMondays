# Teacher Notes — Create Your Own RGB Color

<video controls src="https://storage.googleapis.com/noah-education-videos/circuithackingmondays/arduino-rgbled.mov" ></video>


## Wiring

![rgb led](../assets/stations/rgbled/rgb_led.jpg)

![wires](../assets/stations/rgbled/wires.png)

### Arduino Connections

| RGB LED Connection   | Arduino Pin |
| -------------------- | ----------: |
| Red                  |         D11 |
| Green                |         D10 |
| Blue                 |          D9 |
| Ground — longest leg |         GND |

Each red, green, and blue leg should use a resistor.


## How the RGB LED Works

The LED contains three smaller lights:

* Red
* Green
* Blue

Each color uses a number between `0` and `255`.

* `0` means that color is off.
* `255` means that color is at full brightness.
* Numbers between `0` and `255` create different brightness levels.

Mixing the three values creates a new color.

## Student Activity

### Create Your Own Color

Find these three lines near the top of the code:

```cpp
int red = 100;
int green = 0;
int blue = 100;
```

Change the numbers to create your own color.

Then:

1. Copy the code.
2. Open Duino.
3. Connect the Arduino.
4. Upload the code.
5. Look at the color produced by the LED.
6. Change the numbers and try again.

[Open the Arduino Upload Instructions](TODO)

---

## Starter Code

```cpp
/// EDIT COLORS

int red = 100;
int green = 0;
int blue = 100;

int RED_PIN = 11;
int GREEN_PIN = 10;
int BLUE_PIN = 9;

void setup() {
  pinMode(RED_PIN, OUTPUT);
  pinMode(GREEN_PIN, OUTPUT);
  pinMode(BLUE_PIN, OUTPUT);

  analogWrite(RED_PIN, red);
  analogWrite(GREEN_PIN, green);
  analogWrite(BLUE_PIN, blue);
}

void loop() {
}
```

---

## Colors to Try

| Color      | Red | Green | Blue |
| ---------- | --: | ----: | ---: |
| Red        | 255 |     0 |    0 |
| Green      |   0 |   255 |    0 |
| Blue       |   0 |     0 |  255 |
| Purple     | 150 |     0 |  150 |
| Yellow     | 255 |   100 |    0 |
| Cyan       |   0 |   150 |  150 |
| White      | 255 |   255 |  255 |
| Light pink | 255 |    40 |  100 |

The exact colors may look different depending on the LED and the room lighting.


## Things to Try

* Create your favorite color.
* Make the LED brighter.
* Make the LED dimmer.
* Create the strangest color you can.
* Try changing only one number at a time.
* Try to create white without using the example table.


## Teacher Notes

Keep the explanation short. Students do not need a detailed lesson about PWM before experimenting.

A simple explanation is enough:

> The Arduino rapidly turns each color on and off to control how bright it appears.

Let students change the numbers and upload repeatedly. The immediate feedback is the lesson.

Some RGB LEDs may use common anode instead of common cathode. With a common-anode LED, the brightness values work in reverse. This page assumes the longest leg connects to ground and that larger numbers create brighter colors.



## Memories

*Add photos and notes after the class.*

* What colors did people create?
* Did anyone discover an unexpected color?
* Which color was the class favorite?
* What made people laugh?
