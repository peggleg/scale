# ESP32 WiFi Scale with HX711 (and Optional OLED Display)

This project provides ESPHome configurations for building a WiFi-connected digital scale using an ESP32 and an HX711 load cell amplifier. An optional configuration adds an SSD1306 OLED display for local readout.

## Features

- **WiFi-enabled:** Integrates with Home Assistant.
- **Accurate weight measurement:** Uses HX711 and a load cell.
- **Optional OLED display:** Shows weight, date and time.
- **Easy calibration:** Instructions included in the YAML files.
- **Restart switch:** Remotely reboot the device from Home Assistant.

---

## Hardware Required

- ESP32 development board
- HX711 load cell amplifier
- Load cell
- (Optional) SSD1306 OLED display (I2C, 128x64 recommended)
- Jumper wires, breadboard or PCB
- (Optional) 3D-printed or custom scale enclosure

---

## Wiring Diagram

See `scale.png`

---

## Configuration Files

### 1. `scale.yaml` (Basic WiFi Scale)

- For a simple WiFi-connected scale.
- No display; all readings are sent to Home Assistant.
- Sensors:
  - Weight (HX711, GPIO18/19)
  - ESP32 chip model (text sensor)
- Includes a restart switch.
- Calibration instructions in comments.

### 2. `scale-with-oled.yaml` (WiFi Scale with OLED Display)

- All features of `scale.yaml`.
- Adds SSD1306 OLED display (I2C: SDA=GPIO21, SCL=GPIO22).
- Displays:
  - Current weight (in grams or kg depening on yaml setting)
  - Current date and time
- Custom fonts for improved readability.
  - Add fonts to /esphome/fonts folder in Home Assistant

---

## Setup Instructions

1. **Clone this repository** and open in your favorite editor.

2. **Wiring:**  
   Follow the wiring diagram in `scale.webp` for your chosen configuration.

3. **Fonts (for OLED version):**  
   Ensure the `fonts/arial.ttf` file is present in the `fonts/` directory.

4. **Secrets:**  
   Create a `secrets.yaml` file with your WiFi credentials:
   ```yaml
   iot_wifi_ssid: "YOUR_WIFI_SSID"
   iot_wifi_password: "YOUR_WIFI_PASSWORD"
   ```

5. **Flashing:**
   - Install [ESPHome](https://esphome.io/guides/installing_esphome.html).
   - Flash the desired YAML to your ESP32:
     ```sh
     esphome run scale.yaml
     # or for OLED version:
     esphome run scale-with-oled.yaml
     ```

6. **Calibration:**  
   - Place a known weight on the scale and follow the calibration comments in the YAML file.
   - Adjust the `calibrate_linear` filter as needed for accurate readings.

7. **Home Assistant Integration:**  
   - The device will auto-discover in Home Assistant if on the same network.

---

## Usage

- View weight and device status in Home Assistant.
- (OLED version) See real-time weight, WiFi signal, and time on the display.
- Use the "Restart device" switch in Home Assistant to reboot the ESP32 remotely.

---

## Troubleshooting

- **No readings?** Double-check wiring, especially HX711 and I2C connections.
- **Display issues?** Confirm the OLED address (default is `0x3C`) and wiring.
- **Calibration off?** Repeat the calibration steps with a known weight.
