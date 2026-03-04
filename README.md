# ⚡ deathframe

> ESP32-based Wi-Fi deauthentication tool with OLED display.  
> One button. One purpose. Authorized testing only.

---

## ⚠️ Legal Disclaimer

**This tool is strictly for use in authorized, controlled test environments.**  
Using this on networks you don't own or without **explicit written permission** is illegal in most countries (§202c StGB in Germany, Computer Fraud and Abuse Act in the US, etc.).  
The author takes no responsibility for misuse. **You have been warned.**

---

## 🔩 Hardware Required

| Component | Details |
|-----------|---------|
| ESP32 | Any variant (DevKit, WROOM, etc.) |
| OLED Display | SSD1306 128x64, I2C |
| Button | Momentary push button (or use built-in BOOT button) |

**Wiring:**

```
OLED SDA  →  GPIO 21
OLED SCL  →  GPIO 22
OLED VCC  →  3.3V
OLED GND  →  GND

Button    →  GPIO 0 + GND (or use built-in BOOT button)
```

---

## 📦 Dependencies

Install via Arduino Library Manager:

- `Adafruit SSD1306`
- `Adafruit GFX Library`

**Board:** ESP32 by Espressif (via Arduino Board Manager)  
`https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json`

---

## 🚀 How to Use

1. Flash `nexus_jammer.ino` to your ESP32
2. Boot screen shows → device is ready
3. **Press button** → scans all nearby networks → starts sending deauth frames to all detected APs
4. OLED shows: network count + total packets sent
5. **Press button again** → stops, shows summary

```
┌─────────────────┐
│  [ JAMMING ]    │
│  Networks : 7   │
│  Pkts sent: 420 │
│                 │
│  Press to STOP  │
└─────────────────┘
```

---

## ⚙️ Configuration

Edit these values at the top of `nexus_jammer.ino`:

```cpp
#define MAX_APS         20    // max networks to track
#define DEAUTH_PER_AP   10    // frames sent per AP per cycle
#define SCAN_INTERVAL   15000 // re-scan interval in ms
```

---

## 🧠 How It Works

The ESP32 uses raw 802.11 frame injection (`esp_wifi_80211_tx`) to broadcast **deauthentication frames** — a standard part of the Wi-Fi protocol used by access points to disconnect clients. By spoofing the AP's MAC address and broadcasting to `FF:FF:FF:FF:FF:FF`, all clients on that network receive the disconnect signal.

This is a known vulnerability in WPA2 (fixed in WPA3 with Management Frame Protection / MFP).

---

## 📁 Repo Structure

```
nexus_jammer/
├── nexus_jammer.ino   # Main sketch
└── README.md          # This file
```

---

## 🤝 Contributing

PRs welcome. Ideas:
- [ ] Per-channel hopping optimization
- [ ] Target whitelist/blacklist
- [ ] Packet counter history graph on OLED
- [ ] WPA3/MFP detection warning

---

## 📜 License

MIT — use freely, responsibly, and legally.

---

<div align="center">
<sub>Built by <a href="https://github.com/Nexus007008">Nexus_</a> · For educational purposes only</sub>
</div>
