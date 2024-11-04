# Digital Circuit Energy Management Project

## Project Overview
This project focuses on developing key skills in digital integrated circuit management, specifically in interpreting datasheets, analyzing energy consumption, and implementing energy management strategies. Using an Arduino UNO R3 board, the project integrates various components, including sensors and output modules, to create a basic data acquisition and transmission system.

## Project Objectives
1. **Data Extraction from Datasheets**: Learn to interpret and use datasheet information to select and optimize electronic components.
2. **Energy Consumption Analysis**: Evaluate power consumption in different modes (idle and running) for efficient system design.
3. **Energy Management Strategy**: Implement strategies to reduce energy consumption in battery-powered applications.

## Components
- **Microcontroller**: ATmega328P (on Arduino UNO R3)
- **Light Sensor**: Photoresistor (GL5528)
- **Pulse Sensor**: Heart Rate Monitor
- **LEDs**: Green and Red LEDs for status indication
- **Buzzer**: Active buzzer for auditory alerts

## System Requirements
- **Supply Voltage**: 5V for the Arduino board
- **Clock Frequency**: 16 MHz (external quartz on the development board)

## System Power Consumption Estimate
- Pulse Sensor: 4 mA
- LEDs: 20 mA x 2 = 40 mA (when active)
- Buzzer: 30 mA
- Photoresistor: Negligible (under 1 mA)

### Total Maximum Power Consumption
- Total current: 75 mA
- Power at 5V: 375 mW

### Battery Requirements
- **Battery Type**: 1.2V, 2500mAh
- **Batteries Needed**: 5 batteries in series (5V total)
- **Operating Time Estimate**: ~33 hours with 2500mAh capacity

## Energy Management Strategies
- **Sleep Mode**: Configure ATmega328P to enter sleep mode between readings to save power.
- **Component Optimization**:
    - Use low-power LEDs.
    - Consider replacing the active buzzer with a piezo element to reduce energy consumption.

## Conclusion
This project highlights the practical aspects of digital circuit design, emphasizing energy efficiency and component compatibility.
By implementing energy management strategies, the system achieves a balance between performance and power consumption,
making it suitable for portable and battery-operated applications.

Below is the code to be uploaded to the Arduino board:

## Code Implementation

```cpp
// Define pins
const int buzzerPin = 11;
const int lightSensorPin = 12;
const int ledGreenPin = 13; // Green LED
const int ledRedPin = 10;   // Red LED

void setup() {
  // Initialize pins
  pinMode(buzzerPin, OUTPUT);
  pinMode(lightSensorPin, INPUT);
  pinMode(ledGreenPin, OUTPUT);
  pinMode(ledRedPin, OUTPUT);
  
  // Initialize serial monitor (for debugging)
  Serial.begin(9600);
}

void loop() {
  // Read the light sensor value
  int lightValue = digitalRead(lightSensorPin);
  
  // Check if it is light or dark
  if (lightValue == HIGH) {
    // It is light
    digitalWrite(buzzerPin, LOW);       // Deactivate buzzer
    digitalWrite(ledGreenPin, HIGH);    // Activate green LED
    digitalWrite(ledRedPin, LOW);       // Deactivate red LED
    Serial.println("It's dark!");
  } else {
    // It is dark
    digitalWrite(buzzerPin, HIGH);      // Activate buzzer
    digitalWrite(ledGreenPin, LOW);     // Deactivate green LED
    digitalWrite(ledRedPin, HIGH);      // Activate red LED
    Serial.println("It's light!");
  }
  
  // Wait for one second
  delay(1000);
}

