---
title: My DIY Volume Mixer Part 1
description: >-
  Creating a custom hardware volume mixer using ESP32 microcontroller and slide potentiometers.
  Control app volumes like a DJ with this open-source solution for Windows/Linux.
author: ahempi
date: 2025-03-07 16:22:00
categories: [DIY Electronics, Audio Projects]
tags: [ESP32, Hardware Mixer, Open-Source, Volume Control]
pin: false
media_subpath: "/assets/img"
---

With guidance from my father, I've embarked on creating a custom hardware volume mixer for my PC.

## What is Deej?

Deej is an open-source project that turns hardware sliders into app-specific volume controls for Windows/Linux. Key features:

- **Multi-app control**: Adjust music, games, and chat volumes independently
- **Plug-and-play**: No drivers needed
- **Customizable**: Map sliders to any audio session
- **Cross-platform**: Works with both Windows and Linux

GitHub Repo: [https://github.com/omriharel/deej](https://github.com/omriharel/deej)

# Hardware components

### 1. ESP32 Development Board

![ESP32 Module](ESP32.png){: .right w="300" h="200" }

**Why ESP32?**

- Built-in WiFi/Bluetooth for wireless connectivity
- 18-bit ADC resolution for precise analog readings
- Dual-core processor for smooth operation
- Supports MicroPython for rapid prototyping

_Specs_:

- 240 MHz CPU
- 520 KB SRAM
- 802.11 b/g/n WiFi
- Hall sensor & touch GPIOs

[ESP32 on AliExpress](https://de.aliexpress.com/item/1005005704190069.html)

### 2. Slide Potentiometers

![10KΩ Linear Pot](Liner_Potentiometer.png){: .right w="250" h="200" }

**Key Specifications:**

- Resistance: 10KΩ
- Stroke length: 75mm
- Mounting: PCB-friendly vertical pins

**Why linear taper?**  
Provides consistent resistance change per unit movement, crucial for precise volume control compared to logarithmic tapers used in audio equipment.

[Potentiometers on AliExpress](https://www.aliexpress.com/item/1005005453551178.html)

### 3. Prototype Board

![Universal PCB](Protoboard.png){: .right w="250" h="200" }

**Chosen Specifications:**

- Size: 12x8cm
- Material: FR-4 fiberglass
- Layout: 2.54mm standard pitch
- Features: Power rails & component labels

Perfect for creating a durable circuit without custom PCB fabrication.

[Prototype Board on AliExpress](https://www.aliexpress.com/item/1005004941494955.html)

### 4. Jumper Wires Kit

![Breadboard Wires](Breadboard_Jumper_Cable_Wire_Kit.png){: .right w="250" h="200" }

**Kit Includes:**

- Transparent and high-quality storage box
- 140 long and short jumpers, red, orange, yellow, green, blue, purple, gray, brown and white.

[Jumper Kit on AliExpress](https://www.aliexpress.com/item/1005004917329293.html)

Total cost of the components at a time was 11.4 USD.

## Circuit Design & Simulation

### Wokwi Simulation Setup

![Simulation Screenshot](simulation_ESP32.png){: .center w="600" h="400" }

**Key Steps:**

1. **ADC Configuration**:  
   Set up ESP32's ADC1_CHANNEL_0 with 12-bit resolution

   ```python
   from machine import ADC, Pin
   pot = ADC(Pin(34))
   pot.atten(ADC.ATTN_11DB)  # Full 3.3V range
   ```

2. **Reading Values**:  
   Continuous sampling with 100ms interval
   ```python
   while True:
       val = pot.read()
       print("ADC Value:", val)
       time.sleep(0.1)
   ```

**Try my simulation yourself:**  
[Wokwi Project Link](https://wokwi.com/projects/395695341575852033)
