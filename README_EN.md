<p align="center"><img src="logo.png" width="128" alt="PSVIETHOA"></p>

<h1 align="center">PSVIETHOA OVERLAY</h1>

<p align="center"><a href="README.md">Tiếng Việt</a> · <b>English</b></p>

An on-screen overlay (OSD) for the PS5 that draws on top of your game: see FPS,
temperatures, clocks and memory in game, steer the fan by temperature, and use an
**in-game cheat menu opened with the controller**. Everything is configured from a
web page you open on a PC or phone.

All you need is **one file**: `psvh_overlay.elf`.

---

## Features

- **In-game HUD**: FPS, CPU / GPU / SSD temperature, CPU load, CPU / GPU clock,
  RAM, VRAM, fan speed, power draw, IP address. Toggle each item, reorder them,
  change colors, position and font size.
- **Fan override**: set a target temperature from 50 to 91 °C. A lower target
  spins the fan harder and keeps the console cooler.
- **In-game cheat menu**: hold **L1+R1** (configurable) to open it. It detects the
  running game and loads the matching cheat file.
- **Three cheat formats**: `.json`, `.shn`, `.mc4`.
- **Remembers your cheats**: after a reboot or relaunching the game, the cheats you
  picked are turned back on automatically.
- **Bilingual**: Vietnamese when the PS5 is set to Vietnamese, English for any other
  language. Can be forced in the settings.
- **Web settings page** (port `8386`) plus a **PSVIETHOA.COM tile** on the home
  screen for quick access.
- **No game hooks**: no game files are modified, nothing is installed into games.

## Requirements

- A **jailbroken** PS5 that can run ELF payloads through **elfldr** (port `9021`).
- Tested on **PS5 Pro, firmware 10.01**. Other firmware versions are untested.

## Running it

1. Download `psvh_overlay.elf` from this page.
2. Send it to port `9021` on the PS5 with your usual payload sender (or add it to
   your autoload list).
3. When the **"PSVIETHOA OSD is running"** notification with the PSVIETHOA logo
   appears, you are done.

Open the settings page in either way:

- On the PS5: open the **PSVIETHOA.COM** tile on the home screen.
- From a PC / phone on the same network: go to `http://<PS5-IP>:8386`.

To remove it, or before loading a newer version: go to the **System** tab →
**Unload from SceShellUI**, wait until the page says it is unloaded, then send the
new ELF. Sending it while the old one is still running leaves two copies running.

## Cheats

### Adding cheat files

Copy files into **`/data/PSVIETHOA/cheat`** (over FTP), named like this:

```
<TITLEID>_<version>.json     e.g. PPSA04264_01.005.000.mc4
```

The extension can be `.json`, `.shn` or `.mc4`. After adding or replacing a file,
press **Reload file** on the web page (or **△** in the menu); there is no need to
reload the ELF.

### Opening the menu in game

While playing, hold **L1+R1** for about 0.8 seconds.

| Button | Action |
|---|---|
| **↑ ↓** | Move |
| **×** | Toggle the cheat |
| **△** | Reload the list |
| **○** | Close the menu |
| **L1 / R1** | Change page |

The button combo and hold time can be changed in the **Cheat** tab of the web
page. Cheats can also be toggled straight from the web page.

### Cheats turned back on automatically

Every cheat you turn on is remembered per game. The next time you start that game,
it is turned back on about 6 seconds later and a notification tells you so. The
list lives in `/data/PSVIETHOA/cheat_tu_bat.txt`, one `TITLEID<tab>cheat name`
per line. Delete a line and that cheat is no longer turned on automatically.
Pressing **Turn all off** on the web page clears the list for that game.

### Safety

Before writing anything, the ELF checks that the bytes in game memory match the
cheat file. A cheat file made for another game version is **refused** instead of
written blindly. Cheats still modify game memory: save your game first, and **do
not use them online**.

## Language

The default is **Auto**: Vietnamese when the PS5 is set to Vietnamese, English for
any other language. This covers the web page, the cheat menu and notifications.
Change it in the **System** tab → **Language**, then press **Save and apply to PS5**.

## Files on the console

| Path | What it is |
|---|---|
| `/data/PSVIETHOA/config.ini` | Settings; can be edited by hand. Read again every time the ELF loads. |
| `/data/PSVIETHOA/cheat/` | Folder for cheat files |
| `/data/PSVIETHOA/cheat_tu_bat.txt` | Cheats that are turned back on automatically |
| `/data/PSVIETHOA/logo.png` | Logo used by notifications (written by the ELF) |
| `/user/app/FAKE08585/` | The PSVIETHOA.COM tile on the home screen |

## Checksum

```
psvh_overlay.elf   945392 bytes
SHA-256  a5980efe5c944551ca061654269908af208adac8b597bf87b0e9466b9e71ecd6
```

## Credits

Made by **PSVIETHOA.COM**. Based on
[ps5-new-overlay](https://github.com/smoxa/ps5-new-overlay); the ELF loading code
is by John Törnblom.

Use at your own risk. Not affiliated with Sony Interactive Entertainment.
