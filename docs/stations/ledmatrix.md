# LED Matrix Animation Studio

Create your own pixel art and animations for a 8×8 LED matrix using a simple web-based editor. Design your animation, copy the generated Arduino code, upload it, and watch your creation come to life!

## Project

![Project](../assets/stations/ledmatrix/project.png)

## Video

<video controls src="https://storage.googleapis.com/noah-education-videos/circuithackingmondays/ledmatrix-station-arduino.mov" ></video>

## Duino App Libraries

- LedControl

## What It Does

This project lets you design animations for a 8×8 LED matrix without writing binary by hand.

Using the web editor you can:

* Draw pixel art
* Create multiple animation frames
* Change the animation speed
* Automatically generate Arduino code
* Copy and paste the generated code into the Arduino IDE

## Components

* Arduino Uno
* 8×8 MAX7219 LED Matrix 
* USB cable
* Jumper wires

## Wiring

| Arduino Pin | LED Matrix Pin | Purpose     |
| ----------- | -------------- | ----------- |
| 5V          | VCC            | Power       |
| GND         | GND            | Ground      |
| 12          | DIN            | Data        |
| 11          | CLK            | Clock       |
| 10          | CS / LOAD      | Chip Select |

---

## Setup

- Go to this site and [Web Animation Editor](https://phptuts.github.io/Tools/ledmatrix.html) bookmark it.

- Ex




