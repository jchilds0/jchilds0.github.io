---
title: DIY Follow Focus
date: 2026-03-05 00:00
categories: [Embedded Systems]
tags: [esp32, embedded systems]     # TAG names should always be lowercase
math: true
comments: false
---

## **Introduction**

I have a DSLR which I use as a webcam or for video presentations.
Unfortunately, being a Nikon, the video autofocus isn't great and doesn't usually perform well for videos.
Manually focussing is not an option when the camera is too far away to reach, but the video production industry has a solution to this problem, the [follow focus](https://en.wikipedia.org/wiki/Follow_focus).
I don't need a professional wireless follow focus system, so I decided to build one myself. 
The following is the design and build instructions for anyone looking to build one too.
Source code for ESP32 firmware, KiCad schematics and 3D models available on [GitHub](https://github.com/jchilds0/follow-focus).
For programming, I'm using [ESP-IDF](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/index.html).

Disclaimer: I'm not an electrical engineer, do your own research and follow at your own risk.

## **Parts**

### **Control Unit**

- ESP32-C3 (from seeed studio)
- Rotary Encoder (part no. ACZ16NBR1E-15KQD1-24C or equivalent)
- 4x 100k Ohm resistor
- 2x 100nF ceramic capacitor
- 4x M3 brass heatset inserts
- 4x M3x8mm socket head bolts
- 4x M2x6mm socket head bolts

### **Motor Unit**

- ESP32-C3 (from seeed studio)
- NEMA 17 stepper motor
- DRV8825 stepper motor driver (or equivalent)
- L7805CV 5v regulator
- HUSB238 USB C Power Delivery Breakout Board
- 2x 100nF ceramic capacitor
- 1μF electrolytic capacitor
- 10μF electrolytic capacitor
- 100μF electrolytic capacitor
- 6x M2x8mm socket head bolts

Some parts can be substituted if not available:
- L7805CV: only used to power ESP32, can be replaced with any other power source such as a battery or usb c cable.
- HUSB238: used to deliver 12v 2A power to stepper motor and ESP32, can be replaced with any other 12v 2A source.
- ESP32-C3: may require modifying the 3D models if using a larger ESP32.

I hand-soldered both units, using 2x 70x30 mm prototype perf boards for the circuitry.

## **Design**

### **Control Unit**

The control unit is responsible for reading the rotary encoder inputs and transmitting the movements to the motor unit.
The control unit is powered using USB-C, but powering with a LiPo battery is also possible.

The rotary encoder requires decoding in order to read the movements.
I started with the filter circuit recommended by the rotary encoder manufacturer, using 100k Ohm pull down resistors and 10nF ceramic capacitors.
On the ESP32 C3, I used pos edge interrupts on the A output of the encoder, and reading the value of the B output to determine the direction.
This didn't debounce the encoder well, resulting in many erroneous readings.
The next attempt was using the ESP32's internal pull down resistors instead of external, but this also suffered from the same issues.
Next I moved back to the external filter, upped the capacitors to 100nF and re-wrote the ESP32 code to use a state machine, with interrupts on any edge change from output A and B.
This successfully filtered the rotary encoder.

For communication between ESP's, I'm using [ESP-NOW](https://www.espressif.com/en/solutions/low-power-solutions/esp-now).
This can be replaced with any other communication method.
The control unit sends two `uint8_t`, the first is the number of steps to take, and the second number is 1 for clockwise and 0 for anti-clockwise rotation.
This means we can only send up to 255 steps in one message, but due to the high frequency of communication, we don't require more than this.
This requires the MAC address of each ESP to send messages, which can be obtained using the following simple ESP-IDF program.

```c 
static const char *TAG = "mac_example";

void app_main(void)
{
    uint8_t mac[6];
    esp_err_t ret = esp_read_mac(mac, ESP_MAC_WIFI_STA);

    if (ret == ESP_OK) {
        ESP_LOGI(TAG, "ESP32-C3 MAC Address: %02X:%02X:%02X:%02X:%02X:%02X",
                 mac[0], mac[1], mac[2],
                 mac[3], mac[4], mac[5]);
    } else {
        ESP_LOGE(TAG, "Failed to read MAC address");
    }
}
```

Schematic

![control-unit-schematic](assets/follow-focus/control-unit-schematic.png)

### **Motor Unit**

The stepper motor requires 12v and can draw up to 2A.
For the circuit to work correctly, ensure the USB-C cable and the PD source used is rated for 2A at 12v.
If not, the HUSB238 will output 5v and the stepper motor won't work.

The motor unit receives messages from the control unit and instructs the motor driver to move the stepper motor.
The 100μF capacitor should be placed close to the VMOT and GND pins to prevent destructive LC voltage spikes which can damage the board.
Additionally the current should be limited using the potentiometer on the board, I set the current limit to 1A.
M0, M1 and M2 pins are used to set the microstep mode, and the `STEP_FACTOR` macro sets the number of steps to complete per step sent from the control unit.
I found using 1/8th microstep resolution and 2 step factor worked well.

Schematic

![motor-unit-schematic](assets/follow-focus/motor-unit-schematic.png)

## **Build**

### **Control Unit**

Solder the parts onto the prototype perf board and wire together or custom PCB.
Print the enclosure parts, PLA at any reasonable infill is sufficient.
Add brass inserts and screw together.
The RF antenna for the ESP32 is attached below the PCB

![control-unit-2](assets/follow-focus/control-2.jpg)
![control-unit-1](assets/follow-focus/control-1.jpg)

### **Motor Unit**

Solder the parts onto the prototype perf board and wire together or custom PCB.
Configure the HUSB238 to deliver 12v 2A, default is usually 5v 1A.
Print the enclosure parts, PLA at any reasonable infill is sufficient.
The PCB holder is glued to the motor mount.
The RF antenna for the ESP32 is attached to the underside of the PCB holder.

Depending on tolerances, the stepper motor gear may require sanding to fit on the stepper motor.
If requires, a brass insert can be added to use an M3 bolt to hold the gear to the stepper motor.

To attach the motor to a camera rig, I used the follow focus mount from a [3d printed dslr rig](https://pinshape.com/items/20920-3d-printed-dslrigger-open-source-camera-rig).

![motor-unit-1](assets/follow-focus/motor-1.jpg)
![motor-unit-2](assets/follow-focus/motor-2.jpg)
