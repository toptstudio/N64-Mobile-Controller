# 🎮 N64 Touch UI

A clean, mobile‑first touch controller interface for Nintendo 64 emulation via WebAssembly (WASM).  
This repository contains **only** the front‑end UI shell – no emulator core, no game ROMs, no copyrighted assets.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## ⚠️ Disclaimer & Legal Awareness

This project is **not affiliated with, endorsed by, or sponsored by Nintendo Co., Ltd.**  
"Nintendo 64", "N64", and all associated game titles, characters, and assets are registered trademarks of Nintendo.  

This software is provided **for educational and interoperability purposes only**.  
Users are **solely responsible** for complying with all applicable copyright laws in their jurisdiction.  
The author assumes no liability for any misuse, including but not limited to the use of unauthorized ROMs or emulator cores.

**This repository does NOT include, distribute, or condone the sharing of:**
- Any emulator core (`.wasm` / `.js` files)
- Any game ROMs or BIOS files
- Any proprietary Nintendo code, assets, or trademarks

---

## 📄 License

The HTML, CSS, and JavaScript code in this repository (the touch UI) is the original work of the author and is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.  
You are free to use, modify, and distribute this UI, provided you retain the copyright notice.

---

## 📱 What This UI Is

`index.html` is a fully self‑contained, responsive touch‑controller overlay designed to work with any WebAssembly‑based N64 emulator that accepts keyboard input.  
It provides **no emulation logic itself** – it is purely a visual/input bridge that translates touch gestures into standard keyboard events.

### ✨ Key Features
- **Two analog sticks** – a large movement stick (character control) and a smaller camera stick (C‑Stick look).
- **Action buttons** – A (jump/confirm), B (attack/cancel), Z (modifier/crouch), plus shoulder L and Start.
- **Fully responsive** – optimised layouts for both portrait and landscape orientations on mobile.
- **Real‑time key display** – shows which virtual keys are currently pressed.
- **Semi‑transparent controls** – overlay blends over the game canvas without hiding the action.
- **Fullscreen toggle** – button to enter/exit fullscreen on supported browsers.
- **Multi‑touch ready** – joysticks and buttons can be used simultaneously.
- **Zero dependencies** – everything is in one HTML file (CSS and JavaScript inline).

---

## 🚀 Setup Instructions

### 1. Download the UI
- Get `index.html` from this repository.

### 2. Add Your Own Emulator Core
- Place your WebAssembly N64 emulator core (e.g., `n64_wasm_core.js` and `n64_wasm_core.wasm`) in the same folder as `index.html`.
- The UI expects a core that listens to keyboard events and renders to a `<canvas>`.
- If your core has a different filename, you can edit the last `<script>` tag in `index.html` (search for `src="…"`).

### 3. Provide Your Own ROM
- You must legally own the game ROM you intend to play.
- The emulator core typically loads a ROM via its own interface or by editing the core’s configuration – refer to your core’s documentation.

### 4. Open in Browser
- Open `index.html` in a modern browser (Chrome, Firefox, Edge) on desktop or Android.
- On touch devices the controls will appear automatically.
- Tap **Start** (or press Enter) to begin the game.

---

## 🔧 Customizing the UI

All customisation is done by editing `index.html` with a simple text editor. No build tools required.

### ⌨️ Modifying Key Bindings (Touch → Keyboard)

The UI works by converting touch inputs into **keyboard key events**. Each on‑screen button has a `data-key` attribute that determines which key is sent.

**How it works:**
- When you touch a button, `keydown` and `keyup` events are fired on the `<canvas>` and `document`.
- The emulator core listens for these events and translates them into N64 controller inputs.

#### Default Key Mappings

| Control         | Keyboard Key   | HTML Attribute       | N64 Function                     |
|-----------------|----------------|----------------------|----------------------------------|
| A (big red)     | `x`            | `data-key="x"`       | Jump / Confirm                   |
| B (yellow)      | `c`            | `data-key="c"`       | Attack / Cancel                  |
| Z (purple)      | ` ` (Space)    | `data-key=" "`       | Crouch / Modifier                |
| Start (green)   | `Enter`        | `data-key="Enter"`   | Pause / Start game               |
| L (blue top)    | `q`            | `data-key="q"`       | Camera shoulder button           |

**Movement Stick:**  
Right joystick sends `ArrowUp` `ArrowDown` `ArrowLeft` `ArrowRight` (up, left, down, right).  

**Camera Stick (C‑Stick):**  
Left joystick sends `W` `A` `S` `D` (up, left, down, right).

#### Changing a Button's Key

1. Open `index.html` in a text editor.
2. Search for the button you want to modify, e.g. `id="btn-a"`.
3. Change the `data-key` value. For example, to make A send the `z` key, change `data-key="x"` to `data-key="z"`.
   - Original: `<button id="btn-a" data-key="x">A</button>`
   - Modified: `<button id="btn-a" data-key="z">A</button>`

The same method applies to all buttons:  
- **B** (`id="btn-b"`) – change `data-key="c"`  
- **Z** (`id="btn-z"`) – change `data-key=" "` (a single space for Space)  
- **Start** (`id="btn-start"`) – change `data-key="Enter"`  
- **L** (`id="btn-l"`) – change `data-key="q"`

#### Common Key Values You Can Use

| Desired Key  | `data-key` Value |
|--------------|------------------|
| Letter a‑z   | `a` … `z`        |
| Space        | ` ` (one space)  |
| Enter        | `Enter`          |
| Shift        | `Shift`          |
| Control      | `Control`        |
| Alt          | `Alt`            |
| Tab          | `Tab`            |
| Escape       | `Escape`         |
| Arrow Up     | `ArrowUp`        |
| Arrow Down   | `ArrowDown`      |
| Arrow Left   | `ArrowLeft`      |
| Arrow Right  | `ArrowRight`     |

---

### 📐 Adjusting the Visual Layout (CSS)

The UI uses responsive CSS with `clamp()`, `vh`, `vw`, and `%` units. You can tweak the sizes and positions of all controls by editing the `<style>` section in `index.html`.

**Common customizations:**

- **Joystick sizes:** Look for `#joy-cstick` (movement stick) and `#joy-move` (camera stick). Change `width` and `height`.
- **Button sizes:** Look for `#btn-group` – adjust `width`, `height`, and `gap` for spacing.
- **Font sizes:** Search for `font-size` inside the button and label selectors.
- **Landscape vs. portrait:** Different styles are applied under `@media (orientation: landscape)` and `@media (max-width: 480px)`. You can fine‑tune the control positions for each orientation.

All changes take effect immediately after saving the file and refreshing the browser.

---

## ⚖️ Legal Compliance Summary

| What you distribute        | Copyright status             | Action required                          |
|----------------------------|------------------------------|------------------------------------------|
| `index.html` (UI code)     | Your original work           | MIT License already included             |
| Emulator core (.js/.wasm)  | Not in this repo             | User must obtain separately, legally     |
| Game ROMs                  | Not in this repo             | User must own and provide legally        |

This repository contains **only** the original UI code. No copyrighted third‑party code, assets, or ROMs are included.  
The author does **not** encourage or facilitate software piracy.

---

## 🤝 Contributing

You are welcome to fork this repository and adapt the UI for your own emulation projects.  
If you make improvements (e.g., better responsiveness, new features), feel free to open a pull request.  
Please retain the original copyright notice in the source code if you redistribute.

---

## 🆘 Support

This project is provided “as‑is” without warranty of any kind.  
For issues with specific emulator cores or ROMs, please consult the respective documentation.  
If you encounter a bug in the touch UI itself, open an issue on GitHub with a clear description and screenshot if possible.

---

**Happy retro gaming – responsibly! 🕹️**
