<h1 align="center">ZeroWave_FlipperZero-BlueJammer</h1>
<img width="1280" height="721" alt="image" src="https://github.com/user-attachments/assets/07208d89-435e-45f5-88f0-262318754507" />


<h3 align="center">by @emensta</h3>
<h3 align="center">⚠️Jamming is ILLEGAL! Educational purposes only!</h3>

<p align="center">
  <a href="https://github.com/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer/stargazers">
    <img src="https://img.shields.io/github/stars/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer?style=for-the-badge&color=yellow" alt="GitHub Stars"/>
  </a>
  <a href="https://github.com/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer/network/members">
    <img src="https://img.shields.io/github/forks/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer?style=for-the-badge&color=orange" alt="GitHub Forks"/>
  </a>
  <a href="https://github.com/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer/watchers">
    <img src="https://img.shields.io/github/watchers/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer?style=for-the-badge&color=blue" alt="GitHub Watchers"/>
  </a>
  <a href="https://hits.sh/github.com/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer/">
    <img src="https://hits.sh/github.com/EmenstaNougat/ZeroWave_FlipperZero-BlueJammer.svg?style=for-the-badge&color=brightgreen" alt="Repo Views"/>
  </a>
</p>

---

## 🧩 Overview

**ZeroWave_FlipperZero-BlueJammer** is the official firmware port of the **[ESP32‑BlueJammer](https://github.com/EmenstaNougat/ESP32-BlueJammer)** project, built to run on the **[ZeroWave extension board](https://www.elecrow.com/flipper-zero-zerowave-extension-board.html)** for the Flipper Zero.
<img width="1184" height="549" alt="image" src="https://github.com/user-attachments/assets/df4a8f9e-bf8a-46fc-823f-87e038e8ae3b" />
This project allows you to use the Flipper Zero as a user‑interface and control hub for the jamming hardware, enabling selectable modes via the directional pad while managing power safely.

The ZeroWave is designed as an **educational tool** to explore RF communication, protocol interference, and hardware control, under the strict caveat of responsible usage and full legal compliance.

---

## 🧠 Features

- 🎮 **Flipper Zero App Integration**  
  Use your Flipper Zero directional pad to select modes:  
  - **Up** → Bluetooth  
  - **Right** → Bluetooth Low Energy (BLE)  
  - **Down** → WiFi  
  - **Left** → RC (remote‑control systems)  
  - **OK** → Idle (no jamming)  
  - **Back** → Exit the app & safely power down the ZeroWave board  

- ⚡ **Managed 5 V Rail Activation**  
  The firmware handles enabling the 5 V rail that powers the RF modules, ensuring stable voltage and safe operation.

- 🔐 **Dual nRF24 Interface Support**  
  Supports two RF modules (GT24‑Mini), enabling effective channel interferance across the whole 2.4 GHz band.

  **Example device‑types that can be affected include:**

  - Bluetooth speakers (wireless audio devices)
  
  - Smartwatches and fitness trackers using Bluetooth or BLE
  
  - IoT devices operating in the 2.4 GHz band (smart plugs, sensors, smart locks)
  
  - WiFi devices such as wireless security cameras and routers set on the 2.4 GHz channel
  
  - Wireless gamepads/controllers (e.g., Bluetooth or 2.4 GHz dongle gamepads - DualShock, DualSense, Xbox, etc. controllers) 
  
  - Remote‑control (RC) drones, cars, toys that operate at ~2.4 GHz
  
  - Wireless keyboards/mice or proprietary peripherals using 2.4 GHz dongles

  - And way more, in short "ANYTHING OPERATING ON 2.4GHz!"

- 📡 **Multi‑Mode Jamming Capability**  
  By selecting different modes, you can experiment with jamming Bluetooth classic, BLE, WiFi, and RC frequencies, all on controlled hardware setup, for learning purposes.

---

## 🧰 Required Hardware

| Component                                | Description / Notes                              | Link (affilate)                                                      |
|------------------------------------------|--------------------------------------------------|----------------------------------------------------------------------|
| **ZeroWave Extension Board**            | The custom PCB that hosts the C3-Supermini and RF modules | [Elecrow ZeroWave Board](https://www.elecrow.com/flipper-zero-zerowave-extension-board.html) |
| **ESP32C3‑Supermini**                   | The MCU running the firmware                      | [AliExpress](https://s.click.aliexpress.com/e/_c39ycjND)             |
| **2× GT24‑Mini nRF modules**            | RF modules for jamming                            | [AliExpress](https://s.click.aliexpress.com/e/_c3i1ugBz)             |
| **RP‑SMA Connector (Right Foot 13.5, SMA‑KE Inner Hole)** | Antenna connection              | [AliExpress](https://s.click.aliexpress.com/e/_EwDocU4)              |
| **Capacitor Set (0805, 720pcs, 36 Values)** | For decoupling & signal stability             | [AliExpress](https://s.click.aliexpress.com/e/_ExudcGk)              |
| **U.FL IPX Connector**                  | For antenna cabling                               | [AliExpress](https://s.click.aliexpress.com/e/_EHvWoP2)              |
| **Male & Female Pin Headers**           | For board headers / connections                   | [AliExpress](https://s.click.aliexpress.com/e/_EygfqSo)              |
| **U.FL Pigtails**                       | Antenna cables                                    | [AliExpress](https://s.click.aliexpress.com/e/_Ezq6xJO)              |

> ⚠️ Ensure proper antenna configuration and safe soldering practices. The RF modules and 2.4 GHz band are sensitive; improper setup can cause unwanted interference or hardware damage.

---

## ⚙️ Installation & Setup

### Step 1: Flash the Firmware  
Download the latest `.bin` from the Releases section of the repo and flash it using `esptool.py` or a suitable ESP32 flash tool.

Open up this path: ZeroWave_FlipperZero-BlueJammer-main\ZeroWave_FlipperZero-BlueJammer-main\ZeroWave-firmware_files

Out of this folder, continue with the flash below:

Make sure to change the COM port (COM16) to the corresponding port that your system recognizes it at!
```bash
python -m esptool --chip esp32c3 --port COM16 --baud 115200 write_flash ^
  0x0 ZeroWave.ino.bootloader.bin ^
  0x8000 ZeroWave.ino.partitions.bin ^
  0x10000 ZeroWave.ino.bin

````

### Step 2: Connect to the Flipper Zero

* Insert the ZeroWave board into your Flipper Zero’s expansion port.
* Ensure it’s properly seated and powered.
* On the Flipper Zero, open the “ESP32‑BlueJammer” app (installed as part of the overall ecosystem).

### Step 3: Use the App

Use the directional pad to select your jamming mode:

```
↑ = Bluetooth  
→ = BLE  
↓ = WiFi  
← = RC systems  
OK = Idle mode (no jamming)  
Back = Exit & power down board  
```
<img width="2160" height="1080" alt="image" src="https://github.com/user-attachments/assets/ae6c35e2-0b2b-4707-91e5-ed9c3225f4f6" />
The firmware will handle powering down the 5 V rail safely when you exit, ensuring your hardware is not left in an unsafe state.

- This application interface was created using Lopaka (see https://lopaka.app), a browser‑based graphics‑editor tool tailored for embedded systems (including platforms such as Flipper Zero, Arduino, ESP32, STM32). It enables pixel‑perfect drawing of shapes, text and images and then auto‑generates ready‑to‑use C/C++ code for display libraries like U8g2, AdafruitGFX or the Flipper UI framework. 
I have used Lopaka to rapidly prototype and export the menu screen you interact with on the device, ensuring a consistent look and feel across hardware and software layers.

---

## 🧩 Technical Details & Architecture

* **Platform:** ESP32‑C3 SuperMini (32‑bit RISC‑V core)
* **SPI Interfaces:** connected to both nRF24 modules
* **Voltage Management:** 5 V rail activation via Flipper Zero expansion + full firmware control
* **App Interface:** Flipper Zero directs commands communicating with the firmware
* **Channel Hopping Logic:** Firmware interferes through a defined set of channels for each mode (Bluetooth classic, BLE, WiFi, RC) for maximal coverage.

### Firmware Structure Highlights

* `ZeroWave.cpp` - Entry point that initializes SPI bus, dual nRF24 modules and orchestrates mode switching & logics.
* `ZeroWaveBlueJammer.h` / `ZeroWaveBlueJammer.cpp` - Core jamming logic: channel sets, interferance routines and mode‑specific behaviour.
* `FlipperToBoardCom.h` / `FlipperToBoardCom.cpp` - Communication interface between the Flipper Zero and the expansion board: handles D‑pad commands, mode selection and status feedback.
* `Powermanagement.h` / `Powermanagement.cpp` - Manages the 5 V rail: safe powering‑on of the hardware, and clean powering‑off when exiting the app.

---

## 📜 Legal & Ethical Considerations

Use of jamming equipment is **highly regulated** (and in many jurisdictions outright illegal)!

> **Please note:** This firmware is provided for educational and research purposes only. The author ([@emensta](https://github.com/EmenstaNougat)) assumes no responsibility for misuse, illegal activity, or resulting consequences.

---

## 💬 Feedback

* Found a bug, improvement, or idea? Please open an **Issue** in the repo.

---

## ⭐ Support & Community

If you like the project and want to support it, please consider starring the repo, every star helps spread awareness and keeps the momentum going for future work.

---

## Discord

You can join my Discord server [here](https://discord.gg/emensta)!

## Portfolio and all my links

Here you can visit my Portfolio, you’ll find everything that you’re looking for [here](https://emensta.pages.dev)!

## Support me

Via [this link](https://ko-fi.com/emensta), you can leave a tip to keep me motivated developing future projects! Thank you for your support :)

<h1 align="center">DISCLAIMER</h1>

<h4 align="center">Please note that the use of this tool is entirely at your own risk. It is intended strictly for educational purposes and should not be used for any illegal or unethical activities. Jamming is illegal and can get you in big trouble!</h4>  
<h4 align="center">I’m not responsible for your actions!</h4>
