# Ultrasonic Distance Measurement

## 📌 Overview
This project uses the HC-SR04 ultrasonic distance sensor to measure distance to nearby objects. The sensor works by sending ultrasonic sound waves and measuring the echo return time, calculating distance based on the speed of sound.

## 📚 Concepts Learned

### Ultrasonic Sensing
- **Transducer:** Converts electrical signal to sound and vice versa
- **40 kHz:** Frequency above human hearing range (20 Hz - 20 kHz)
- **Echo Method:** Measures return time of reflected sound

### Timing Measurement
- **pulseIn():** Measures duration of pulse in microseconds
- **Timeout:** Function waits max 1 second for echo response
- **Blocking:** Code pauses until measurement complete

## 🔧 Hardware Components

| Component | Model/Value | Quantity | Purpose |
|-----------|------------|----------|---------|
| Microcontroller | Arduino UNO | 1 | Main processor |
| Ultrasonic Sensor | HC-SR04 | 1 | Distance measurement |
| LCD Display | 16x2 Character LCD | 1 | Visual output |
| Potentiometer | 10kΩ | 1 | LCD contrast adjustment |
| Resistor | 220Ω | 1 | Current limiting (optional for backlight) |
| Breadboard | Standard | 1 | Prototyping |
| USB Cable | USB A-B | 1 | Power & communication |

## 🔌 Circuit Design

### HC-SR04 Pin Configuration
```
VCC  -------- Arduino 5V
GND  -------- Arduino GND
TRIG -------- Arduino Pin 8  (Trigger pulse)
ECHO -------- Arduino Pin 9  (Echo pulse)
```
### 16x2 LCD Display Pin Configuration
```
LCD Pin    Arduino Pin    Purpose
---        -----------    -------
1 (GND)    GND            Ground
2 (VCC)    5V             Power supply
3 (V0)     10kΩ Pot       Contrast control
4 (RS)     Pin 7          Register Select
5 (RW)     GND            Read/Write (write mode)
6 (E)      Pin 6          Enable
7-10       Not used       Data bits D0-D3 (not in 4-bit mode)
11 (D4)    Pin 5          Data bit 4
12 (D5)    Pin 4          Data bit 5
13 (D6)    Pin 3          Data bit 6
14 (D7)    Pin 2          Data bit 7
15 (A)     5V (via 220Ω)  Backlight anode
16 (K)     GND            Backlight cathode
```

## 📝 Key Code Functions

```cpp
void setup()
- Sets TRIG pin as OUTPUT
- Sets ECHO pin as INPUT
- Initializes Serial at 9600 baud

void loop()
- Sends 10µs trigger pulse
- Measures echo pulse width
- Converts to distance
- Prints results
```

## 🧪 Expected Behavior

**Serial Monitor Output:**
```
Distance: 15.2 cm
Distance: 15.1 cm
Distance: 45.3 cm
Distance: 45.2 cm
```

**Physical Behavior:**
1. Sensor emits 40 kHz ultrasonic burst
2. Sound travels to object and reflects back
3. Sensor detects return echo
4. Arduino calculates: Distance = (Echo Time × Sound Speed) / 2

## 🧪 Testing & Results

### Test Checklist
- Sensor detects objects up to 400 cm away
- Readings update at least 10 times per second
- Accuracy within ±1 cm
- No false readings at maximum range
- Stable readings with hand objects

### Distance Range Testing
| Test Object | Expected Distance | Measured Distance | Pass/Fail |
|-------------|------------------|-----------------|-----------|
| Hand at 5cm | 5 cm | 5.1 cm | ✅ |
| Hand at 20cm | 20 cm | 20.3 cm | ✅ |
| Wall at 50cm | 50 cm | 49.8 cm | ✅ |
| Wall at 100cm | 100 cm | 100.5 cm | ✅ |

## 📊 Performance Metrics
- **Measurement Range:** 2 cm - 400 cm
- **Accuracy:** ±1-2 cm (typical)
- **Frequency:** 40 kHz (ultrasonic)
- **Update Rate:** 10-20 Hz (measurements/sec)
- **Supply Voltage:** 5V
- **Current Consumption:** 15 mA (average)

## 🚀 How to Use

### Hardware Setup
1. Connect HC-SR04:
   - VCC to Arduino 5V
   - GND to Arduino GND
   - TRIG to Digital Pin 8
   - ECHO to Digital Pin 9
2. Use USB cable to power Arduino
3. Open Serial Monitor (9600 baud)

### Software Upload
1. Copy code to Arduino IDE
2. Verify Pin numbers match (TRIG=8, ECHO=9)
3. Click Upload
4. Observe distance readings

### Code Modification Examples
```cpp
// Change pin assignments
const int trigPin = 7;  // Change from 8
const int echoPin = 6;  // Change from 9

// Filter out noisy readings
if (distance > 2 && distance < 400) {
  Serial.println(distance);
}
```

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| No readings or -1 cm | Check ECHO pin connection, verify pin assignments |
| Constant maximum range | Sensor not detecting echoes; check lens is clean |
| Noisy/fluctuating readings | Add averaging filter or wait time between measurements |
| Readings always same | Check if code loops correctly, verify Serial Monitor open |
| Sensor gets hot | Normal; 5V current is low. Check if excessive current supply |

## 🚀 Further possible additions

1. **Alarm System** - Sound buzzer when object too close
2. **LCD Display** - Show distance on 16x2 LCD
3. **LED Indicator** - Different colors for distance ranges
4. **Data Logging** - Store measurements to SD card with timestamps
5. **Multiple Sensors** - Create motion detector with 4 directions
6. **Obstacle Avoidance** - Use with motors for robot

## 📋 Difficulty Level
**Intermediate** | **Time to Complete:** 30 minutes 

## 📝 Version History
- v1.0 (27-10-25) - Initial project creation

---
