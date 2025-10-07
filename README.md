# Kimi K2 Stealth (Violentmonkey)

Stealth userscript for Moonshot Kimi K2: crosshair A→B screen capture, clipboard text/image, smart prompting, auto‑copied outputs, and a camouflaged context menu.

<img width="318" height="365" alt="Screenshot_9" src="https://github.com/user-attachments/assets/f0f673ee-1bd0-4d66-b3a7-093216e491c2" />


API note: This script assumes Moonshot Kimi’s Chat Completions API is OpenAI‑compatible at `https://api.moonshot.ai/v1/chat/completions`. If your account uses different endpoints/models, adjust settings in the menu.

---

## Features

- Alt+Right‑click camouflaged mini menu + fallback opener hotkey
- Two‑click crosshair capture (A → B) with vision model (no extra UI)
- Input sources:
  - Selected text (fallback to clipboard text if none)
  - Clipboard text
  - Clipboard image (or right‑clicked `<img>`)
- Auto‑copy outputs for all actions (no extra dialogs)
- Smart prompt profile:
  - Language: English (US) or Spanish (Spain), optional auto‑detect for text
  - Modes: technical, student, singleAnswer, shortAnswer
  - Length presets: short, medium, long, extraLong
  - Plain text only (no filler/markdown) or minimal JSON for single/short answers
- Toggleable bottom toasts (silent mode)
- Privacy‑first: no telemetry; API key stored locally by Violentmonkey

---

## Install

1) Install Violentmonkey  
- Chrome/Edge/Brave: https://violentmonkey.github.io/get-it/  
- Firefox: https://addons.mozilla.org/firefox/addon/violentmonkey/

2) Install the userscript  
- Click the Raw link below and confirm install in Violentmonkey:

Raw install (main):  
https://raw.githubusercontent.com/Microck/kimi-k2-stealth-script/main/kimi-k2-stealth.user.js

3) Configure  
- Open the Violentmonkey popup → your script → Menu commands:
  - Set Kimi API Key (paste your Moonshot Kimi key)
  - Optional: Toggle toasts, Language, Mode, Output length, Hotkeys

---

## Quick start

- Alt+Right‑click anywhere (or press Ctrl+Shift+M) to open the small menu.
- Choose:
  - Input selected text → sends highlighted text (or clipboard text if none).
  - Input clipboard text → sends your clipboard text.
  - Input image → uses clipboard image if available; otherwise the right‑clicked image.
  - Capture area (A→B) → click point A then point B on the chosen screen/tab; region is captured and sent.
- Every result is automatically copied to the clipboard. You can optionally show the last output in a floating tooltip.

Note: The browser’s “select a screen/window/tab” permission prompt for capture is required by browser security and cannot be bypassed. For best mapping, choose “This tab” or “Entire screen.”

---

## Default hotkeys

- Open menu at cursor: Ctrl+Shift+M
- Input selected text: Ctrl+Shift+T
- Input clipboard text: Ctrl+Shift+L
- Input image (clipboard/hovered): Ctrl+Shift+I
- Capture area (A→B): Ctrl+Shift+C
- Paste output text: Ctrl+Shift+P
- Copy output: Ctrl+Shift+Y
- Show output tooltip: Ctrl+Shift+U

You can change these under “Set hotkeys.”

---

## Settings (Violentmonkey menu) — in depth

Open Violentmonkey → click the script → Menu commands. All settings persist locally.

### 1) Set Kimi API Key
- Stores your Moonshot Kimi API key locally (Violentmonkey storage).
- Required once. You can rotate it anytime.

### 2) Toggle toasts
- Shows/hides the small bottom messages (“Copied.” / “Error.”).
- Useful for stealth or when you only want silent auto‑copy behavior.

### 3) Toggle Language (ES/EN)
- Switches prompt language: Spanish (Spain) or English (US).
- Also used for “student” tone.

### 4) Cycle Mode (technical / student / singleAnswer / shortAnswer)
- technical: expert‑level, precise, concise.
- student: simpler language, clearer explanations.
- singleAnswer: output reduced to a single letter/word. Internally requests minimal JSON and then extracts the “answer”.
- shortAnswer: a few words only. Same minimal‑JSON discipline internally.
- Note: In single/short modes, “Output format” is forced to minimal JSON internally, but the script outputs clean text only (the value of `answer`).

### 5) Select Output Length (short / medium / long / extraLong)
- Provides soft targets for response size (ignored in single/short modes):
  - short: ~1 sentence (≈1 line)
  - medium: ~1 paragraph (≈3 lines)
  - long: ~1 paragraph (≈5 lines)
  - extraLong: ~3 short paragraphs
- The model is guided to those sizes; actual lengths can vary slightly.

### 6) Edit default prompts (per action)
- You can redefine the quiet directive for each action:
  - Selected text
  - Clipboard text
  - Input image
  - Capture area
- These are micro‑prompts appended to your request to keep tokens minimal. No dialog is shown during use; defaults are applied automatically.

### 7) Set hotkeys
- Reassign any shortcut, including menu opener.
- Format tips:
  - Case‑insensitive strings like `Ctrl+Shift+T`, `Alt+X`, `Ctrl+Alt+I`
  - Avoid conflicts with system/global shortcuts when possible.

### 8) Toggle Alt+Right‑click activation
- Alt+Right‑click (default): more discreet; normal right‑click behaves as usual.
- Always Right‑click: shows this menu on any right‑click. Use only if you want quick access everywhere. If a page blocks context menus, use the fallback hotkey (Ctrl+Shift+M) instead.

### 9) Toggle debug logs
- Prints verbose logs to the browser console for troubleshooting.
- Turn off for normal stealth use.

### 10) API Base/Path/Models (if present)
- Adjusts:
  - Base URL (default: `https://api.moonshot.ai`)
  - Endpoint path (default: `/v1/chat/completions`)
  - Text model (default: `kimi-k2-0905-preview`)
  - Vision model (default: `moonshot-v1-128k-vision-preview`)
- Only change these if your Kimi account specifies different endpoints/models.

---

## Behavior details

- Auto‑copy: Every response is copied to clipboard automatically (across all inputs).
- No user prompts: Uses saved default directives; no per‑action dialogs appear.
- Language auto‑detect: For text inputs, the script attempts basic EN/ES detection on your content and may switch language accordingly (can be toggled off inside the script if you prefer a fixed language).
- Output cleanup:
  - Plain mode removes greetings, “Answer:”, markdown, extra whitespace.
  - Single/short modes reduce structured responses to a single clean line/word.
- Input image priority:
  - Clipboard image if present
  - Else right‑clicked `<img>` when menu opened
- Capture (A→B): Two clicks define a rectangle in the shared screen view; the captured region is scaled down (if needed) to reduce tokens.

---

## Permissions and privacy

- Clipboard: reads text/images on demand and writes outputs automatically.
- Screen capture: invokes the browser’s screen picker for region capture (mandatory by browser security).
- Network: calls your configured Kimi endpoint via `GM_xmlhttpRequest`.
- Storage: Violentmonkey local storage for settings and API key.
- No analytics/telemetry collected by this script.

---

## Known limitations

- The screen‑picker dialog is enforced by modern browsers for security and cannot be bypassed.
- Crosshair mapping is most accurate when sharing “This tab” or the “Entire screen.”
- Some sites intercept the native context menu; use Ctrl+Shift+M to open the script’s menu at the cursor.

---

## Updating

This userscript supports manual updates via Violentmonkey. For auto‑updates, add metadata URLs pointing to your GitHub raw file.

### Metadata: updateURL/downloadURL (optional)

In the root userscript `kimi-k2-stealth.user.js`, add:

```javascript
// @updateURL   https://raw.githubusercontent.com/Microck/kimi-k2-stealth-script/main/kimi-k2-stealth.user.js
// @downloadURL https://raw.githubusercontent.com/Microck/kimi-k2-stealth-script/main/kimi-k2-stealth.user.js
```

For tagged releases, replace `main` with your tag (e.g., `v1.4.0`).

---

## API configuration

Defaults assume:
- Base URL: https://api.moonshot.ai
- Endpoint: /v1/chat/completions
- Text model: kimi-k2-0905-preview
- Vision model: moonshot-v1-128k-vision-preview

If your account differs, use the menu to update.

---

## Troubleshooting

- “Menu doesn’t show”: Hold Alt while right‑clicking, or press Ctrl+Shift+M. Some pages block context menus.
- “Clipboard read blocked”: Ensure you interacted with the page (click once) and your browser grants clipboard permissions.
- “Screen capture denied”: The browser prompt was canceled or policy blocks capture. Try again and select “This tab” or “Entire screen.”
- “No image found”: Put an image on your clipboard first, or right‑click over an `<img>` before opening the menu.

---

## License

MIT © Microck
