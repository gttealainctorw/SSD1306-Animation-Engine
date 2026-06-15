# SSD1306 PROGMEM Animation

<p align="center">
  <img src="docs/demo.gif" width="450" alt="Animation Demo">
</p>

<p align="center">
  Optimized SSD1306 OLED Animation Engine for ESP8266 and ESP32
</p>

---
## Overview

SSD1306 PROGMEM Animation is a lightweight animation engine for SSD1306 OLED displays running on ESP8266 and ESP32 microcontrollers.

The project stores animation frames in Flash memory (PROGMEM), minimizing RAM usage while allowing long animation sequences to be played efficiently.

The repository includes a sample animation to demonstrate the engine's capabilities.

---

## Demo

The repository contains a demonstration animation.

<img width="537" height="622" alt="img" src="https://github.com/user-attachments/assets/41d3991e-d675-4194-b42f-d69e9c8e2701" />

## Features

* ESP8266 and ESP32 compatible
* SSD1306 OLED 128×64 support
* Frame storage in PROGMEM
* Non-blocking playback using millis()
* Multiple playback modes:

  * Loop
  * Once
  * Reverse
  * Ping-Pong
* Low RAM usage
* Watchdog-safe operation
* Modular AnimationPlayer architecture

---

## Hardware Requirements

### Supported Microcontrollers

* ESP8266

  * NodeMCU
  * Wemos D1 Mini
  * ESP-01
* ESP32

### Supported Displays

* SSD1306 OLED 128×64 (I2C)
* I2C address 0x3C (default)

---

## Required Libraries

Install through Arduino Library Manager:

* Adafruit GFX Library
* Adafruit SSD1306

---

## Wiring

### ESP8266

| OLED | ESP8266    |
| ---- | ---------- |
| VCC  | 3.3V       |
| GND  | GND        |
| SDA  | D2 (GPIO4) |
| SCL  | D1 (GPIO5) |

### ESP32

| OLED | ESP32  |
| ---- | ------ |
| VCC  | 3.3V   |
| GND  | GND    |
| SDA  | GPIO21 |
| SCL  | GPIO22 |

---

## Project Structure

```text
SSD1306-PROGMEM-Animation/
│
├── SSD1306-PROGMEM-Animation.ino
├── animation_frames.h
├── README.md
```

---

## Frame Format

Each frame must be stored in PROGMEM:

```cpp
const unsigned char frame_0[] PROGMEM = {
    // bitmap data
};

const unsigned char frame_1[] PROGMEM = {
    // bitmap data
};
```

The frame table must also be stored in PROGMEM:

```cpp
const unsigned char* const epd_bitmap_allArray[] PROGMEM = {
    frame_0,
    frame_1
};
```

---

## Does it work with any animation?

Yes, as long as the animation meets the following requirements:

* Monochrome bitmap format
* SSD1306 compatible
* 128×64 resolution (current configuration)
* Frames stored in PROGMEM

### Current limitations

The default configuration is designed for 128×64 OLED displays.

Additional resolutions require changing:

```cpp
SCREEN_WIDTH
SCREEN_HEIGHT
FRAME_BYTES
```

Color displays and grayscale images are not supported.

---

## Playback Modes

```cpp
PlaybackMode::LOOP
PlaybackMode::ONCE
PlaybackMode::REVERSE
PlaybackMode::PING_PONG
```

---

## Performance

* 400 kHz I2C communication
* Direct frame copy from PROGMEM
* Non-blocking timing
* Optimized RAM usage
* ESP8266 and ESP32 watchdog friendly

---

## Memory Usage

For a 128×64 display:

* Frame size: 1024 bytes
* 102 frames: ~102 KB Flash
* Display buffer: 1024 bytes RAM

---

## License

MIT License

---

## Author

@gttealainctorw

