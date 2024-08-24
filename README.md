
# PC Steering Wheel with Arduino Uno and UnoJoy

![Project Demo](demo.gif)

This project demonstrates how to build a PC steering wheel using an Arduino Uno and the UnoJoy library. The steering wheel is designed to function as a USB game controller compatible with most PC games.

## Project Overview

This project involves the following key components:
- **Arduino Uno**: Acts as the main controller, interfacing with the steering wheel's buttons and potentiometers.
- **UnoJoy Library**: Converts the Arduino into a USB joystick, allowing it to be recognized by the computer as a game controller.

## Features

- **Analog Stick Support**: The steering wheel uses analog inputs for smooth control of the steering, throttle, and other functions.
- **Button Mapping**: 12 buttons are mapped to various functions, such as gear shifting, handbrake, and more.
- **Compact Design**: All necessary components are housed within a custom-printed enclosure.

## Hardware Requirements

- Arduino Uno
- Potentiometers for steering and pedals
- Push buttons for various controls
- Custom 3D-printed enclosure
- USB cable for connecting the Arduino to the PC

## Software Requirements

- Arduino IDE
- UnoJoy Library ([GitHub Repository](https://github.com/AlanChatham/UnoJoy))

## Wiring Diagram

(Insert wiring diagram here)

## Code Explanation

```cpp
#include "UnoJoy.h"

void setup(){
  setupPins();
  setupUnoJoy();
}

void loop(){
  // Always be getting fresh data
  dataForController_t controllerData = getControllerData();
  setControllerData(controllerData);
}

void setupPins(void){
  // Set all the digital pins as inputs
  // with the pull-up enabled, except for the 
  // two serial line pins
  for (int i = 2; i <= 12; i++){
    pinMode(i, INPUT);
    digitalWrite(i, HIGH);
  }
  pinMode(A4, INPUT);
  digitalWrite(A4, HIGH);
  pinMode(A5, INPUT);
  digitalWrite(A5, HIGH);
}

dataForController_t getControllerData(void){
  // Set up a place for our controller data
  dataForController_t controllerData = getBlankDataForController();

  // Button mappings
  controllerData.triangleOn = !digitalRead(2);
  controllerData.circleOn = !digitalRead(3);
  controllerData.squareOn = !digitalRead(4);
  controllerData.crossOn = !digitalRead(5);
  controllerData.dpadUpOn = !digitalRead(6);
  controllerData.dpadDownOn = !digitalRead(7);
  controllerData.dpadLeftOn = !digitalRead(8);
  controllerData.dpadRightOn = !digitalRead(9);
  controllerData.l1On = !digitalRead(10);
  controllerData.r1On = !digitalRead(11);
  controllerData.selectOn = !digitalRead(12);
  controllerData.startOn = !digitalRead(A4);
  controllerData.homeOn = !digitalRead(A5);

  // Analog stick mappings
  controllerData.leftStickX = (analogRead(A0) >> 2);
  controllerData.leftStickY = (analogRead(A1) >> 2);
  controllerData.rightStickX = (analogRead(A2) >> 2);
  controllerData.rightStickY = (analogRead(A3) >> 2);
  
  return controllerData;
}
```

## How to Build

1. **Assemble the Hardware**: Connect the potentiometers and buttons to the Arduino as per the wiring diagram.
2. **Upload the Code**: Use the Arduino IDE to upload the provided code to the Arduino Uno.
3. **Install UnoJoy**: Follow the instructions in the UnoJoy library to convert your Arduino into a USB game controller.
4. **Test and Calibrate**: Connect the Arduino to your PC and test the steering wheel in your favorite racing game.

## 3D Printing

The enclosure and components are designed to be 3D printed. You can find the STL files in the `3D_Models` folder of this repository.

## Contributions

Contributions are welcome! Please fork this repository and submit a pull request if you have any improvements or suggestions.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
