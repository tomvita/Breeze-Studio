# Breeze Studio

Breeze on your PC: one window, with a tab for each kind of work. It talks to Breeze on a Switch over
Wi-Fi, to a game in an emulator (the Lichii fork, or any yuzu-family emulator through emuhost), or to
a game running on the PC itself through pchost.

This repository holds Studio's releases. Breeze itself is released on
[Breeze-Beta](https://github.com/tomvita/Breeze-Beta/releases); each Breeze release note names the
Studio release to use with it, and each Studio release names the Breeze it needs.

## First time

1. Install **Python 3** from [python.org](https://www.python.org/downloads/) (on Windows keep "py launcher"
   ticked; it is on by default).
2. Download `pc_app.zip` from the [latest release](https://github.com/tomvita/Breeze-Studio/releases/latest)
   and unzip it into a folder of its own.
3. Double-click `breeze_studio.bat` (or run `python breeze_studio.py`). The first time, Studio says which
   Python packages are missing (Pillow, capstone) and installs them if you say Yes.
4. Start what Studio talks to, then type its address and code at the top and press **Connect**:

| You use Studio with | First | Address | Code |
|---|---|---|---|
| a Switch | open Breeze, turn on Settings > PC connect (same network as the PC) | the IP Breeze shows | the code Breeze shows |
| the Lichii fork | Configure > Debug > Enable PC connect, start a game | `127.0.0.1` | the code shown there |
| another yuzu-family emulator | turn on Enable GDB stub in its Debug settings, start the game, then `emuhost.exe` (`emuhost_<version>.zip`) | `127.0.0.1` | `1234` |
| a game on this PC (64-bit Windows) | start the game, then `pchost.exe` (`pchost_<version>.zip`) | `127.0.0.1` | `1234` |

The address and code are remembered. If Connect fails, the Start page says what to check:
"nothing answers" means nothing is listening yet (step 4's "First" column), "no answer" means the IP or
the network is wrong, and a wrong code says where the right one is shown.

## Downloads

Each [release](https://github.com/tomvita/Breeze-Studio/releases) has:

- **`pc_app.zip`**: Breeze Studio and the PC app (`breeze_studio.py`, `pcconnect_app.py` and the
  `studio` folder). Unzip it into one folder, keeping `studio` beside `breeze_studio.py`.
- **`emuhost_<version>.zip`**: `emuhost.exe`, for a game in an unchanged emulator of the yuzu family
  (from 0.6, released here; 0.5 was in Breeze beta129.04). Turn on the emulator's GDB stub, start the
  game, then emuhost; connect Studio to 127.0.0.1, code 1234.
- **`pchost_<version>.zip`**: `pchost.exe`, for games on the PC (64-bit Windows). Start the game,
  then pchost; connect Studio to 127.0.0.1, code 1234.

A release whose notes say "added" also got a newer emuhost or pchost after it came out.

## What you need

- **Python 3** with Tk (the python.org installer for Windows includes it; on Linux `python3-tk`).
- `pip install pillow capstone`, and `keystone-engine` for Hook here in the Code tab.
- For a Switch: Breeze with PC connect on (Settings > PC connect shows the address and the code).

## Guide

The [Breeze Studio guide](https://github.com/tomvita/Breeze-Beta/blob/master/docs/breeze%20studio.md)
and [PC Connect](https://github.com/tomvita/Breeze-Beta/blob/master/docs/pcconnect.md) (emuhost,
pchost) are in Breeze-Beta's docs.

Feedback and support: [Discord](https://discord.gg/bEFfp7MZUD).
