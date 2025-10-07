# Kimi K2 Stealth (Violentmonkey)
Stealth userscript for Moonshot Kimi K2: crosshair A→B screen capture, clipboard
text/image, smart prompting, auto-copied outputs, and a camouflaged context menu.

API note: This script assumes Moonshot Kimi’s Chat Completions API
is OpenAI-compatible at `https://api.moonshot.ai/v1/chat/completions`. If your
account uses different endpoints/models, adjust the settings in the menu.

## Features
- Alt+Right-click camouflaged mini menu + fallback opener hotkey
- Two-click crosshair capture (A → B) with vision model
- Input sources:
  - Selected text (fallback to clipboard text if none)
  - Clipboard text
  - Clipboard image (or right-clicked <img>)
- Auto-copy outputs for all actions
- Smart prompt profile:
  - Language: English (US) or Spanish (Spain), optional auto-detect for text
  - Modes: technical, student (FP nivel medio), singleAnswer, shortAnswer
  - Length presets: short, medium, long, extraLong
  - Plain text only (no filler/markdown) or minimal JSON for single/short answers
- Toggleable bottom toasts (silent mode)
- Privacy-first: no telemetry, keys stored locally by Violentmonkey

## Install
1) Install Violentmonkey:
- Chrome/Edge/Brave: https://violentmonkey.github.io/get-it/
- Firefox: https://addons.mozilla.org/firefox/addon/violentmonkey/

2) Install the userscript:
- Click the Raw link to the file below and confirm install in Violentmonkey:

Raw install (main):
https://raw.githubusercontent.com/<YOUR_GH_USERNAME>/kimi-k2-stealth-vm/main/userscript/kimi-k2-stealth.user.js

Or lock to a tag (recommended for updates):
https://raw.githubusercontent.com/<YOUR_GH_USERNAME>/kimi-k2-stealth-vm/v1.4.0/userscript/kimi-k2-stealth.user.js

3) Open the Violentmonkey popup → your script → Menu commands:
- Set Kimi API Key (paste your Moonshot Kimi key)
- Optional: Toggle toasts, Language, Mode, Output length, Hotkeys

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

## How to use
- Alt+Right-click (or Ctrl+Shift+M) to open the small menu near the cursor.
- Pick one of:
  - Input selected text → sends highlighted text (or clipboard text if none).
  - Input clipboard text → sends your clipboard text directly.
  - Input image → uses clipboard image if available; otherwise the right-clicked image.
  - Capture area (A→B) → allows a two-click rectangle on the shared screen view and sends it.
- Every result is automatically copied to the clipboard. Optionally show the last output in a floating tooltip.

## Settings (Violentmonkey menu)
- Set Kimi API Key
- Toggle toasts (hide bottom messages)
- Toggle Language (ES/EN)
- Cycle Mode (technical / student / singleAnswer / shortAnswer)
- Select Output Length (short / medium / long / extraLong)
- Edit default prompts (per action)
- Set hotkeys
- Toggle Alt+Right-click activation (use normal Right-click if preferred)
- Toggle debug logs (console)

## Permissions and privacy
- Clipboard: used to read text/images on demand and copy outputs automatically.
- Screen capture: invokes the browser’s screen picker (required by browser security) for A→B region capture.
- Network: requests your configured Kimi endpoint via `GM_xmlhttpRequest`.
- No analytics/telemetry. Your API key is stored locally by Violentmonkey.

## Known limitations
- Browser’s screen picker dialog cannot be bypassed by any script/extension.
- Crosshair region mapping works best when you select “This tab” or “Entire screen.”
- Some pages intercept the native context menu; use Ctrl+Shift+M to open the script menu at the cursor.

## Updating
This userscript supports manual updates via Violentmonkey. For auto-updates, set
the metadata fields in the file to point at your raw GitHub path (see below).

## Metadata: updateURL/downloadURL (optional)
In `userscript/kimi-k2-stealth.user.js`, add or edit:
```javascript
// @updateURL   https://raw.githubusercontent.com/Microck/kimi-k2-stealth-script/main/userscript/kimi-k2-stealth.user.js
// @downloadURL https://raw.githubusercontent.com/Microck/kimi-k2-stealth-script/main/userscript/kimi-k2-stealth.user.js
```

## API configuration
Defaults assume:
- Base URL: https://api.moonshot.ai
- Endpoint: /v1/chat/completions
- Text model: kimi-k2-0905-preview
- Vision model: moonshot-v1-128k-vision-preview

If your account differs, use “Set API Base/Path/Models” in the menu to update.
