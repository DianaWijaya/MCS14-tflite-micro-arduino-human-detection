
# Arduino TensorFlow Lite Micro Human Detection Library

This repository contains the code and necessary examples to perform human detection using TensorFlow Lite Micro on the Arduino Nano 33 BLE Sense, integrated with the Arducam 2MP Plus camera module.

---

## Table of Contents
<!--ts-->
* [Project Overview](#project-overview)  
* [Hardware Requirements](#hardware-requirements)  
* [Hardware Integration](#hardware-integration)  
* [Installing Arduino IDE and Libraries](#installing-arduino-ide-and-libraries)  
* [Running the Program](#running-the-program)  
* [Customizing the Model and Configuration](#customizing-the-model-and-configuration)
<!--te-->

---

## Project Overview  
This project enables real-time human detection using TinyML models directly on the Arduino Nano 33 BLE Sense. The system utilizes a quantized TensorFlow Lite model to efficiently run inferences with minimal hardware resources, making it ideal for low-power IoT applications.  

---

## Hardware Requirements  

| Hardware                    | Quantity |
|-----------------------------|----------|
| Arduino Nano 33 BLE Sense Rev2 | 1        |
| Arducam OV2640 2MP Plus     | 1        |
| Breadboard                  | 1        |
| Male to Male Jumper Wires   | 8        |
| Header Pins                 | 2        |
| Micro USB Cable             | 1        |
| Programming Device          | 1        |

*Refer to Table 1.2.1 in the documentation for detailed specifications.*

---

## Hardware Integration  

Follow the pin mapping table below to establish proper SPI and I2C connections between the Arduino and Arducam modules:

| Arduino Nano 33 BLE Sense | Arducam 2MP Plus | Functionality      |
|---------------------------|------------------|--------------------|
| D7                        | CS               | SPI Communication  |
| D11                       | MOSI             | SPI Communication  |
| D12                       | MISO             | SPI Communication  |
| D13                       | SCK              | SPI Communication  |
| GND                       | GND              | Power              |
| 3.3V                      | VCC              | Power              |
| A4                        | SDA              | I2C Communication  |
| A5                        | SCL              | I2C Communication  |

*Refer to the official [Arduino Nano 33 BLE Sense Datasheet](https://docs.arduino.cc/resources/datasheets/ABX00069-datasheet.pdf) and the [Arducam 2MP Plus Guide](https://www.arducam.com/arducam-2mp-spi-camera-b0067-arduino.html) for additional details.*

---

## Installing Arduino IDE and Libraries  

Ensure that the following libraries are installed in your Arduino IDE:

| Library Name         | Description                         |
|----------------------|-------------------------------------|
| Arduino_TensorFlowLite | Run TFLite Micro models on Arduino |
| Arducam              | Interface with Arducam cameras     |
| JPEGDecoder          | Decode JPEG images to raw formats  |

Follow the detailed setup instructions in section 1.2.3 of the project documentation.

---

## Running the Program  

1. Open the Arduino IDE and connect your Arduino Nano 33 BLE Sense via USB.  
2. Select the correct board and port under the Tools menu.  
3. Load the program from:  
   `File > Examples > Arduino_TensorFlowLite > person_detection`  
4. Upload the code to your Arduino.  
5. The device will start performing inferences and indicate detections via the onboard LEDs:
   - **Green LED**: Person detected.
   - **Blue LED**: No person detected.
6. To view detailed inference outputs, open the Serial Monitor from the Arduino IDE.

---

## Customizing the Model and Configuration  

- Update `model_settings.h` to change input shape or image channels.  
- Adjust inference logic and thresholds in `person_detection.ino`.  
- To deploy a new model, convert your `.pth` model to `.tflite`, then to a C array using `xxd` or similar tools, and replace `person_detect_model_data.cpp`.  
- For optimizing memory, manually register only the necessary TFLite Micro operations using `MicroMutableOpResolver`.  
