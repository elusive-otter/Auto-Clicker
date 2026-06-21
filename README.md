#  AutoClicker by elusive-otter

An AutoHotkey v2 autoclicker with a clean GUI, adjustable speed, mouse button selection, auto walk, auto jump, and global hotkeys.

---

## Requirements

- **AutoHotkey v2** — Download from https://www.autohotkey.com/
  - Must be **v2**, not v1 (they are not compatible)

---

## Files

| File | Description |
|------|-------------|
| `autoclicker.ahk` | The main script — run this |
| `README.md` | This file |
| `GUIDE.md` | Full usage, editing, and AHK basics guide |
| `LICENSE` | MIT License |

---

## Quick Start

1. Install AutoHotkey v2
2. Double-click `autoclicker.ahk`
3. The GUI window will appear
4. Set your interval, pick a button, and press **Start** or **F6**

---

## Hotkeys

| Key | Action |
|-----|--------|
| `F6` | Toggle autoclicker on / off |
| `F7` | Toggle auto walk on / off |
| `F8` | Toggle auto jump on / off |
| `F9` | Quit the script entirely |

---

## GUI Controls

| Control | What it does |
|---------|--------------|
| Click Interval (ms) | Time between clicks in milliseconds |
| Slider | Drag to adjust click speed visually |
| Left / Right / Middle | Which mouse button to click |
| Single / Double | Click once or twice per interval |
| Start Walk | Holds the W key continuously for auto walking |
| Jump Interval (ms) | How often the Space key is pressed |
| Start Jump | Repeatedly presses Space for auto jumping |
| Start / Stop | Toggle the autoclicker |
| Quit | Close the script |

---

## Status Indicators

The top of the GUI shows live status for all three features:

```
CLICK  OFF     WALK  OFF     JUMP  OFF
```

Each switches to **ON** when active.

---

## Notes

- The clicker clicks at your **current cursor position**
- Auto Walk holds `W` — works in most games that use W to move forward
- Auto Jump presses and releases `Space` on a timer — adjustable from 100ms to 2000ms
- The window stays **always on top** so you can adjust while using other apps
- Quit is now **F9** (moved from F8 to make room for auto jump)

---

*Made by elusive-otter — see GUIDE.md for full documentation*
