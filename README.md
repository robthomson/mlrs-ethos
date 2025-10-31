# MLRS mBridge-over-CRSF Tool for Ethos

A Lua utility for **Ethos transmitters** that provides a graphical configuration interface for **MLRS (Modular Long Range System)** devices over the **CRSF protocol** using the *mBridge* layer.

This script allows you to **view, edit, and save MLRS parameters** directly from your Ethos radio without connecting to a computer or using the MLRS web configurator.

---

## ✨ Features

- 📡 **Direct MLRS integration** via CRSF (Crossfire) telemetry.
- 🧭 **Automatic discovery** of device parameters and metadata.
- 💾 **On-radio save** — write changes directly to flash.
- 🔁 **Smart persistent progress loader** for seamless UX (no flicker between save/reboot/reload).
- ⚙️ **Auto-reconnect** after module reboot or power cycle.
- 🧱 **Fully dynamic UI** — fields are built automatically from MLRS parameter descriptors.

---

## 🛰️ What Is MLRS?

**MLRS (Modular Long Range System)** is an open-source, low-latency, long-range RC link used by the FPV and RC communities.  
It supports both RC control and telemetry and is highly customizable, allowing flexible configuration of parameters such as power, frequency, failsafe, etc.

Project links:

- 🌍 [Official MLRS GitHub](https://github.com/AlessandroAU/ExpressLRS/tree/mlrs)
- 💬 [Discord & Community](https://discord.gg/expresslrs)

---

## 🧩 What Is mBridge?

**mBridge** is a lightweight bridge layer inside MLRS that exposes its internal parameters over the CRSF protocol.  
This script communicates with mBridge by sending and receiving `A0+CMD` packets over CRSF telemetry.  
Each parameter (or "item") is described by a set of structured frames (`ITEM`, `ITEM2`, `ITEM3`), from which the script dynamically builds the Ethos form fields.

---

## 🕹️ Installation

1. Copy `main.lua` into your transmitter’s **Ethos → Tools → Scripts** folder.  
   Example:  
```/SCRIPTS/TOOLS/MLRS/main.lua```


2. Restart your radio or reload the tools list.

3. In Ethos:
- Open **Model → Tools**
- Add a new tool
- Select **MLRS**

4. Power up your MLRS module.  
The script will automatically connect, read the parameter list, and show configuration fields.

---

## 💾 Saving Settings

- After editing values, tap **Save** at the bottom of the form.
- The script will:
1. Send the `PARAM_STORE` command to MLRS.
2. Keep the progress loader open while the module reboots.
3. Automatically reconnect and reload the parameters.
- The loader text will change from “Writing…” → “Reconnecting…” → “Complete” once ready.

---

## 🧠 Troubleshooting

- **Not all parameters appear?**  
Wait a few seconds — some metadata arrives after the main list.  
If persistent, ensure your CRSF link is stable and firmware up to date.

- **Progress dialog flickers or closes early?**  
This version uses a *persistent loader* that stays visible through save → reboot → reconnect.  
If you still see flicker, verify that your Ethos version supports `form.openProgressDialog()` properly.

- **No MLRS detected?**  
Make sure the module is powered and connected via CRSF UART.

---

## 🧑‍💻 Development Notes

- Written entirely in **Lua** for the Ethos scripting API.
- Compatible with both internal and external MLRS modules using CRSF telemetry (e.g. TX16S, X20, etc.).
- All form fields are created dynamically from parameter frames.
- Implements a **single persistent progress dialog** managed by `progressEnsure()` for smoother user flow.

---

## 📜 License

GPL-3.0 © 2025 Rob Thomson  
See [LICENSE](LICENSE) for details.

---

## 🧩 Credits

- **Rob Thomson** — development and Ethos integration  
- **MLRS / mBridge developers** — for open protocol and reference implementations  
- **Ethos Team** — for providing a flexible Lua interface

---
