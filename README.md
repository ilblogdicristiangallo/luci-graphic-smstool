# luci-graphic-smstool

**LuCI Graphic SMS Tool** is a complete, lightweight, and powerful Web UI for OpenWrt to manage SMS directly from your 3G/4G/5G USB or PCIe modems (e.g., ZTE, Quectel, Fibocom, Huawei). 

| OpenWrt | Package | Version | Extra dependencies |
|---------|---------|---------|--------------------|
| **24.x** | `.ipk` (`opkg`) | `1.1.0-1` | `luci-lua-runtime`, `luci-compat`, `sms-tool`, `curl` |
| **25.x** | `.apk` (`apk`) | `1.1.0-r1` | `sms-tool`, `curl` |

*(LuCI views and controllers are fully compatible with both OpenWrt 24 and 25 (`PKG_ARCH:=all`). OpenWrt 24 does not ship a Lua runtime with LuCI by default, so it requires `luci-lua-runtime` and `luci-compat`.)*

---

## ✨ Overview & Features

This package transforms your OpenWrt router into a smart SMS hub with advanced capabilities, without using the command line.

- 🔄 **Dual Modem Backend:** Native integration with both **sms_tool** (QMI / Serial AT) and **ModemManager** (`mmcli`). You can switch dynamically depending on your network setup.
- 💬 **Inbox & Messaging:** Read, preview, send, and delete messages with multi-storage support (SIM `SM`, Modem `ME`, or ModemManager daemon).
- 🤖 **Telegram Notification Daemon:** An automated background service that silently monitors your inbox and forwards any new incoming SMS directly to your Telegram chat, complete with emojis and permanent duplicate filtering.
- 📱 **Contacts Directory:** A built-in address book to save, edit, and quickly pick phone numbers.
- ⚙️ **Advanced Settings & SMSC:** Read and modify your SMS Center (SMSC) number. Features a smart fallback that queries `/dev/ttyUSB2` if the main interface is locked by ModemManager.
- 🧙‍♂️ **Interactive Setup Wizard:** A guided initial setup that automatically scans for available serial AT ports, tests modem responsiveness live, and configures the correct country prefix and memory storage in seconds.

---

## 📸 Interface Preview

Take a look at the LuCI Graphic SMS Tool interface, from the initial Setup Wizard to the Inbox, Contacts, Telegram configuration, and Settings pages:

<div align="center">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot2.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot3.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot4.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot5.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot6.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot7.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot8.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot9.png?raw=true" width="800" style="margin-bottom: 15px;">
  <img src="https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot10.png?raw=true" width="800" style="margin-bottom: 15px;">
</div>

---

## 🔧 Dependencies

### All OpenWrt Releases
- `sms-tool` (`/usr/bin/sms_tool`)
- `curl` (Required for the Telegram notification daemon)

### OpenWrt 24.x Only
Without these packages, LuCI will show a **Runtime exception: No Lua runtime installed** error.

| Package | Purpose |
|---------|---------|
| **`luci-lua-runtime`** | Lua interpreter + LuCI Lua libraries (**mandatory**) |
| **`luci-compat`** | Compatibility layer for LuCI controllers and menus |

---

## 🚀 Installation Guide

### Option A — OpenWrt 25.x (APK Package Manager)

#### 1. Via Repository (Recommended)
```bash
# Add repository
echo 'https://github.com/ilblogdicristiangallo/ilblogdicristiangallo_repo_openwrt_APK/raw/refs/heads/main/packages.adb' >> /etc/apk/repositories.d/ilblogdicristiangallo.list

# Add public key
wget https://raw.githubusercontent.com/ilblogdicristiangallo/ilblogdicristiangallo_repo_openwrt_APK/main/ilblogdicristiangallo.apkpub.pem \
     -O /etc/apk/keys/ilblogdicristiangallo.apkpub.pem

# Update index and install
apk update
apk add luci-graphic-smstool
