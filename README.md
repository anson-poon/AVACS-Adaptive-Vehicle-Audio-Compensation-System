# Adaptive Vehicle Audio Compensation System

An embedded, hardware-in-the-loop application developed in C++ for the Arduino UNO architecture. This system automatically normalizes vehicle audio output relative to ambient road noise by mapping real-time velocity metrics to mechanical servo actuation.

The system acts as a human-factors safety feature, eliminating the need for a driver to manually adjust audio hardware while traveling at higher speeds to compensate for external noise, making it an ideal retrofit for classic or legacy vehicles lacking modern digital interfaces.


## Features

* **Real-Time Telemetry Parsing:** Decodes streaming serial data from a GPS module to extract accurate velocity metrics.
* **Actuation Mapping:** Translates velocity values into precise target rotation angles for a servo motor, accounting for mechanical gear ratios.
* **Mechanical Smoothing:** Implements an incremental dampening loop to transition the servo smoothly between states, preventing sudden mechanical jerks and system strain.
* **Fault-Tolerant Diagnostics:** Actively monitors GPS signal validity, updating an onboard OLED display over I2C with real-time tracking data and cycling status LEDs to indicate connectivity states.
* **Custom 3D-Printed Integration:** Utilizes 3D-printed gears with calibrated gear ratios, servo motor enclosures, and custom mounts to physically bridge the electronic components to a vehicle's mechanical audio interface.


## System Architecture & Hardware

### Components Used
* **Microcontroller:** Arduino UNO R3
* **Telemetry Sensor:** Neo-6M V2 GPS Module (UART Serial interface)
* **Display Interface:** 1.3" 128x64 I2C SH1106 OLED Display Module
* **Actuator:** SM-S2309S Micro Servo Motor (PWM interface)
* **Status Indicators:** Red & Green LEDs (with 220-ohm current-limiting resistors)

### Mechanical Design
The physical interface was designed using Autodesk Fusion to handle the translation of motion from the micro-servo to the hardware dashboard controls. The CAD models are optimized for rapid 3D-printed prototyping:
* **Gearing:** Custom-calculated bevel gear and pinion set to establish 1.5x mechanical gear ratio.
* **Structural Enclosure:** A custom snap-fit housing to rigidly secure the servo motor against rotational torque.

Isometric Assembly (exploded-view)
![Installation Isometric](https://github.com/anson-poon/Dynamic-Road-Noise-Equalizer/assets/75619539/ad5bdb2a-4c47-4796-9582-ef9677e20962)

Wiring Schematic (w/breadboard)
![Breadboard Wiring Schematic](https://github.com/anson-poon/Dynamic-Road-Noise-Equalizer/assets/75619539/46167d5c-4750-48a5-a66e-4267710476cf)

Wiring Schematic (net)
![Net Wiring Schematic](https://github.com/anson-poon/Dynamic-Road-Noise-Equalizer/assets/75619539/4cc4920d-4ce5-4468-8241-81d79541acd3)


## Repository Structure

```text
├── GPS_OLED.ino              # Main C++ embedded driver application
├── Enclosure Assembly.3mf    # 3D model for the snap-fit servo housing
├── Servo Bevel Wheel Gear.stl # 3D model for the driven bevel gear
└── Servo Bevel Pinon Gear.stl # 3D model for the motor-mounted pinion gear
```

## Dependencies & Libraries

The application relies on the following standard embedded libraries:
* `<TinyGPS++.h>` - Object-oriented parsing of NMEA data streams.
* `<SoftwareSerial.h>` - Emulation of an additional hardware serial port for telemetry intake.
* `<PWMServo.h>` - Jitter-free hardware PWM control for precise servo positioning.
* `<Adafruit_SH1106.h>` & `<Wire.h>` - I2C communication protocol management for visual diagnostics.
