# -IoT-Smart-Irrigation-System
Arduino-based Smart Automatic Irrigation System that monitors soil moisture and automatically controls a water pump using a relay module for efficient irrigation and water conservation.

# Smart Automatic Irrigation System

## Overview

The Smart Automatic Irrigation System is an Arduino-based project designed to automate the irrigation process by continuously monitoring soil moisture levels. When the soil becomes dry, the Arduino activates a water pump through a relay module to irrigate the plants. Once the soil reaches the predefined moisture level, the pump is automatically switched off.

This system helps conserve water while ensuring plants receive sufficient moisture without manual intervention.

---



<img width="512" height="279" alt="image" src="https://github.com/user-attachments/assets/03293aa9-f57f-47e1-9f0d-baa77001c583" />

## Features

- Automatic soil moisture monitoring
- Automatic water pump control
- Real-time moisture measurement
- Relay-based pump switching
- Water-saving irrigation
- LED status indicators
- Expandable for IoT monitoring

---

## Components Used

- Arduino Uno
- Soil Moisture Sensor
- 5V Relay Module
- DC Water Pump
- Water Pipe
- External Power Supply
- Red LED
- Green LED
- Jumper Wires
- Breadboard

---

## Software Used

- Arduino IDE

---

## Working Principle

The soil moisture sensor continuously measures the moisture content of the soil and sends analog data to the Arduino Uno.

If the soil moisture falls below the predefined threshold, the Arduino energizes the relay module, switching on the water pump. Water is supplied to the soil until the moisture level reaches the desired value.

Once the target moisture level is achieved, the Arduino deactivates the relay, turning off the water pump automatically.

This fully automated cycle ensures efficient irrigation while preventing overwatering.

---

## Applications

- Smart Agriculture
- Home Gardening
- Greenhouses
- Plant Irrigation
- Precision Farming
- Water Conservation Systems

---

## Future Improvements

- Wi-Fi Monitoring (ESP8266/ESP32)
- Mobile Application Control
- LCD/OLED Display
- Weather Forecast Integration
- Solar Powered Irrigation
- Multiple Soil Sensors
- Cloud Data Logging
- AI-Based Irrigation Scheduling

---
-------*Code*------
/*
  Smart Automatic Irrigation System
  Author: Muhammad Muzammal Ali

  Components:
  - Arduino Uno
  - Soil Moisture Sensor
  - 5V Relay Module
  - DC Water Pump
  - Red LED
  - Green LED
*/

const int moisturePin = A0;
const int relayPin = 7;
const int redLED = 8;
const int greenLED = 9;

// Moisture thresholds
const int dryLevel = 30;   // Pump turns ON below this
const int wetLevel = 60;   // Pump turns OFF above this

bool pumpRunning = false;

void setup() {

  Serial.begin(9600);

  pinMode(relayPin, OUTPUT);
  pinMode(redLED, OUTPUT);
  pinMode(greenLED, OUTPUT);

  // Relay OFF (Active LOW Relay)
  digitalWrite(relayPin, HIGH);

  digitalWrite(redLED, LOW);
  digitalWrite(greenLED, HIGH);

  Serial.println("===== SMART IRRIGATION SYSTEM =====");
}

void loop() {

  int sensorValue = analogRead(moisturePin);

  // Convert sensor value to moisture percentage
  int moisture = map(sensorValue, 1023, 0, 0, 100);

  // Keep values between 0 and 100
  moisture = constrain(moisture, 0, 100);

  Serial.print("Soil Moisture: ");
  Serial.print(moisture);
  Serial.println("%");

  // Soil is dry
  if (moisture < dryLevel && !pumpRunning) {

    Serial.println("Status: Soil Dry");
    Serial.println("Pump: ON");

    digitalWrite(relayPin, LOW);     // Relay ON
    digitalWrite(redLED, HIGH);
    digitalWrite(greenLED, LOW);

    pumpRunning = true;
  }

  // Soil has enough moisture
  if (moisture >= wetLevel && pumpRunning) {

    Serial.println("Status: Moisture Sufficient");
    Serial.println("Pump: OFF");

    digitalWrite(relayPin, HIGH);    // Relay OFF
    digitalWrite(redLED, LOW);
    digitalWrite(greenLED, HIGH);

    pumpRunning = false;
  }

  Serial.println("--------------------------");

  delay(1000);
}



## Author

Muhammad Muzammal Ali
