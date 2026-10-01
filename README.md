# LEGO Ninjago: Tournament - Modern Android Fix (Android 14+)

![Android Support](https://img.shields.io/badge/Android-14%2B-brightgreen.svg)
![Engine](https://img.shields.io/badge/Engine-FUSION_Engine-blue.svg)

---
A technical patch to natively revive **LEGO Ninjago: Tournament** (`com.lego.ninjago.toe`) on Android 14, 15, and 16, resolving OpenGL initialization crashes and fixing legacy FUSION Engine multi-touch defects

### Technical Patches
1. Hidden API Bypass (pass through google checker to point right into game library)
2. Multi-Touch Isolation & Floating Joystick Rewrite (this may not worked well)

### Quick Setup
(make sure that you have downloaded the .obb file before proccessing, you can find it on community source)
1. Download `game_aligned.apk` from [Releases](../../releases).
2. Place original OBB files into `Internal Storage/Android/obb/com.lego.ninjago.toe/`, note that put the .obb file in `com.lego.ninjago.toe`.
3. Install the APK and launch.

### Relative Bug
The game input may stucked while pressing 2 buttons or press while moving in a time due to the engine, i can't fix it unless i have the source code.

### Disclaimer

Non-profit reverse-engineering and preservation project. All game assets and engine code belong to **WB Games** and **The LEGO Group**.

---
