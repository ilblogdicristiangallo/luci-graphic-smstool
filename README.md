# luci-graphic-smstool

LuCI Graphic SMS Tool: send and receive SMS from a USB modem (e.g. ZTE) via the OpenWrt web UI. Inbox, contacts, setup wizard (AT port, country prefix, SIM/ME storage), USSD and modem reset.

**LuCI Graphic SMS Tool** — send and receive SMS from a USB 3G/4G/5G modem (e.g. ZTE) through the OpenWrt web interface.

| OpenWrt | Package | Extra dependencies |
|---------|---------|--------------------|
| **24.x** | `.ipk` (`opkg`) | `luci-lua-runtime`, `luci-compat`, `sms-tool` |
| **25.x** | `.apk` (`apk`) | `sms-tool` |

**Version:** 1.0.0  

LuCI files are the same on 24 and 25 (`PKGARCH:=all`). OpenWrt 24 does **not** ship a Lua runtime with LuCI by default, so this Lua app needs extra packages.

## Screenshots

### Setup wizard — Welcome
First-run setup. Configures the modem once (step 1 of 5).

![Setup wizard — Welcome](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot.png?raw=true)

### Setup wizard — Modem port
Choose the AT port (`/dev/ttyUSB0`, `ttyUSB1`, `ttyUSB2`), auto-detect or test the selected port.

![Setup wizard — Modem port](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot2.png?raw=true)

### Setup wizard — Country prefix
Default country prefix (e.g. `39` for Italy). Example: `3331234567` → `393331234567`.

![Setup wizard — Country prefix](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot3.png?raw=true)

### Setup wizard — SMS storage
Where SMS are stored: SIM (SM), modem memory (ME) or both.

![Setup wizard — SMS storage](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot4.png?raw=true)

### Setup wizard — Finish
Summary of port, prefix and storage, then Finish Setup.

![Setup wizard — Finish](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot5.png?raw=true)

### Inbox — Received SMS
Received messages (From, Number, Date, Message). New SMS, Receive SMS, Contacts, Settings, Reset Modem.

![Inbox — Received SMS](https://github.com/ilblogdicristiangallo/luci-graphic-smstool/blob/main/Screenshot/Screenshot6.png?raw=true)

---

## Dependencies

### All versions

- `luci-base`
- `sms-tool` (`/usr/bin/sms_tool`)

### OpenWrt 24.x only (required)

Without these, LuCI shows **Runtime exception: No Lua runtime installed**.

| Package | Why |
|---------|-----|
| **`luci-lua-runtime`** | Lua interpreter + LuCI Lua libraries (**mandatory**) |
| **`luci-compat`** | Lua controller / menu compatibility |

# Install OpenWrt 24
<pre>opkg update
opkg install luci-lua-runtime luci-compat sms-tool</pre>

# Install OpenWrt 25

<pre>
  apk update
  
  apk add sms-tool
  
  apk add --allow-untrusted /tmp/luci-graphic-smstool-1.0.0-r1.apk
</pre>
