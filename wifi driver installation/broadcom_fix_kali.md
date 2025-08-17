
# ✅ How I Installed Broadcom Wi-Fi Driver on Kali Linux (2024/2025)

---

## 🧭 1. Check Initial Problem

- Wi-Fi not working (`wlan0` not showing)
- `modprobe wl` gives:  
  ```
  modprobe: FATAL: Module wl not found...
  ```
- No kernel headers for current kernel version (e.g., `6.6.15-amd64`)

---

## 🧹 2. Clean Start: Update System

```bash
sudo apt update && sudo apt full-upgrade -y
```

---

## 🏗️ 3. Install Kali Default Kernel + Headers

```bash
sudo apt install linux-image-amd64 linux-headers-amd64
```

This installs the **official supported kernel and headers** (`6.6.x-kali1`, etc.)

---

## 🔁 4. Reboot into New Kernel

```bash
sudo reboot
```

After reboot, check your kernel:

```bash
uname -r
```

✅ Should say something like:
```
6.6.0-kali1-amd64
```

---

## 📦 5. Install Broadcom Driver

```bash
sudo apt install broadcom-sta-dkms
```

---

## 🧠 6. Load the Broadcom `wl` Module

```bash
sudo modprobe -r b43 bcma brcmsmac
sudo modprobe wl
```

✅ This removes conflicting modules and activates the correct one.

---

## 🚀 7. Reboot Again (Optional)

```bash
sudo reboot
```

Then check Wi-Fi:

```bash
iwconfig
# or
nmcli dev wifi list
```

🎉 You should now see `wlan0` and nearby networks!

---

## 🔐 8. Optional: Monitor Mode (for Wi-Fi tools)

Enable monitor mode for hacking tools:

```bash
sudo airmon-ng start wlan0
iwconfig
# You should see wlan0mon in Mode:Monitor
```

To return to normal (managed) mode:

```bash
sudo ip link set wlan0mon down
sudo iw dev wlan0mon set type managed
sudo ip link set wlan0mon up
```

---
