# ESP32-CAM Face Unlock — Solenoid Lock Demo 🔐📷

[![Project Status](https://img.shields.io/badge/status-proof%20of%20concept-blue)]()
[![License](https://img.shields.io/badge/license-MIT-green)]()

**This repository demonstrates unlocking a solenoid lock using face detection on an ESP32-CAM.**  
The ESP32-CAM performs face detection locally; when a recognized face (or any detected face, depending on your firmware settings) is found, the board triggers a relay that energizes a solenoid lock (representing a door lock).

> ⚠️ Safety note: This project uses mains-level batteries and electromechanical components. Follow safe wiring and insulation practices. See the **Safety** section.

---

## 🔎 What’s included
- `code/` — firmware source (face detection + relay control).  
- `docs/circuit-diagram.png` — wiring and circuit diagram.  
- `hardware/components-list.txt` — parts used in the prototype.  
- `docs/demo_video.mp4` and photos to show the working prototype.

> I may update the firmware and hardware files over time — check the `code/` and `docs/` folders for the latest.

---

## 📦 Components (prototype)
ESP32-CAM
Relay Module (5V)
Solenoid lock (12V)
2 × LED (status indicators)
Breadboard
12V Battery
7805 Voltage Regulator (12V → 5V)
100µF 16V Capacitor (optional)


---

## 🧩 Quick overview (how it works)
1. The ESP32-CAM runs face detection on the camera frames.
2. When a face is detected (or a configured known face), the firmware sets a GPIO HIGH to activate the relay.
3. The relay switches the 12V supply to the solenoid lock — the lock actuates (unlocks) while energized.
4. LEDs provide simple status feedback (e.g., detection / locked / unlocked).

---

## 🔧 Wiring (prototype summary)
- **Power:**
  - 12V battery → 7805 Vin
  - 7805 Vout → 5V rail (power for relay module and ESP32-CAM 5V pin)
  - 12V battery → solenoid lock V+ (solenoid ground goes to battery negative)
- **ESP32-CAM:**
  - 5V → 5V pin (or +5V on the board), GND → GND
  - IO GPIOx → Relay module IN pin (choose a GPIO that is safe for use with camera functions; see `code/README-FIRMWARE.md`)
- **Relay & Solenoid:**
  - Relay Vcc → 5V
  - Relay GND → GND
  - Relay NO (normally open) → solenoid +12V
  - Relay COM → 12V battery + (or vice versa depending on relay pins)
- **LEDs:**
  - Status LEDs connected via current-limiting resistors to chosen GPIOs

> ⚠️ The above is a summary. Refer to `docs/circuit-diagram.png` for the exact pin mapping. If your relay is a module with an optocoupler, follow the module wiring recommendations (some modules expect JD-VCC separation).

---

## 🖥️ Flashing / Run
1. Install Arduino IDE / PlatformIO and ESP32 board support.
2. Open `code/face_unlock.ino` (or PlatformIO workspace).
3. Set the correct board: **AI-Thinker ESP32-CAM** (or your variant).
4. Set the upload method / serial parameters according to your board.
5. Flash and open the Serial Monitor to see logs (baud rate typically 115200).

The firmware logs detection events; when a face is detected the relay GPIO toggles and unlocks the solenoid for a configurable duration.

---

## 🔐 Privacy & Security
- Face detection here is performed **locally on the ESP32-CAM** — no cloud services required.
- If you later add face recognition that stores templates, keep templates encrypted and be explicit about consent.
- This demo is for educational/prototyping use only — do **not** use it in production security systems without appropriate safeguards, backups, and tested fail-safes.

---

## 🛠️ What you can upload if code is private
If parts of the code are proprietary, still include:
- a `README-FIRMWARE.md` describing firmware modules and APIs
- a `firmware-interface.txt` listing serial commands/JSON formats
- circuit diagrams, photos, and demo videos
- compiled binaries (if you prefer not to share source) — label clearly

---

## ✅ Suggestions / Next steps
- Add EMG or RFID fallback for multi-factor unlocking.
- Replace breadboard prototype with a proper MOSFET / driver circuit (for direct solenoid control) and a dedicated power regulator.
- Add a webUI on ESP32 if you want remote status/management (remember auth + TLS concerns).

---

## 📜 License
This repository is available under the **MIT License** — see `LICENSE` for details.

---

## 👤 Author
**Abdelkerim El Bani** — Final year / hobby projects.  
Contact: add your preferred contact or GitHub profile link.

---

