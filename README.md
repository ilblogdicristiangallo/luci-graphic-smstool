# luci-graphic-smstool
LuCI Graphic SMS Tool: send and receive SMS from a USB modem (e.g. ZTE) via the OpenWrt web UI. Inbox, contacts, setup wizard (AT port, country prefix, SIM/ME storage), USSD and modem reset.

# luci-graphic-smstool

**LuCI Graphic SMS Tool** — send and receive SMS from a USB 3G/4G/5G modem (e.g. ZTE) through the OpenWrt web interface.

| OpenWrt | Package |
|---------|---------|
| **24.x** | `.ipk` (`opkg`) |
| **25.x** | `.apk` (`apk`) |

**Version:** 1.0.0  
**Depends:** `luci-base`, `sms-tool`

---

## What it does

Adds **Services → Graphic SMS Tool** in LuCI:

- **First-run wizard** (5 steps): AT port, country prefix, SMS storage
- **Inbox** — receive, read, delete SMS
- **New SMS** — compose and send
- **Contacts** — address book (name, number, note)
- **USSD** — run codes such as `*123#`
- **Reset modem**
- Storage: SIM (**SM**), modem memory (**ME**) or both

Backend: `/usr/bin/sms_tool` (AT commands on the selected `/dev/ttyUSB*` port).

Web path: `/cgi-bin/luci/admin/services/luci_graphic_smstool/inbox`

---

## Screenshots

### 1. Setup wizard — Welcome

First-run setup. Configures the modem once (5 steps).

![Setup welcome](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot.png?raw=true)

### 2. Setup wizard — Modem port

Choose the AT command port (`/dev/ttyUSB0`, `ttyUSB1`, `ttyUSB2`), **Auto-Detect Working Port**, **Refresh List** or **Test Selected Port**.

![Modem port](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot2.png?raw=true)

### 3. Setup wizard — Country prefix

Default country prefix (e.g. `39` for Italy).  
Example: `3331234567` → `393331234567`.

![Country prefix](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot3.png?raw=true)

### 4. Setup wizard — SMS storage

Where SMS are stored: **SIM (SM)**, **Modem (ME)** or **Both**.

![SMS storage](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot4.png?raw=true)

### 5. Setup wizard — Finish

Summary of port, prefix and storage, then **Finish Setup**.

![Finish setup](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot5.png?raw=true)

### 6. Inbox

Received SMS (From, Number, Date, Message, Actions).

Buttons: **New SMS**, **Receive SMS**, **Contacts**, **Settings**, **Reset Modem**, **Refresh**, **Delete All**.

![Inbox](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot6.png?raw=true)

Also in the UI (same app):

- **Contacts** — add name, phone (`3331234567` or `+393331234567`), optional note; search the address book
- **Settings** — modem port, country prefix, SMS storage, USSD (`*123#`)

---

## Install

Copy the package to the router (`/tmp`), then:

### OpenWrt 24 (IPK)
<pre>
opkg update
  
opkg install sms-tool
  
opkg install /tmp/luci-graphic-smstool_1.0.0-1_all.ipk</pre>

### OpenWrt 25 (APK)
<pre>
  apk update
  
  apk add sms-tool
  
  apk add --allow-untrusted /tmp/luci-graphic-smstool-1.0.0-r1.apk
</pre>
