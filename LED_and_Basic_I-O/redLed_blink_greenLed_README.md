# Red & Green LED Blinking

## 📌 Overview
This is a fundamental GPIO project that demonstrates basic LED control through digitalWrite operations. The system alternates between turning red and green LEDs on and off at regular intervals, teaching core concepts of digital output and timing.

## 🎯 Learning Objectives
- ✅ Understand GPIO (General Purpose Input/Output) pins
- ✅ Control digital outputs with `digitalWrite()`
- ��� Implement timing with `delay()` function
- ✅ Work with active HIGH/LOW logic
- ✅ Build basic circuit with resistors and LEDs

## 🔧 Hardware Components

| Component | Model/Value | Quantity | Purpose |
|-----------|------------|----------|---------|
| Microcontroller | Arduino UNO | 1 | Main processor |
| Red LED | 5mm standard | 1 | Visual indicator |
| Green LED | 5mm standard | 1 | Visual indicator |
| Resistor | 220Ω | 2 | Current limiting |
| Breadboard | Standard | 1 | Prototyping |
| Jumper Wires | Various | 6+ | Connections |

## 🔌 Circuit Design

### Pin Configuration
- **Red LED:** Digital Pin 8 (through 220Ω resistor to GND)
- **Green LED:** Digital Pin 9 (through 220Ω resistor to GND)

### Circuit Diagram
```
Arduino Pin 8 ---[220Ω]---[RED LED]---GND
Arduino Pin 9 ---[220Ω]---[GREEN LED]---GND
Arduino 5V ---- Breadboard Power Rail
Arduino GND ---- Breadboard Ground Rail
```

### Wokwi Simulation
[View Simulation on Wokwi](https://wokwi.com/projects/[your-project-id])

## 💾 Code Structure

```
redLed_blink_greenLed/
├── redLed_blink_greenLed.ino    # Main program
├── README.md                     # This file
└── circuit_diagram.png           # Schematic image
```

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
- ✅ Red LED lights up when power applied
- ✅ Green LED lights up when power applied
- ✅ Alternating pattern is consistent
- ✅ No flickering or unstable behavior
- ✅ Timing is approximately 1 second per LED

### Test Photo
![LED Blinking Demo](./photos/led_demo.jpg)

## 📊 Performance Metrics
- **Current per LED:** ~15-20 mA (with 220Ω resistor)
- **Total Power Consumption:** ~50 mA @ 5V
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

### Code Modification Examples
```cpp
// Speed up the blinking (500ms each)
delay(500);

// Slower blinking (2 seconds each)
delay(2000);

// Sequence 3 LEDs
digitalWrite(ledPin1, HIGH); delay(500);
digitalWrite(ledPin1, LOW); 
digitalWrite(ledPin2, HIGH); delay(500);
digitalWrite(ledPin2, LOW);
// ... and so on
```

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| LEDs don't light up | Check resistor polarity, LED orientation, pin connections |
| Only one LED works | Test LED with multimeter, check resistor values |
| Flickering/unstable | Verify stable power supply, check loose connections |
| Wrong timing | Ensure delay() values match desired intervals |

## 📚 Concepts Learned

### GPIO (General Purpose Input/Output)
- Digital pins can be configured as INPUT or OUTPUT
- digitalWrite() sets pin to HIGH (5V) or LOW (0V)

### Current Limiting
- LEDs require resistors to prevent burnout
- Resistor value = (Voltage - LED Voltage Drop) / Desired Current
- 220Ω resistor limits current to ~15-20 mA

### Timing with delay()
- delay(milliseconds) pauses execution
- Useful for controlling blink rates and sequences
- Called 1000 times per second (1ms resolution)

## 🚀 Next Steps & Enhancements

1. **Button Control** - Add pushbutton to control LED on/off
2. **PWM Brightness** - Use `analogWrite()` for LED dimming
3. **Multiple LEDs** - Create patterns with 4+ LEDs
4. **Sensor Input** - Control LED based on sensor readings
5. **Timing Library** - Replace delay() with non-blocking timing for better control

## 📖 References

- [Arduino digitalWrite() Reference](https://www.arduino.cc/reference/en/language/functions/digital-io/digitalwrite/)
- [Arduino delay() Reference](https://www.arduino.cc/reference/en/language/functions/time/delay/)
- [LED Circuit Design Guide](https://learn.adafruit.com/all-about-leds)
- [Arduino Pin Modes](https://www.arduino.cc/en/Tutorial/Foundations/DigitalPins)

## 📋 Difficulty Level
⭐ **Beginner** | **Time to Complete:** 15 minutes | **Estimated Cost:** $3-5

## 📝 Version History
- v1.0 (2026-03-11) - Initial project creation

---