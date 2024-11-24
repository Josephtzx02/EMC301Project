# EMC301Project
EMC301 Project: Title 4 [Smart home automation using light, sound, and temperature sensors.]

Smart home automation system using **light**, **sound**, and **temperature sensors** with an Arduino 

---

### **1. List of Components Needed**
### **1. Sensors**
- **Light Sensor**: 
  - Photoresistor (LDR) or TSL2561 Digital Light Sensor.
- **Sound Sensor**: 
  - Microphone sound detection module (e.g., KY-038 or LM393).
- **Temperature and Humidity Sensor**: 
  - DHT11 or DHT22 (temperature and humidity).
  - Alternative: LM35 or DS18B20 for temperature only.

---

### **2. Actuators and Outputs**
- **LEDs**: 
  - For visual indicators or notifications.
- **Relay Module**: 
  - To control high-power devices like lights or fans.
- **Buzzer**: 
  - For sound alerts.
- **Servo Motor or DC Motor**: 
  - To control doors, windows, or other mechanical elements.

---

### **3. Microcontroller**
- **Arduino Board**: 
  - Arduino Uno, Mega, or Nano (depending on the number of sensors and outputs).

---

### **4. Communication Modules (Optional)**
- **Wi-Fi Module**: 
  - ESP8266 or ESP32 for remote monitoring and control.
- **Bluetooth Module**: 
  - HC-05 or HC-06 for local communication.

---

### **5. Power Supply**
- **Power Source**: 
  - 5V power adapter or USB connection.
- **Battery Backup (Optional)**: 
  - Rechargeable Li-ion or power bank for uninterrupted operation.

---

### **6. Connectors and Miscellaneous**
- **Jumper Wires**: 
  - For connecting components.
- **Breadboard**: 
  - For prototyping circuits.
- **Resistors and Capacitors**: 
  - To stabilize sensor readings and protect components.
- **Transistors**: 
  - If additional current amplification is needed for actuators.
- **Heat Shrink Tubes** or **Electrical Tape**: 
  - For insulation and safety.
- **Cables and Screw Terminals**: 
  - For reliable connections to power and appliances.

---

### **7. Software and Libraries**
- **Arduino IDE**: 
  - For programming the Arduino.
- **Sensor Libraries**: 
  - Libraries for DHT, LDR, or other specific sensors (downloadable via the Arduino Library Manager).

---

### **8. Optional Smart Integration**
- **Home Automation Frameworks**: 
  - Home Assistant or Blynk for mobile control.
- **IoT Cloud Platforms**: 
  - Thingspeak or Arduino IoT Cloud for remote monitoring.

---

### **Application Example**
1. **Light Control**: Use the LDR to turn on lights when it gets dark.
2. **Sound-based Alerts**: Use the sound sensor to detect claps or other noises and trigger actions.
3. **Temperature Management**: Use the temperature sensor to control fans or AC based on room temperature.

---

### **2. Circuit Diagram Explanation**
#### **Components & Connections:**
1. **Light Sensor (LDR):**
   - Connect one leg of the LDR to **5V** and the other to an analog pin (e.g., A0) with a **10kΩ resistor** in series to GND.

2. **Sound Sensor (KY-038):**
   - Connect the **DO pin** of the sound sensor to a digital pin (e.g., D2).
   - **VCC** and **GND** go to 5V and GND, respectively.

3. **Temperature and Humidity Sensor (DHT11 or DHT22):**
   - Connect the **signal pin** to a digital pin (e.g., D3).
   - Connect **VCC** and **GND** to 5V and GND.

4. **Relay Module (For controlling lights or fans):**
   - Connect the **input pin** of the relay to a digital pin (e.g., D4).
   - **VCC** and **GND** to Arduino's 5V and GND.

5. **LEDs (Indicators):**
   - Connect the positive terminal of the LED to a digital pin (e.g., D5) through a **220Ω resistor**.

6. **Buzzer:**
   - Connect the **positive terminal** to a digital pin (e.g., D6) and the other terminal to GND.

7. **Power:**
   - Use the USB connection or a 5V external power supply.

---

### **3. Functionality**
- **Light Control:**
  - The relay turns on when the light level drops below the threshold.
  - The LED indicates when the relay is active.

- **Sound Alert:**
  - When the sound sensor detects a noise above the threshold, the buzzer activates briefly.
 
  - Let’s design the **smart home automation system** using light, sound, and temperature sensors with Arduino. Below, you'll find the circuit diagram explanation and code examples for each functionality.

- **Temperature Monitoring:**
  - If the temperature exceeds the threshold, it triggers a message. You can integrate a fan or AC control via the relay.

---

To integrate **Wi-Fi control and mobile app functionality** into the smart home system using **Blynk**,

---

### **1. Required Additional Components**
- **Wi-Fi Module:**  
  Use **ESP8266** (NodeMCU) or **ESP32** for Wi-Fi connectivity.
  - **NodeMCU/ESP32** replaces Arduino UNO as it has built-in Wi-Fi.
  
- **Smartphone with Blynk App Installed:**  
  - Download from [Google Play Store](https://play.google.com/store) or [Apple App Store](https://apps.apple.com/).

---

### **2. Steps to Configure Blynk**
#### **Step 1: Set Up Blynk App**
1. Open the **Blynk app** on your smartphone.
2. Create a new project:
   - Select **ESP8266** or **ESP32** as the hardware model.
   - Choose Wi-Fi as the connection type.
3. Add widgets to your project:
   - **Button**: To control relay (light/fan).
   - **LED Display**: To show temperature, light levels, or sound status.
4. Save your project, and you'll receive an **authentication token** via email.

---

#### **Step 2: Hardware Setup**
Wire the components as described earlier but connect sensors and actuators to the **ESP8266/ESP32** GPIO pins instead of Arduino.

Example:
- **Relay Module**: GPIO5 (D1).
- **LDR Sensor**: GPIO36 (A0 for ESP32).
- **DHT11 Sensor**: GPIO4 (D2).
- **Sound Sensor**: GPIO14 (D5).
- **Buzzer**: GPIO12 (D6).

---

#### **Step 3: Install Blynk Library**
1. Install the **Blynk Library**:
   - Open Arduino IDE.
   - Go to **Tools > Manage Libraries**.
   - Search for **Blynk** and install it.

2. Install ESP8266/ESP32 Boards:
   - Go to **File > Preferences**.
   - Add the following URL to the Additional Board Manager URLs:
     ```
     https://arduino.esp8266.com/stable/package_esp8266com_index.json
     ```
   - Go to **Tools > Board > Boards Manager**, search for ESP8266/ESP32, and install.

---

### **4. App Functionality**
- **Button Widget (V1):**  
  Toggle relay for controlling lights or fans.
  
- **Value Display Widgets (V2, V3):**  
  Show temperature, light intensity, and sound status.

- **Push Notifications (Optional):**  
  Add a **notification widget** in Blynk for alerts (e.g., high temperature or sound detection).

---

### **5. Testing**
1. Upload the code to the ESP8266/ESP32.
2. Ensure the ESP is connected to your Wi-Fi.
3. Open the Blynk app and test the widgets:
   - Tap the button to toggle the relay.
   - Observe real-time sensor values on the app.

Would you like assistance setting up more advanced features, like push notifications or a custom app interface?
