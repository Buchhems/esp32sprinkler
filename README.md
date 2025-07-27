# 🌱 ESP32 Smart Sprinkler Controller

An intelligent, time-based irrigation system powered by ESPHome and ESP32. This project automates garden watering using GPIO-controlled valves, rain pause logic, and a web interface for configuration and monitoring.
You can get a Esp32 Relay Board with up to 8 relays quite cheap on Aliexpress for as little as €30.
![82607cfc8dc6e7aae33cdee51993b18b29d1bcfd-222773943](https://github.com/user-attachments/assets/2297f28c-2e1d-4b5c-b5d2-f7196104a18f)

To power your valves or pumps you need the equivalent power supply (in my case 24V AC) plus the necessary 5V DC power supply.
The 5V DC power supply powers the board itself (green screwable connectors on top of the board). Alternatively you can power it with 7-30V DC (different connector).
The power supply for the valves needs to be connected directly to the relays (outgoing power cable from PS to green COM connector, NC => valve, - from PS => arriving power cable from valves).

---

## 🚀 Features

- 💧 Multi-zone irrigation: Supports 5 watering zones (sprinklers + drip irrigation)
- ⏰ Time-based scheduling: Custom start time and interval between watering days
- 🌧 Rain pause logic: Temporarily suspend watering for configurable days
- 📊 Real-time status: Displays current valve, last watering days, and system uptime
- 🖥 Web interface: Control and monitor via browser with authentication
- 🔧 Manual override: Start/stop sequence, emergency shutoff, and system restart
- 📅 SNTP time sync: Ensures accurate scheduling using NTP servers

---

## 🧠 System Overview

| Component        | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| **ESP32 Board**  | `esp32dev` used as the core controller                                      |
| **Valves**       | 5 GPIO-controlled valves for different garden zones                         |
| **Rain Pause**   | Toggleable pause with duration tracking                                     |
| **Web Server**   | Accessible via port 80 with login credentials                               |
| **Time Sync**    | Uses SNTP with European timezone settings                                   |
| **Globals**      | Tracks system state, valve index, rain pause, and watering history         |
| **Scripts**      | Modular logic for starting/stopping sequences and handling rain pause       |
| **Sensors**      | Uptime, next watering calculation, total sequence duration                  |
| **Buttons**      | Manual controls for sequence, emergency stop, and restart                   |

---

## 💻 Web Interface

- **Authentication**:  
  - Username: `root`  
  - Password: `abc`

- **Fallback Access Point**:  
  - SSID: `Sprinkler Fallback`  
  - Password: `fallback123`

- **Controls**:
  - ▶️ Start/Stop watering sequence
  - 🛑 Emergency valve shutdown
  - 🌧️ Rain pause toggle
  - 🔄 System restart

- **Status Display**:
  - 🚿 Current valve running
  - 🌧️ Rain pause status
  - 🕒 Days until next watering
  - 📅 Last watering days
  - ⏱️ System uptime
  - 🌐 Device IP address

---

## 🧩 Customization

To add more valves, simply extend the configuration:

```yaml
- platform: gpio
  pin: GPIO14
  name: "C1 💧 Greenhouse"
  id: valve_5
  icon: "mdi:greenhouse"
