# DC Motor Control with H-Bridge and Arduino

This project shows how to control a DC motor using an H-Bridge (L293D) with an Arduino. 

https://github.com/user-attachments/assets/fb206ab3-4657-4a08-9efd-ec0be253ecba

## Components

- Arduino Uno
- L293D H-Bridge
- DC Motor
- 9V Battery


## Circuit Connections

Pin connections between the Arduino, H-Bridge, and other components:

| Component       | Arduino Pin | H-Bridge Pin | Description                    |
|-----------------|-------------|--------------|--------------------------------|
| Enable 1,2      | 9           | 1            | PWM control for motor speed    |
| Input 1         | 7           | 2            | Controls motor direction       |
| Output 1        |             | 3            | Connects to Motor Terminal 1   |
| Ground          | GND         | 4, 5         |                                |
| Output 2        |             | 6            | Connects to Motor Terminal 2   |
| Input 2         | 8           | 7            | Controls motor direction       |
| Motor Power     |             | 8            | Connects to the 9V Battery     |
| Logic Power     | 5V          | 16           | Powers H-Bridge logic          |



- The motor runs in one direction, stops, and then runs in the opposite direction for the same amount of time

```cpp
int enablePin = 9;  // enable Pin 1,2
int motorPin1 = 7;  // input 1
int motorPin2 = 8;  // input 2

void setup() {
  pinMode(enablePin, OUTPUT);
  pinMode(motorPin1, OUTPUT);
  pinMode(motorPin2, OUTPUT);

  // stop the motor
  digitalWrite(motorPin1, LOW);
  digitalWrite(motorPin2, LOW);
  analogWrite(enablePin, 255);
}

void loop() {
  // run motor in one direction for 5 secs then stop for 5 secs
  digitalWrite(motorPin1, HIGH);
  digitalWrite(motorPin2, LOW);
  delay(5000); 
  digitalWrite(motorPin1, LOW);
  digitalWrite(motorPin2, LOW);
  delay(5000); 

  //opposite direction
  digitalWrite(motorPin1, LOW);
  digitalWrite(motorPin2, HIGH);
  delay(5000); 
  digitalWrite(motorPin1, LOW);
  digitalWrite(motorPin2, LOW);
  delay(5000); 
}
