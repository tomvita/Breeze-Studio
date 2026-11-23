# Breeze Studio

Breeze on your PC: one window, with a tab for each kind of work. It talks to Breeze on a Switch over
Wi-Fi, to a game in an emulator (the Lichii fork, or any yuzu-family emulator through emuhost), or to
a game running on the PC itself through pchost.

This repository holds Studio's releases. Breeze itself is released on
[Breeze-Beta](https://github.com/tomvita/Breeze-Beta/releases); each Breeze release note names the
Studio release to use with it, and each Studio release names the Breeze it needs.

## Downloads

Each [release](https://github.com/tomvita/Breeze-Studio/releases) has:

- **`pc_app.zip`**: Breeze Studio and the PC app (`breeze_studio.py`, `pcconnect_app.py` and the
  `studio` folder). Unzip it into one folder, keeping `studio` beside `breeze_studio.py`.
- **`pchost_<version>.zip`**: `pchost.exe`, for games on the PC (64-bit Windows). Start the game,
  then pchost; connect Studio to 127.0.0.1, code 1234.

## What you need

- **Python 3** with Tk (the python.org installer for Windows includes it; on Linux `python3-tk`).
- `pip install pillow capstone`, and `keystone-engine` for Hook here in the Code tab.
- For a Switch: Breeze with PC connect on (Settings > PC connect shows the address and the code).

## Guide

The [Breeze Studio guide](https://github.com/tomvita/Breeze-Beta/blob/master/docs/breeze%20studio.md)
and [PC Connect](https://github.com/tomvita/Breeze-Beta/blob/master/docs/pcconnect.md) (emuhost,
pchost) are in Breeze-Beta's docs.

Feedback and support: [Discord](https://discord.gg/bEFfp7MZUD).
