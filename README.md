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

### **2. Code Examples**

#### **Setup Code**
Here’s a combined Arduino code to manage all the sensors and actuators.

```cpp
#include <DHT.h>

// Pin Assignments
#define LDR_PIN A0  // Light sensor
#define SOUND_PIN 2 // Sound sensor digital pin
#define DHT_PIN 3   // Temperature sensor
#define RELAY_PIN 4 // Relay module
#define LED_PIN 5   // LED indicator
#define BUZZER_PIN 6 // Buzzer

// DHT Sensor Type (DHT11 or DHT22)
#define DHT_TYPE DHT11
DHT dht(DHT_PIN, DHT_TYPE);

// Thresholds
int lightThreshold = 500; // Adjust based on ambient light levels
int soundThreshold = 100; // For sound sensor triggering
float tempThreshold = 30.0; // Degrees Celsius

void setup() {
  // Initialize components
  pinMode(SOUND_PIN, INPUT);
  pinMode(RELAY_PIN, OUTPUT);
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  digitalWrite(RELAY_PIN, LOW); // Initially turn off the relay
  digitalWrite(LED_PIN, LOW);   // Turn off LED
  digitalWrite(BUZZER_PIN, LOW); // Turn off buzzer

  // Start communication
  Serial.begin(9600);
  dht.begin();

  Serial.println("Smart Home System Initialized!");
}

void loop() {
  // Read sensors
  int lightValue = analogRead(LDR_PIN);
  int soundValue = digitalRead(SOUND_PIN);
  float temperature = dht.readTemperature();

  // Light control based on LDR
  if (lightValue < lightThreshold) {
    digitalWrite(RELAY_PIN, HIGH); // Turn on the light
    digitalWrite(LED_PIN, HIGH);   // LED indicator ON
  } else {
    digitalWrite(RELAY_PIN, LOW); // Turn off the light
    digitalWrite(LED_PIN, LOW);  // LED indicator OFF
  }

  // Sound detection for buzzer
  if (soundValue == HIGH) {
    digitalWrite(BUZZER_PIN, HIGH); // Sound alarm
    delay(500); // Keep the buzzer on for 500ms
    digitalWrite(BUZZER_PIN, LOW);
  }

  // Temperature control
  if (temperature > tempThreshold) {
    Serial.println("Temperature exceeded threshold!");
    // You can add fan control here using a relay
  }

  // Log data to serial monitor
  Serial.print("Light: "); Serial.print(lightValue);
  Serial.print(", Sound: "); Serial.print(soundValue);
  Serial.print(", Temp: "); Serial.println(temperature);

  delay(1000); // Wait for 1 second before repeating
}
```

---

### **3. Circuit Diagram Explanation**
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

### **4. Functionality**
- **Light Control:**
  - The relay turns on when the light level drops below the threshold.
  - The LED indicates when the relay is active.

- **Sound Alert:**
  - When the sound sensor detects a noise above the threshold, the buzzer activates briefly.
 
  - Let’s design the **smart home automation system** using light, sound, and temperature sensors with Arduino. Below, you'll find the circuit diagram explanation and code examples for each functionality.

- **Temperature Monitoring:**
  - If the temperature exceeds the threshold, it triggers a message. You can integrate a fan or AC control via the relay.

---

To integrate **Wi-Fi control and mobile app functionality** into the smart home system using **Blynk**, follow these steps:

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

### **3. Code Example for Blynk Integration**

Below is an example sketch:

```cpp
#define BLYNK_TEMPLATE_ID "Your_Template_ID"
#define BLYNK_DEVICE_NAME "Smart Home"
#define BLYNK_AUTH_TOKEN "Your_Auth_Token"

// Include necessary libraries
#include <WiFi.h> // For ESP32/ESP8266
#include <BlynkSimpleEsp32.h> // Use <BlynkSimpleEsp8266.h> for ESP8266
#include <DHT.h>

// Wi-Fi credentials
char ssid[] = "Your_SSID";         // Replace with your Wi-Fi name
char pass[] = "Your_PASSWORD";     // Replace with your Wi-Fi password

// DHT Sensor setup
#define DHTPIN 4 // GPIO4 (D2 on ESP8266)
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

// Relay and other pins
#define RELAY_PIN 5   // GPIO5 (D1)
#define BUZZER_PIN 12 // GPIO12 (D6)
#define SOUND_PIN 14  // GPIO14 (D5)
#define LDR_PIN 36    // GPIO36 (A0 for ESP32)

// Blynk virtual pins
#define V_LIGHT V1
#define V_TEMP V2
#define V_SOUND V3

void setup() {
  // Start serial monitor
  Serial.begin(9600);

  // Initialize Blynk
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

  // Initialize sensors and actuators
  pinMode(RELAY_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(SOUND_PIN, INPUT);
  digitalWrite(RELAY_PIN, LOW); // Turn off relay initially

  dht.begin();
}

void loop() {
  Blynk.run();

  // Read sensor values
  int lightValue = analogRead(LDR_PIN);
  float temperature = dht.readTemperature();
  int soundDetected = digitalRead(SOUND_PIN);

  // Send data to Blynk app
  Blynk.virtualWrite(V_LIGHT, lightValue);
  Blynk.virtualWrite(V_TEMP, temperature);
  Blynk.virtualWrite(V_SOUND, soundDetected);

  // Auto-control example
  if (lightValue < 500) { // Low light
    digitalWrite(RELAY_PIN, HIGH); // Turn on relay
  } else {
    digitalWrite(RELAY_PIN, LOW); // Turn off relay
  }
}
```

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
  
---

Here’s how to set up advanced features, like **push notifications** and **customizing your Blynk app interface**, for a more powerful smart home system:

---

## **1. Push Notifications in Blynk**

### **What are Push Notifications?**
Push notifications send real-time alerts to your smartphone via the Blynk app. For example:
- A notification when the temperature exceeds a threshold.
- Alerts when sound is detected.

### **Steps to Set Up Push Notifications**
#### **a. Add the Push Notification Widget**
1. Open your Blynk project.
2. Click the **+** button to add a widget.
3. Select **Notifications**.
4. Place the widget in your project.

#### **b. Modify Your Code for Notifications**
Add the following lines to trigger notifications based on sensor values.

```cpp
void loop() {
  Blynk.run();

  // Read sensors
  float temperature = dht.readTemperature();
  int soundDetected = digitalRead(SOUND_PIN);

  // Check conditions and send notifications
  if (temperature > 30.0) { // Example: Temp threshold
    Blynk.notify("High Temperature Alert! Room temperature is above 30°C.");
  }

  if (soundDetected == HIGH) { // Example: Sound threshold
    Blynk.notify("Sound detected!");
    delay(5000); // Add delay to prevent multiple alerts in a short time
  }

  // Other Blynk updates
  Blynk.virtualWrite(V_TEMP, temperature);
  Blynk.virtualWrite(V_SOUND, soundDetected);
}
```

---

## **2. Customizing the Blynk App Interface**

You can design a tailored interface for better control and monitoring:

### **a. Interface Suggestions**
- **Button Widget:** To toggle lights or fans (linked to the relay pin).
- **LED Indicator Widget:** To show the status of appliances (on/off).
- **Value Display Widgets:** To monitor real-time sensor data (temperature, light, sound).
- **Graph Widget:** To track historical trends of temperature or light levels.
- **Notification Widget:** For push alerts.

### **b. Customizing with Virtual Pins**
Use virtual pins in your Blynk app to customize data flow between the ESP and the app. For example:
- **Virtual Pin V1:** Control relay (lights).
- **Virtual Pin V2:** Display temperature.
- **Virtual Pin V3:** Display light sensor values.

### **Example Configuration**
1. **Relay Control (V1):**
   - Add a **Button Widget** linked to V1.
   - Update your code to control the relay via this button:

   ```cpp
   BLYNK_WRITE(V1) {
     int buttonState = param.asInt(); // Get button state
     digitalWrite(RELAY_PIN, buttonState); // Control relay
   }
   ```

2. **Temperature Display (V2):**
   - Add a **Value Display Widget** linked to V2.
   - Send temperature data to V2:

   ```cpp
   Blynk.virtualWrite(V2, temperature);
   ```

3. **Light Sensor Graph (V3):**
   - Add a **Graph Widget** linked to V3.
   - Send light sensor data periodically:

   ```cpp
   Blynk.virtualWrite(V3, analogRead(LDR_PIN));
   ```

---

## **3. Advanced Automation**
You can automate actions based on sensor inputs without manual control.

### **a. Automate Relay Based on Temperature**
Control a fan/AC relay if the temperature crosses a threshold:

```cpp
if (temperature > 30.0) {
  digitalWrite(RELAY_PIN, HIGH); // Turn on fan/AC
} else {
  digitalWrite(RELAY_PIN, LOW); // Turn off fan/AC
}
```

### **b. Night Mode for Lights**
Turn on lights automatically when it gets dark:

```cpp
if (analogRead(LDR_PIN) < 500) { // Example threshold
  digitalWrite(RELAY_PIN, HIGH); // Turn on lights
} else {
  digitalWrite(RELAY_PIN, LOW); // Turn off lights
}
```

---

## **4. Additional Features**
### **a. Email Alerts**
Blynk also allows sending email notifications for critical events.
1. Add the **Email Widget** in your project.
2. Modify your code to send emails:

```cpp
Blynk.email("your_email@example.com", "Alert", "High temperature detected!");
```

### **b. Dashboard for Multiple Rooms**
You can monitor multiple rooms or devices by:
- Adding separate widgets for each room/device.
- Assigning unique virtual pins for each sensor or relay.

---

## **5. Testing the App**
1. Open the Blynk app and test each widget:
   - Toggle the relay using the button.
   - Check if sensor values update in real time.
   - Simulate events (e.g., loud sounds or high temperature) to test notifications.
2. Fine-tune thresholds and delays for smoother operation.

---

## **6. What’s Next?**
- **Voice Integration:** Use Google Assistant or Alexa to control the system via IFTTT.
- **Web Dashboard:** Create a Blynk web interface to control and monitor from a browser.
- **Expandable System:** Add more sensors or devices, like motion detectors or security cameras.

---

To set up a **Blynk web interface** for monitoring and controlling your smart home system from a browser, follow these steps:

---

### **1. What You Need**
- **Blynk IoT Account**:  
  The web interface is part of the **Blynk IoT platform**. If you’re using the new Blynk IoT version (launched in 2021), you already have access to the web dashboard.
  
- **Hardware**:  
  ESP32 or ESP8266 with the previous system components (LDR, DHT11, relay, sound sensor, etc.).

---

### **2. Set Up Blynk IoT**
#### **Step 1: Create an Account**
1. Go to the [Blynk IoT website](https://blynk.io/).
2. Sign up for a free account (or log in if you already have one).
3. Once logged in, you'll see the **Blynk Console**, which is used to manage your projects.

#### **Step 2: Create a New Template**
1. In the **Blynk Console**, click **Templates** > **New Template**.
2. Fill in the details:
   - **Template Name**: Smart Home Automation
   - **Hardware**: ESP32 or ESP8266
   - **Connection Type**: Wi-Fi
3. Save the template.

#### **Step 3: Set Up Data Streams**
Data streams define how data is sent between your ESP and Blynk. Create streams for your sensors and actuators:
1. Go to the **Datastreams** tab in your template.
2. Add **Virtual Pin Datastreams** for:
   - Light Level (`V1`)
   - Temperature (`V2`)
   - Sound Detection (`V3`)
   - Relay Control (`V4`)
3. Configure each stream:
   - **Name**: For example, "Light Level."
   - **Pin Type**: Virtual.
   - **Data Type**: Integer (for light level/sound) or Float (for temperature).

---

### **3. Set Up the Web Dashboard**
#### **Step 1: Design the Dashboard**
1. Go to the **Web Dashboard** tab in your template.
2. Drag and drop widgets:
   - **Label Display** for light, sound, and temperature values.
   - **Switch** for relay control.
   - **Chart** to show historical trends (for temperature or light level).
3. Assign each widget to its respective virtual pin.

#### **Step 2: Customize Widget Settings**
- **Switch Widget**:  
  Link it to the relay's virtual pin (e.g., `V4`).
- **Label Displays**:  
  Assign them to their corresponding data streams (`V1`, `V2`, `V3`).
- **Chart Widget**:  
  Configure the chart to show historical data for selected data streams.

---

### **4. Update the ESP Code**
The ESP needs to send and receive data via the Blynk IoT platform. Here's an updated code example:

```cpp
#define BLYNK_TEMPLATE_ID "Your_Template_ID"
#define BLYNK_DEVICE_NAME "Smart Home"
#define BLYNK_AUTH_TOKEN "Your_Auth_Token"

// Include necessary libraries
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>
#include <DHT.h>

// Wi-Fi credentials
char ssid[] = "Your_SSID";         // Replace with your Wi-Fi name
char pass[] = "Your_PASSWORD";     // Replace with your Wi-Fi password

// DHT Sensor setup
#define DHTPIN 4 // GPIO4
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

// Pin assignments
#define RELAY_PIN 5
#define LDR_PIN 36
#define SOUND_PIN 14

void setup() {
  // Initialize serial communication
  Serial.begin(9600);

  // Initialize Blynk
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

  // Initialize sensors and actuators
  pinMode(RELAY_PIN, OUTPUT);
  pinMode(SOUND_PIN, INPUT);
  digitalWrite(RELAY_PIN, LOW); // Turn off relay initially

  dht.begin();
}

void loop() {
  Blynk.run();

  // Read sensors
  int lightValue = analogRead(LDR_PIN);
  float temperature = dht.readTemperature();
  int soundDetected = digitalRead(SOUND_PIN);

  // Send data to Blynk
  Blynk.virtualWrite(V1, lightValue);
  Blynk.virtualWrite(V2, temperature);
  Blynk.virtualWrite(V3, soundDetected);
}

// Control relay via the web interface
BLYNK_WRITE(V4) {
  int relayState = param.asInt();
  digitalWrite(RELAY_PIN, relayState);
}
```

---

### **5. Testing the Web Dashboard**
1. Flash the updated code to your ESP32/ESP8266.
2. Log in to your Blynk IoT console.
3. Open the **Web Dashboard**.
4. Test the widgets:
   - Use the **Switch Widget** to toggle the relay.
   - Monitor real-time sensor data updates in the **Label Displays**.
   - View historical data in the **Chart Widget**.

---

### **6. Adding Mobile App Support**
Once the web interface is set up, the Blynk app can sync automatically:
1. Open the Blynk app on your smartphone.
2. Log in using the same account as the web console.
3. Your project will appear in the app, ready to use with the same widgets.

---

### **7. Next Steps**
- Add **event notifications** to trigger alerts for critical conditions.
- Configure **roles and permissions** to share the dashboard with family members.
- Set up **automation rules** (e.g., automatically turning on lights at night).
