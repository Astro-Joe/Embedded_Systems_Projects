# Red & Green LED Blinking

## 📌 Overview
This is a fundamental GPIO project that demonstrates basic LED control through digitalWrite operations. The system alternates between turning red and green LEDs on and off at regular intervals, teaching core concepts of digital output and timing.

## 📚 Concepts Learned

### GPIO (General Purpose Input/Output)
- Digital pins can be configured as INPUT or OUTPUT
- digitalWrite() sets pin to HIGH (5V) or LOW (0V)

### Timing with delay()
- delay(milliseconds) pauses execution
- Useful for controlling blink rates and sequences
- Called 1000 times per second (1ms resolution)

### Build basic circuit with resistors and LEDs

## 🔧 Hardware Components

| Component | Model/Value | Quantity | Purpose |
|-----------|------------|----------|---------|
| Microcontroller | Arduino UNO | 1 | Main processor |
| Red LED | standard | 1 | Visual indicator |
| Green LED | standard | 1 | Visual indicator |
| Resistor | 220Ω | 2 | Current limiting |
| Breadboard | Standard | 1 | Prototyping |


## 🔌 Circuit Design

### Pin Configuration
- **Red LED:** Digital Pin 8 (through 220Ω resistor to GND)
- **Green LED:** Digital Pin 9 (through 220Ω resistor to GND)

### Circuit Diagram

<div align="center">
  <img src="./.assests/Screenshot%20From%202026-03-11%2017-18-21.png" alt="LED and I-O Simulation" width="300">
  <p><i>Figure 1: Wokwi Simulation of the Basic I/O Logic</i></p>
</div>

## 📝 Key Code Functions

```cpp
void setup()
- Initializes digital pins as OUTPUT
- Sets initial LED states

void loop()
- Alternates LED states
- Controls timing with delay()
```

## 🧪 Expected Behavior

**Normal Operation:**
1. Red LED turns ON (pin 8: HIGH)
2. Green LED is OFF (pin 9: LOW)
3. Wait 1 second
4. Red LED turns OFF (pin 8: LOW)
5. Green LED turns ON (pin 9: HIGH)
6. Wait 1 second
7. Repeat from step 1

**Visual Output:**
- Red LED blinks for 1 second
- Green LED blinks for 1 second
- Pattern repeats indefinitely

## 🧪 Testing & Results

### Test Checklist
- Red LED lights up when power applied
- Green LED lights up when power applied
- Alternating pattern is consistent
- No flickering or unstable behavior
- Timing is approximately 1 second per LED

## 📊 Performance Metrics
- **Current per LED:** ~15-20 mA (with 220Ω resistor)
- **Total Power Consumption:** ~50 mA at 5V
- **Cycle Time:** 2 seconds (1s RED + 1s GREEN)
- **Operating Voltage:** 5V

## 🚀 How to Use

### Hardware Setup
1. Connect Arduino to breadboard
2. Insert red LED with longer leg (anode) to pin 8 side
3. Insert green LED with longer leg (anode) to pin 9 side
4. Connect 220Ω resistors to LED cathodes
5. Connect all resistor cathode ends to GND
6. Connect USB cable to Arduino

### Software Upload
1. Open Arduino IDE
2. Copy code from `redLed_blink_greenLed.ino`
3. Connect Arduino via USB
4. Select correct Board (Arduino UNO) and COM Port
5. Click Upload
6. Observe LED blinking pattern


## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| LEDs don't light up | Check resistor polarity, LED orientation, pin connections |
| Only one LED works | Test LED with multimeter, check resistor values |
| Flickering/unstable | Verify stable power supply, check loose connections |
| Wrong timing | Ensure delay() values match desired intervals |


## Further possible additions

1. **Button Control** - Add pushbutton to control LED on/off
2. **PWM Brightness** - Use `analogWrite()` for LED dimming
3. **Multiple LEDs** - Create patterns with 4+ LEDs
4. **Sensor Input** - Control LED based on sensor readings
5. **Timing Library** - Replace delay() with non-blocking timing for better control

## 📋 Difficulty Level
**Beginner** | **Time to Complete:** 15 minutes 

## 📝 Version History
- v1.0 (27-10-2025) - Initial project creation

---
