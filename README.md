# 🏠 Smart Home Automation System

An advanced IoT-based smart home prototype using ESP8266 NodeMCU and Arduino Uno with real-time web monitoring and control.

## 📋 Features

### 🎛️ Control Systems
- **Relay Control**: Manual and motion-activated modes
- **LED Control**: Web-based on/off control
- **Servo Motor**: Manual positioning (0°, 90°, 180°) or automatic light-dependent mode
- **Smart Fan**: Three operational modes with PWM speed control
  - Manual mode (web control)
  - Temperature-based automatic control
  - Gas sensor-based automatic control

### 📊 Sensors
- **DHT22**: Temperature and humidity monitoring
- **PIR Motion**: Movement detection
- **Flame Sensor**: Fire detection with buzzer alarm
- **LDR**: Light level measurement
- **MQ-2**: Gas leak detection
- **MFRC522 RFID**: Card reader for access control

### 🌐 Web Interface
- Real-time sensor data updates (every 2 seconds)
- Responsive design with modern UI
- Remote control via WiFi
- Device status monitoring

## 🔧 Hardware Requirements

### ESP8266 NodeMCU Components:
- ESP8266 NodeMCU board
- DHT22 Temperature/Humidity sensor
- PIR Motion sensor
- Flame sensor
- LDR (Light Dependent Resistor)
- SG90 Servo motor
- Relay module
- LED
- Buzzer
- Resistors (10kΩ, 220Ω)

### Arduino Uno Components:
- Arduino Uno R3
- MFRC522 RFID reader module
- MQ-2 Gas sensor module
- DC Fan motor
- L293D Motor driver (or BC547 transistor)
- Resistors (1kΩ, 2kΩ for voltage divider)

## 📦 Software Requirements

### Arduino IDE Libraries:
**For ESP8266:**
- ESP8266WiFi (built-in)
- ESP8266WebServer (built-in)
- DHT sensor library (Adafruit)
- Servo (built-in)

**For Arduino Uno:**
- MFRC522 (RFID library)
- SPI (built-in)

### Installation:
```
Arduino IDE → Tools → Manage Libraries → Search and install required libraries
```

## 🔌 Wiring Connections

### ESP8266 NodeMCU Pinout:
| Component | ESP8266 Pin | GPIO |
|-----------|-------------|------|
| DHT22 Data | D2 | GPIO4 |
| PIR Motion | D5 | GPIO14 |
| Flame Sensor | D7 | GPIO12 |
| Buzzer | D8 | GPIO15 |
| Relay | D0 | GPIO16 |
| LED | D1 | GPIO5 |
| Servo | D4 | GPIO2 |
| LDR | A0 | ADC0 |

### Arduino Uno Pinout:
| Component | Arduino Pin |
|-----------|-------------|
| RFID RST | Pin 9 |
| RFID SS | Pin 10 |
| RFID MOSI | Pin 11 |
| RFID MISO | Pin 12 |
| RFID SCK | Pin 13 |
| MQ-2 Gas Sensor | A0 |
| Fan Motor (PWM) | Pin 3 |

### Serial Communication:
```
ESP8266 TX → Arduino RX (Pin 0)
ESP8266 RX → Voltage Divider → Arduino TX (Pin 1)
ESP8266 GND ⟷ Arduino GND (COMMON GROUND!)
```

### ⚠️ Voltage Divider (Important!):
```
Arduino TX (5V) → 1kΩ resistor → ESP8266 RX (3.3V)
                                ↓
                            2kΩ resistor
                                ↓
                               GND
```

## 🚀 Setup Instructions

### 1. Hardware Assembly
- Connect all components according to the wiring diagram
- Ensure common ground between ESP8266 and Arduino
- Use voltage divider for serial communication
- Connect motor driver for fan control

### 2. Software Configuration
**ESP8266 Code:**
```cpp
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
```

**Upload:**
- Upload ESP8266 code to NodeMCU
- Upload Arduino code to Uno
- Open Serial Monitor to see IP address

### 3. Access Web Interface
- Connect to the same WiFi network
- Open browser and navigate to ESP8266's IP address
- Example: `http://192.168.1.100`

## 🎯 Operating Modes

### Fan Control Modes:
1. **Manual Mode**: Direct on/off control from web interface
2. **Temperature Mode**: Automatic control based on temperature
   - < 28°C: OFF
   - 28-30°C: Low speed (PWM 100)
   - 30-33°C: Medium speed (PWM 180)
   - > 33°C: High speed (PWM 255)
3. **Gas Sensor Mode**: Automatic control based on gas level
   - < 400: OFF
   - 400-500: Low speed
   - 500-600: Medium speed
   - > 600: High speed

### Relay Modes:
- **Remote Control**: Manual on/off via web interface
- **Motion Mode**: Automatic activation on motion detection

### Servo Modes:
- **Remote Control**: Manual positioning (0°, 90°, 180°)
- **Light-Dependent**: Automatic positioning based on LDR reading

## 📡 Communication Protocol

### Arduino → ESP8266:
```
Format: G:XXX,R:CARDID,F:X
G: Gas level (0-1023)
R: RFID card ID (hex)
F: Fan state (0/1)
```

### ESP8266 → Arduino:
```
Format: M:X,F:X,T:XX.X
M: Fan mode (0/1/2)
F: Fan command (0/1)
T: Temperature value
```

## 🔍 Testing

1. **Power Up**: Connect both boards to USB power
2. **Serial Monitor**: Verify WiFi connection and IP address
3. **Web Access**: Open IP address in browser
4. **Sensor Test**: Check all sensor readings update
5. **Control Test**: Test all buttons and mode switches
6. **RFID Test**: Scan a card and verify on web interface
7. **Fan Modes**: Test all three fan operation modes

## ⚡ Safety Notes

- ⚠️ Never connect 5V to ESP8266 GPIO pins
- ⚠️ Use voltage divider for ESP8266 RX pin
- ⚠️ RFID module requires 3.3V (not 5V!)
- ⚠️ Always use motor driver for fan (never direct connection)
- ⚠️ Ensure common ground between all components
- ⚠️ Use external power for servo and fan motors

## 🐛 Troubleshooting

**WiFi Not Connecting:**
- Check SSID and password
- Ensure 2.4GHz WiFi (ESP8266 doesn't support 5GHz)

**No Serial Communication:**
- Verify TX/RX connections
- Check voltage divider circuit
- Ensure common ground

**RFID Not Working:**
- Verify SPI connections
- Check 3.3V power supply
- Ensure proper SS pin (Pin 10)

**Fan Not Running:**
- Check motor driver connections
- Verify PWM pin connection
- Test with external power supply

## 📸 Screenshots

The web interface includes:
- Real-time sensor monitoring
- Device control buttons
- Mode switching options
- Status indicators
- RFID card display
- Gas level monitoring

## 📄 License

This project is open source and available for educational purposes.

## 👥 Contributing

Feel free to fork this project and submit pull requests for improvements.

## 📧 Contact

For questions and support, please open an issue in the repository.

---
