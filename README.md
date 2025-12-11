# ESP32-face-recognition-system
This project documents the creation of a low-cost, portable, wireless video streaming system built around the versatile ESP32-CAM module.

---

## **1. Project Overview**

This project involves using the **ESP32-CAM** module to build a **face detection system**. It operates wirelessly and is powered by **lithium-ion battery** via a **step-up voltage regulator**. The goal is to create a portable system that captures video and transmits it wirelessly to a laptop or server for real-time streaming.

This was a mini-project that I created during my second year in Computer Science Engineering.

### **What is an ESP32-cam?**

The **ESP32-CAM** is a low-cost, compact development board that integrates an **ESP32 microcontroller** with a **camera module** (typically the OV2640). It supports **Wi-Fi** and **Bluetooth**, making it ideal for **IoT, surveillance, facial recognition, and streaming applications**. It has a built-in **microSD card slot**, GPIO pins, and can be programmed using **Arduino IDE or ESP-IDF**. However, it lacks onboard USB, requiring an **external FTDI adapter** for programming.

<img width="480" height="377" alt="image" src="https://github.com/user-attachments/assets/5ec2b5db-9b57-4723-8c27-a036675ae73d" />


Box containing the system

<img width="240" height="427" alt="image" src="https://github.com/user-attachments/assets/d8d19d95-24b6-49e9-84fc-faea107def1c" />


Inside of the box

---

## **2. Components Required (Budget ~600 INR)**

- **ESP32-CAM Module**
- **FTDI Programmer** (for initial programming, one side 5 pins, other USB)
- **1x Lithium-ion battery** (1500mAH)
- **5V Step-Up Voltage Regulator** (to power the battery too, e.g., **DIY 18650**)
- **Jumper Wires** (female to female)
- **Other things:** ON/OFF switch, solder, a container box, some wires

It costed me around 600 rupees to make this mini project and I ordered all these components from robocraze.in.

---

## **3. Programming the ESP32-CAM**

### **Step 1: FTDI Programmer Setup**

- Connect the **FTDI programmer** to the ESP32-CAM for uploading code:
    - **FTDI VCC (5V)** → **ESP32-CAM VCC**
    - **FTDI GND** → **ESP32-CAM GND**
    - **FTDI TX** → **ESP32-CAM RX**
    - **FTDI RX** → **ESP32-CAM TX**
    - Connect **IO0** pin to **GND** (this is needed for programming mode).

### **Step 2: Upload Code**

- Reference video → https://www.youtube.com/watch?v=thso22siZY8&ab_channel=Tc0rn
- Connect the USB end of the FTDI unit to the laptop directly.
- Download the TTL driver module from this link.
https://www.mediafire.com/file/982x6iyk89v95dp/Prolific_PL2303_driver_v3.3.2.102_%25282008-24-09%2529_Win8_x64_x86.7z/file
- Extract the files downloaded.
- Then go to Computer Management and then Device Manager. Select ports, right-click the FTDI component and choose update driver. Browse the extracted file named **ser2pl** and install it and close the window.
- Now open Arduino IDE and install **esp32 board** by expressif systems.
- Now go to **tools**, and select **AI-thinker ESP32** module in the board menu, tools → board → ESP32 ARDUINO → **AI-thinker ESP.**
- Now use the **tools** settings shown in the image.
- Now choose **CameraWebServer** menu as from the examples menu shown in the image.
- New code window will be loaded. **Uncomment** the **AI-thinker library** only and comment the other libraries.
- Add your **Home-WI-fi/Mobile hotspot** credentials in the **SSID** and **password** code line.
- Before uploading, press the reset button of the ESP-32 cam and then upload the code.
- Once uploaded, **remove the jumper** between **IO0** and **GND** to exit programming mode.
- Now select the **serial monitor** in Arduino IDE and make sure there is **115200 baud** selected from the dropdown.
- Again, press the reset button of the ESP32 cam.
- You will see an **IP address link** at the end. Copy it.
- Now the code is uploaded in the ESP32 cam and you can remove all the wires from it and keep the FTDI programmer aside, you might use it again.

<img width="320" height="184" alt="image" src="https://github.com/user-attachments/assets/d80698d5-4673-476f-84ad-7b4b41df645c" />

---

## **4. Circuit Connections**

Must use a solder to make these connections.

### **Step 1: Battery Setup**

- Use a **1500mAh lithium-ion battery** as the main power source.
- Connect the **battery's positive (+) terminal** to the **VIN (Input +) pin** of the step-up voltage regulator.
- Connect the **battery's negative (-) terminal** to the **GND (Input -) pin** of the step-up voltage regulator.

### **Step 2: Connect Step-Up Regulator to ESP32-CAM**

- Connect the **5V output (+)** from the step-up regulator to the **VIN** pin on the ESP32-CAM.
- Connect the **ground (-)** from the step-up regulator to the **GND** pin on the ESP32-CAM.

<img width="383" height="309" alt="image" src="https://github.com/user-attachments/assets/1412f1f5-36d9-49a4-9768-c54d9ff81d0e" />

Circuit (The led and the resistor is optional)

---

## **5. Final Assembly and Streaming**

- Connect the **output of the step-up regulator (5V)** to the **VIN** and **GND** pins of the ESP32-CAM.
- The ESP32-CAM is now **turned ON**. It will automatically be connected with your home wi-fi or phone’s hotspot.
- Paste the IP address link in your browser and **START STREAMING.**

---

## **6. Key Notes**

- Camera-Server connection.
    - Your camera and the phone or laptop should be connected to the same Home Wi-fi.
    - Other way is to connect the camera with phone’s hotspot and then access the IP address link via browser.
    - There should only be one browser using the IP link at a time.
    - To connect it with other wi-fi, you can either change your device hotspot credentials to the SSID/password you added in the code or you can re-program the code using the FTDI programmer.
- **Battery Life:**
    - The **1500mAh lithium-ion battery** can provide a runtime of **1-2 hours** of continuous video streaming, depending on the efficiency of the step-up regulator and Wi-Fi usage.
    - Also, use a low-voltage supply source like charging it via a **laptop** USB end.
- **Voltage Regulation:**
    - Ensure the **step-up regulator** maintains a stable **5V output** as ESP32-CAM works at not more than 5V supply.
- Use a solder to make the connections.
- Use a double-sided tape to stick the components of the circuit inside the container box.
- Optional: The ESP-32 cam has already an antenna inside it. But you can integrate an external antenna to it for better range.

---

## **7. Some Use Cases**

The ESP32-CAM wireless face detection system can be adapted for various real-world applications, such as a mirror.

**1. Home Security Systems**

- **Face Recognition for Door Access:** Identifies visitors and grants access to authorized individuals.

**2. Attendance Tracking**

- **Automated Attendance Systems:** Logs attendance in offices or schools without manual intervention.

---

## 8. References

https://chatgpt.com/share/679b56d4-fd48-8003-a147-f53665cf8705

https://www.youtube.com/watch?v=thso22siZY8&ab_channel=Tc0rn

https://www.youtube.com/watch?v=k_PJLkfqDuI&ab_channel=MaxImagination

https://randomnerdtutorials.com/esp32-cam-video-streaming-face-recognition-arduino-ide/

---

## **9. Conclusion**

This blueprint outlines the complete build for an **ESP32-CAM** powered by a **1500mAh lithium-ion battery**, featuring a **step-up voltage regulator** for stable operation. The system is **portable, wireless**, and capable of face detection, making it ideal for applications where mobility is required.

You can contact me on LinkedIn regarding this project.

**Tags:** #miniproject #btech #cse #aiml #project #secondyear

---
