# Blank DG-LAB

![](https://img.shields.io/badge/Minecraft-26.1.x-green?style=for-the-badge) ![](https://img.shields.io/badge/Loader-Fabric-d6c4ff?style=for-the-badge) ![](https://img.shields.io/badge/License-All_Rights_Reserved-blue?style=for-the-badge)

**Connect your DG-LAB Coyote 3.0 device to Minecraft for real-time, game-driven haptic feedback.**

Blank DG‑LAB is a client‑side Fabric mod for Minecraft 26.1 that transforms in‑game events into physical haptic pulses via the DG‑LAB Coyote 3.0 device. Feel every hit, every fall, every close call – all through the official SOCKET V2 protocol, with no external backend required.

> **This is a haptic / biofeedback peripheral mod.** It contains no sexual themes, NSFW elements, or age‑restricted material. All feedback is purely based on in‑game damage and player actions.

***

## ✨ Features

### 🔗 Connection

*   **QR Code Pairing** – Embedded WebSocket server generates a QR code; scan with the DG‑LAB App to connect instantly
*   **No External Backend** – The mod runs its own WebSocket server internally – no Node.js or separate backend needed
*   **Auto Port Detection** – Automatically finds available ports, with a randomize button for quick changes
*   **Reconnection Support** – Automatically attempts to reconnect if the app disconnects
*   **IP Input Sanitization** – Handles Chinese punctuation and full‑width numbers in manual IP entry

### ⚡ Damage & Status Detection

*   **Combat Damage** – Configurable multiplier, min/max strength, and pulse duration per damage type
*   **10 Damage Types** – Separate settings for Generic, Projectile, Fire, Fall, DoT, Magic, Explosion, Drown, Environmental, and Death
*   **Low Health Trigger** – Continuous pulses when below max health (configurable strength per 10% lost)
*   **Low Hunger Trigger** – Continuous pulses when below max hunger (configurable strength per 10% lost)
*   **Absorption Hearts** – Golden apple absorption is counted as effective health
*   **Creative/Spectator Immunity** – No haptics in creative or spectator modes
*   **Pause Detection** – No health/hunger checks when the game is paused (ESC)

### 📊 Strength System

*   **Triple Limit System** – Effective limit = min(APP limit, in‑game config limit)
*   **A/B Channel Independent Limits** – Separate tracking and notifications for each channel
*   **Float Precision Stacking** – All damage contributions use float arithmetic, rounded only at final output
*   **Auto Clamping** – Strength never exceeds the effective limit

### 🖥️ HUD Display

*   **4 Visual Styles** – BAR, WAVE, PULSE, NUMBER
*   **Draggable Position** – In‑game HUD editor with drag‑and‑drop positioning
*   **Adjustable Scale** – 0.5× to 2.0× scaling
*   **Smooth Transitions** – Dynamic lerp animation: fast rise on damage, gradual fall on recovery
*   **Connection Status** – Text indicators showing "✓ Connected" or "✗ Disconnected"
*   **Pause‑Aware Animation** – Wave and pulse animations freeze when the game is paused
*   **Semi‑transparent Background** – Light overlay for readability on any scene

### ⚙️ Configuration (YACL)

*   **No ModMenu Required** – Press B to open the main menu, or access YACL config directly
*   **Per‑Scenario Settings** – Independent multiplier, min, max, and duration for each damage type
*   **Preset System** – Save, load, import, and export strength presets (shader‑pack style list with scrollbar)
*   **Built‑in Presets** – Light, Medium, Heavy, Extreme – ready to use out of the box
*   **Confirmation Dialogs** – Warns when importing presets that exceed current limits

***

## 📋 Requirements

| Software                   |Version                        |
| -------------------------- |------------------------------ |
| Minecraft                  |26.1 / 26.1.1 / 26.1.2         |
| Fabric Loader              |≥ 0.18.0                       |
| Fabric API                 |*                              |
| YetAnotherConfigLib (YACL) |≥ 3.9.0+26.1-fabric (Required) |
| Java                       |≥ 25                           |

**Hardware:**

*   DG‑LAB Coyote 3.0 device
*   A mobile phone with the official DG‑LAB 3.0 App

***

## 🚀 Quick Start

1.  **Install the mod** – Drop `blankdglab-<version>.jar` into your `mods` folder
2.  **Open the mod** – Press `B` in‑game to open the main menu
3.  **Connect your device** – Click "QR Code Connect", then scan the QR code with the DG‑LAB App on your phone
4.  **Set APP limits** – In the DG‑LAB App, go to SOCKET Control and tap the `+` button on both A and B channel limits until they reach your desired maximum
5.  **Play!** – The HUD will show connection status, and in‑game events will trigger haptic pulses

***

## ⚙️ Configuration

All settings are accessible via **`B` key** → main menu → settings, or directly through YACL.  
Configuration is saved to `config/blankdglab.json`.

### Connection Settings

| Setting           |Description                                      |Default |
| ----------------- |------------------------------------------------ |------- |
| Server Port       |Embedded WebSocket server port                   |<code>8877</code> |
| Manual IP         |Override auto‑detected IP (leave empty for auto) |<em>(empty)</em> |
| Max Strength      |Maximum pulse strength (game‑side cap)           |<code>40</code> |
| Min Strength      |Minimum pulse strength                           |<code>0</code> |
| Sync A/B Channels |Send combined strength to both channels          |<code>true</code> |

### Damage Feedback (per type)

Each damage type has independent settings:

| Setting        |Description                                 |
| -------------- |------------------------------------------- |
| Enable         |Toggle haptic feedback for this damage type |
| Strength A / B |Pulse strength for channel A and B          |
| Pulse Duration |Duration of the pulse in milliseconds       |

**Supported damage types:** Generic, Projectile, Fire, Fall, DoT, Magic, Explosion, Drown, Environmental, Death, Attack, Block Break

### Status Feedback

| Setting                   |Description                  |Default |
| ------------------------- |---------------------------- |------- |
| Low Health Feedback       |Pulse when below max health  |<code>true</code> |
| Low Health Strength / 10% |Strength per 10% health lost |<code>5</code> |
| Low Health Pulse Interval |Milliseconds between pulses  |<code>2000</code> |
| Low Hunger Feedback       |Pulse when below max hunger  |<code>false</code> |
| Low Hunger Strength / 10% |Strength per 10% hunger lost |<code>3</code> |
| Low Hunger Pulse Interval |Milliseconds between pulses  |<code>3000</code> |

### HUD Settings

| Setting      |Description                 |Default            |
| ------------ |--------------------------- |------------------ |
| Show HUD     |Toggle HUD visibility       |<code>true</code>  |
| HUD Style    |BAR / WAVE / PULSE / NUMBER |<code>BAR</code>   |
| HUD Layout   |VERTICAL / HORIZONTAL       |<code>VERTICAL</code> |
| HUD Position |Drag‑and‑drop in HUD editor |Left, 30% from top |
| HUD Scale    |0.5× – 2.0×                 |<code>1.0</code>   |

***

## 📡 How it Works

```
Minecraft → Embedded WebSocket Server → DG‑LAB App (phone) → Bluetooth → Coyote Device
```

The mod embeds a WebSocket server that implements the DG‑LAB SOCKET V2 protocol. When you scan the QR code, the DG‑LAB App connects directly to the mod – no external backend or Node.js server needed. The mod sends structured strength and pulse commands, and the App relays them to the device via Bluetooth.

***

## ❓ FAQ

**Q:Is this mod allowed on servers?**  
A:Yes. It is client‑side only and does not interact with server logic. No server installation is required.

**Q:Will it get me banned?**  
A:No. It does not give any unfair advantage and does not modify server packets.

**Q:Do I need to run a separate backend?**  
A:No. The mod has its own embedded WebSocket server. Just scan the QR code and connect.

**Q:Why are the A/B channel limits 0 in the APP?**  
A:The SOCKET V2 protocol does not provide a command to set APP‑side limits. After connecting, go to the APP's SOCKET Control screen and manually tap the `+` button on both A and B channel limits to set them to your desired maximum.

**Q:Can I use it with other haptic devices?**  
A:Currently only the DG‑LAB Coyote 3.0 is supported via the official SOCKET V2 protocol.

**Q:I found a bug / have a suggestion – where can I report?**  
A:Please open an issue on the GitHub issue tracker.

***

## 📜 License

This mod is licensed under the **GNU Lesser General Public License v3.0 (LGPL-3.0)**. See `LICENSE` file for details. _(The DG‑LAB backend is a separate project and uses its own license.)_

***

## 🤝 Acknowledgements

*   DG‑LAB for providing the open‑source SOCKET V2 communication protocol
*   The Fabric team for the excellent modding toolchain
*   YetAnotherConfigLib for the clean configuration GUI framework

***

**Enjoy your new level of immersion – responsibly!**

**Last updated: May 2026 | Supports Minecraft 26.1.x**
