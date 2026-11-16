Yes. I’d structure the page like this, and use names like `motor1Pin1` rather than `D8`.

# Motor Speed Controller

Control two DC motors using an Arduino, an L298N motor driver, and a webpage connected through `navigator.serial`.

## Wiring Table

| Arduino Pin | L298N Connection | Purpose           |
| ----------- | ---------------- | ----------------- |
| 9           | ENA              | Motor 1 speed     |
| 8           | IN1              | Motor 1 direction |
| 7           | IN2              | Motor 1 direction |
| 3           | ENB              | Motor 2 speed     |
| 5           | IN3              | Motor 2 direction |
| 4           | IN4              | Motor 2 direction |
| GND         | GND              | Common ground     |

> **Important:** Remove the ENA and ENB jumpers from the L298N if they are installed. Pins 9 and 3 need to control ENA and ENB with PWM.

## Code

```cpp
typedef enum {
  CLOCKWISE = 0,
  ANTI_CLOCKWISE = 1,
  STOP = -1
} Direction;

// Motor 1
const int motor1Pin1 = 8;
const int motor1Pin2 = 7;
const int enablePin1 = 9;

// Motor 2
const int motor2Pin1 = 5;
const int motor2Pin2 = 4;
const int enablePin2 = 3;

void moveMotor(int motor, int speed, Direction direction) {
  int enablePin = motor == 1 ? enablePin1 : enablePin2;
  int pin1 = motor == 1 ? motor1Pin1 : motor2Pin1;
  int pin2 = motor == 1 ? motor1Pin2 : motor2Pin2;

  speed = constrain(speed, 0, 255);

  switch (direction) {
    case CLOCKWISE:
      digitalWrite(pin1, HIGH);
      digitalWrite(pin2, LOW);
      analogWrite(enablePin, speed);
      break;

    case ANTI_CLOCKWISE:
      digitalWrite(pin1, LOW);
      digitalWrite(pin2, HIGH);
      analogWrite(enablePin, speed);
      break;

    case STOP:
      digitalWrite(pin1, LOW);
      digitalWrite(pin2, LOW);
      analogWrite(enablePin, 0);
      break;
  }
}

void setup() {
  Serial.begin(115200);

  pinMode(motor1Pin1, OUTPUT);
  pinMode(motor1Pin2, OUTPUT);
  pinMode(enablePin1, OUTPUT);

  pinMode(motor2Pin1, OUTPUT);
  pinMode(motor2Pin2, OUTPUT);
  pinMode(enablePin2, OUTPUT);

  moveMotor(1, 0, STOP);
  moveMotor(2, 0, STOP);

  Serial.println("READY");
}

void loop() {
  if (Serial.available()) {
    String command = Serial.readStringUntil('\n');
    command.trim();

    int firstColon = command.indexOf(':');
    int secondColon = command.indexOf(':', firstColon + 1);

    if (firstColon == -1 || secondColon == -1) {
      return;
    }

    String motorText = command.substring(0, firstColon);
    String speedText = command.substring(firstColon + 1, secondColon);
    String directionText = command.substring(secondColon + 1);

    int motor = motorText.substring(1).toInt();
    int speed = speedText.toInt();

    Direction direction = STOP;

    if (directionText == "F") {
      direction = CLOCKWISE;
    } else if (directionText == "R") {
      direction = ANTI_CLOCKWISE;
    } else if (directionText == "S") {
      direction = STOP;
    }

    if (motor == 1 || motor == 2) {
      moveMotor(motor, speed, direction);
    }
  }
}
```

The webpage sends commands over `navigator.serial` in this format:

```text
M1:150:F
```

That means:

* `M1` = Motor 1
* `150` = Speed from 0–255
* `F` = Forward

Other examples:

```text
M2:200:R
M1:100:F
M2:0:S
```

## Memories

### Motor Speed

Motor speed is controlled using PWM.

```cpp
analogWrite(enablePin, speed);
```

The speed can be between:

```text
0   = stopped
255 = full speed
```

Try different values and see what happens:

```cpp
50
100
150
200
255
```

### Motor Direction

The two direction pins determine which way the motor spins.

| Pin 1 | Pin 2 | Motor          |
| ----- | ----- | -------------- |
| HIGH  | LOW   | Clockwise      |
| LOW   | HIGH  | Anti-clockwise |
| LOW   | LOW   | Stop           |

### Serial Commands

The webpage talks to the Arduino over USB.

For example:

```text
M1:175:F
```

The Arduino reads the command and turns Motor 1 forward at speed 175.

### Things to Try

Change the motor speeds and observe what happens. Try making:

* One motor faster than the other
* Both motors the same speed
* One motor go forward and the other backward
* The motors run very slowly
* The motors suddenly stop
