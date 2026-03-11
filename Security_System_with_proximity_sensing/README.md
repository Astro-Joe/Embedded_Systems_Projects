# Security System with Proximity Sensing

## 📌 Overview
This project implements a security system that uses an HC-SR04 ultrasonic sensor or proximity detection and integrates user authentication via a keypad,
time keeping via a real-time clock (RTC), and output display on an LCD. 
When a user approaches within a specified distance, the system activates, prompting for PIN input and logging events with accurate timestamps.

## 🎯 Learning Objectives
- Integrate multiple sensors (ultrasonic, RTC) and output devices (LCD, LED)
- Implement user authentication with a keypad and secure PIN handling
- Master real-time event logging and display management
- Configure and control hardware components in embedded C++
- Develop robust user interface for embedded systems

## 📚 Concepts Learned

- Embedded C++ control of multiple peripherals
- Sensor integration (distance sensing, real-time clock)
- User authentication & secure PIN handling
- Hardware-software debugging and troubleshooting
- Robust user interface and feedback

## 🔧 Hardware Components

| Component             | Model/Value             | Quantity | Purpose                         |
|-----------------------|------------------------|----------|----------------------------------|
| Microcontroller       | Arduino UNO            | 1        | Main processor                   |
| Ultrasonic Sensor     | HC-SR04                | 1        | Proximity detection              |
| Keypad                | 4x4 Matrix             | 1        | User input (PIN/command)         |
| LCD Display           | 16x2 Character LCD     | 1        | Visual output                    |
| RTC Module            | DS3231                 | 1        | Real-time clock/timestamp        |
| Status LED            |5mm LED (A5 pin)        | 1        | RTC status or alarm indication   |
| Potentiometer         | 10kΩ                   | 1        | LCD contrast adjustment          |
| Resistor              | 220Ω                   | 1        | LCD backlight current limiting   |
| Breadboard            | Standard               | 1        | Prototyping                      |
| USB Cable             | USB A-B                | 1        | Power & upload                   |

## 🔌 Schematic

<div align="center">
  <img src="./.assets/Screenshot%20From%202026-03-11%2019-29-55.png" alt="Security System with proximity sensing Simulation" width="500">
  <p><i>Wokwi Simulation of the Security System with proximity sensing Simulation</i></p>
</div>

### Wokwi Simulation
*[https://wokwi.com/projects/445302505931600897]*

### Physical Implementation

<div align="center">
  <img src="./.assets/Wed%2011%20Mar%202026%2019%3A46%3A15%20WAT.png" alt="Security System with Proximity Sensing" width="500">
  <p><i>Security System with Proximity Sensing</i></p>
</div>

### Major Pin Assignments

- **Ultrasonic Sensor**
  - TRIG: D8
  - ECHO: D9
- **LCD Display**
  - RS: D2
  - E:  D3
  - D4: D4
  - D5: D5
  - D6: D6
  - D7: D7
  - Backlight: A0
  - Contrast: V0 (via 10kΩ potentiometer)
- **Keypad**
  - Rows: A1, A2, A3, A4
  - Columns: D13, D10, D11, D12
- **RTC Module**
  - Connected via I2C (SDA, SCL pins)
- **RTC Warning LED**:
  - Cathode: A5
  - Anode: +VCC


## 📝 Code Features & Flow

### Libraries Used

```cpp
#include <Wire.h>
#include <SPI.h>
#include <RTClib.h>
#include <Keypad.h>
#include <LiquidCrystal.h>
#include <HCSR04.h>
```

### Key Functions & Structure

- **Hardware Initialization**
  - LCD, Keypad, RTC, Ultrasonic sensor, Status LED
- **Proximity Detection**
  - Ultrasonic triggers LCD and unlock process when distance is in range
- **Menu System**
  - Option menu displayed; can add new password or login with PIN
- **Authentication**
  - PIN creation and validation; handles user input
- **RTC Status**
  - LED displays if RTC has initialized successfully; logs time, signals error
- **Dynamic Feedback**
  - LCD provides menu options, prompts, feedback, and result messages
- **Escape/Recovery**
  - Keypad can interrupt process or navigate menu

### Example: Main Menu Logic

```cpp
void option_menu() {
  if (!rtc.begin()) {
    digitalWrite(rtc_warning_LED, LOW); // RTC Fail
  } else {
    digitalWrite(rtc_warning_LED, HIGH); // RTC OK
  }
  lcd.setCursor(0, 0); lcd.print("Press a number");
  lcd.setCursor(0, 1); lcd.print("to select      ");
  delay(2000); lcd.clear();
  lcd.setCursor(0, 0); lcd.print("1. New Password");
  delay(1000); lcd.setCursor(0, 1); lcd.print("2. Login");
}
```

### Proximity Handling

```cpp
void loop() {
  distance = hc.dist();
  if (distance <= 45.0 && distance > 6.0) {
    lcd.display(); digitalWrite(lcd_backlight, BACKLIGHT_ON_LEVEL);
  } else {
    lcd.noDisplay(); digitalWrite(lcd_backlight, BACKLIGHT_OFF_LEVEL);
  }
  // Keypad input for PIN management
  char key = keypad.getKey();
  if (key) {
    if (key == '1') promptInput("New PIN: ");
    else if (key == '2') loginInput("Enter your PIN: ");
    else option_menu();
  }
}
```
### System Initialization Animation
When the device powers on or resets, a loading animation is displayed on the LCD to indicate the system is initializing. 
This provides visual feedback and improves user experience.

```cpp
void system_config(){
  display(F("System Init"));
  lcd.setCursor(0, 1);
  lcd.print(F("Press 0 to skip"));

  if (loading_animation(11, 0)) {
    return; // Allows skipping with keypad
  }
  lcd.clear();

  // RTC Initialization also includes animation
  display(F("RTC Init"));
  lcd.setCursor(0, 1);
  lcd.print(F("Press 0 to skip"));
  if (loading_animation(8, 0)) {
    return;
  }
  lcd.clear();
}
```

## Expected Behavior

- **User approaches system (within 6–45cm):** LCD powers on, menu displayed
- **Selects "New Password" or "Login":** Keypad used for input; feedback on LCD
- **RTC module checks:** Status LED turns ON if RTC present; OFF if not
- **Invalid actions:** LCD shows error messages and prompts for retry

## Testing & Results

- LCD responds to proximity sensor
- Keypad allows PIN creation & login
- RTC module status indicated via LED
- Menu and feedback system works; responds to user actions
- Robust error handling (RTC not connected, wrong PIN, etc.)

## Troubleshooting

| Problem                   | Solution                           |
|---------------------------|------------------------------------|
| LCD not responding        | Check backlight, pin connections   |
| RTC warning LED OFF       | RTC module not detected, check I2C |
| Keypad input faulty       | Verify row/column wiring           |
| Ultrasonic not detected   | Check sensor wiring/power           |
| PIN not accepted          | Check correct PIN length, retry     |

## 🚀 Future additions 

- Add SD card logging of events (time, distance, user actions)
- Add buzzer/alarm for failed authentication
- Expand menu for admin/user roles
- Integrate wireless (Bluetooth/WiFi) for remote notifications

## References

- [HC-SR04 Datasheet](https://cdn.sparkfun.com/datasheets/Sensors/Ultrasonic/HCSR04.pdf)
- [Keypad Library Reference](https://playground.arduino.cc/Code/Keypad/)
- [RTClib Reference](https://github.com/adafruit/RTClib)
- [LiquidCrystal Library](https://www.arduino.cc/en/Reference/LiquidCrystal)

## Project Specifications

| Specification        | Value       |
|----------------------|------------|
| Difficulty Level     | Intermediate–Advanced |
| Time to Complete     | 1.5 weeks |
| Components           | 5+          |
| Wiring Complexity    | High (20+ connections) |
| Code Complexity      | Advanced (multi-module) |

## 📝 Version History

- v1.0 (29-10-2025) 
---

This project demonstrates the ability to build production-level embedded systems, integrating multiple sensors, secure input methods, error handling, 
and clear user interaction. It also shows experience in hardware-software integration, modular code, and systematic testing/documentation.
