---

title: My DIY Volume Mixer Part 2
description: >-
  Building the hardware and writing the firmware for the custom volume mixer using ESP32 and potentiometers.
author: ahempi
date: 2025-05-11 10:00:00
categories: [DIY Electronics, Audio Projects]
tags: [ESP32, Hardware Mixer, Open-Source, Volume Control]
pin: false
media_subpath: "/assets/img"

---

In Part 1, we covered the components and initial setup for the DIY volume mixer. In this post, we’ll dive into assembling the hardware, adding resistors, writing the firmware, and flashing the ESP32 to bring the project to life.

---

## Hardware Assembly

### Step 1: Preparing the Components
Before assembling, ensure you have all the components ready:
- ESP32 Development Board
- Slide potentiometers
- Prototype board
- Resistors (10kΩ)
- Jumper wires
- Soldering tools

### Step 2: Soldering the Potentiometers
1. Place the slide potentiometers on the prototype board.
2. Solder the pins securely to the board.
3. Connect the middle pin (signal) of each potentiometer to the ESP32’s ADC pins (e.g., GPIO34, GPIO35, GPIO32).
4. Connect one side pin to 3.3V and the other to GND.

![Soldered Potentiometers and ESP3](soldered_potentiometers_esp32.jpg){: w="500" h="400" }

### Step 3: Adding Resistors
To stabilize the ADC readings and prevent noise, we added 10kΩ pull-down resistors between the signal pins of the potentiometers and GND. This ensures the ADC pins read a stable voltage when the potentiometers are at their minimum position.

### Step 4: Wiring the ESP32
1. Use jumper wires to connect the potentiometers and resistors to the ESP32.
2. Ensure proper connections for power, ground, and signal lines.
3. Double-check the wiring to avoid short circuits.

![Wiring Underneath the Prototype Board](wiring_underneath_prototype_board.jpg){: w="500" h="400" }

---

## Flashing the ESP32

### Step 1: Install Required Tools
1. Download and install Python 3 from [python.org](https://www.python.org/).
2. Install `esptool` using pip:
   ```bash
   pip install esptool
   ```

### Step 2: Flash MicroPython Firmware
1. Download the latest MicroPython firmware for ESP32 from the [MicroPython website](https://micropython.org/download/esp32/).
2. Connect the ESP32 to your PC via a USB cable.
3. Identify the COM port of your ESP32:
   - On Windows, open Device Manager and look under "Ports (COM & LPT)".
4. Erase the flash memory:
   ```bash
   esptool.py --chip esp32 --port COM3 erase_flash
   ```
5. Flash the MicroPython firmware:
   ```bash
   esptool.py --chip esp32 --port COM3 write_flash -z 0x1000 esp32-2025-05-01-v1.20.bin
   ```

---

## Connecting the Serial Monitor

### Step 1: Install a Serial Monitor
You can use any serial monitor tool, such as:
- [PuTTY](https://www.putty.org/)
- [Thonny IDE](https://thonny.org/)
- Arduino IDE (Serial Monitor)

### Step 2: Configure the Serial Connection
1. Open your serial monitor tool.
2. Select the COM port of your ESP32.
3. Set the baud rate to `115200`.
4. Open the connection to view the output.

### Step 3: Test the Connection
1. After flashing the firmware, you should see the MicroPython REPL prompt (`>>>`) in the serial monitor.
2. If you upload the provided firmware code, you will see the ADC values printed in the format `adc1|adc2|adc3|adc4`.

---

## Firmware Development

### Step 1: Writing the Code
The firmware reads ADC values from the potentiometers, applies corrections for noise and scaling, and sends the values to the PC via serial communication.

```python
from machine import Pin, ADC
from time import sleep

# Configure ADC pins
pot1 = ADC(Pin(27))
pot2 = ADC(Pin(25))
pot3 = ADC(Pin(32))
pot4 = ADC(Pin(34))

# Set attenuation for 3.3V range
for pot in [pot1, pot2, pot3, pot4]:
    pot.atten(ADC.ATTN_6DB)

# Function to correct ADC values
def correct_adc(adc_val, min_val, gain):
    adc_val = adc_val - min_val
    adc_val = int(adc_val / gain)
    
    if adc_val > 1023:
        adc_val = 1023
    if adc_val < 0:
        adc_val = 0

    return adc_val

while True:
    # Read and correct ADC values
    adc1 = correct_adc(pot1.read(), 526, 3.36)
    adc2 = correct_adc(pot2.read(), 570, 3.09)
    adc3 = correct_adc(pot3.read(), 454, 3.405)
    adc4 = correct_adc(pot4.read(), 429, 3.42)

    # Print values to serial
    print(f"{adc1}|{adc2}|{adc3}|{adc4}")
    sleep(0.1)
```

### Explanation of the Code
1. **ADC Configuration**:  
   Each potentiometer is connected to an ADC pin on the ESP32. The `atten()` method sets the ADC range to handle the full 3.3V input.

2. **Noise Correction**:  
   The `correct_adc` function adjusts the raw ADC values by subtracting a minimum value (`min_val`) and scaling the result using a gain factor. This ensures consistent readings across all potentiometers.

3. **Serial Output**:  
   The corrected ADC values are printed to the serial monitor in a pipe-separated format (`adc1|adc2|adc3|adc4`), which can be parsed by software like Deej.

---

## Testing the Firmware
1. Connect the ESP32 to your PC via USB.
2. Open a serial monitor (e.g., PuTTY or Thonny) to view the ADC values.
3. Move the sliders and verify that the values change accordingly.

---

## Next Steps
In Part 3, we’ll integrate the firmware with the Deej software to map the potentiometer inputs to specific application volumes. Stay tuned!

---

**Resources:**
- [MicroPython Documentation](https://docs.micropython.org/en/latest/)
- [ESP32 Pinout Reference](https://randomnerdtutorials.com/esp32-pinout-reference/)

**GitHub Repository:** [Volume Mixer Project](https://github.com/ahempi/volume-mixer)
