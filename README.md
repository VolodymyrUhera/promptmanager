# Open Prompt Manager (Firefox Edition)

A lightweight, open-source **Firefox WebExtension (Manifest V3)** for saving, organizing, and inserting prompts across AI chatbots — ChatGPT, Claude, Gemini, Grok, and [17+ more platforms](#supported-platforms).

**Branch:** `main` (Firefox Extension Version) · [Open Prompt Database](https://openpromptdatabase.com/)

---

## Overview & Firefox Compatibility

This branch houses the dedicated **Mozilla Firefox Manifest V3** version of Open Prompt Manager, optimized for Mozilla Add-ons (AMO) standards and Gecko engine execution.

### Firefox WebExtension Features

- **Native Firefox Sidebar Action**: Uses `"sidebar_action"` for native sidebar integration in Firefox (`sidepanel/index.html`).
- **Firefox Background Script Architecture**: Configured with `"background": { "scripts": ["service-worker.js"], "type": "module" }` for background execution.
- **Gecko Browser Settings**: Configured with `browser_specific_settings.gecko` (`open-prompt-manager@openpromptdatabase.com`, min version `115.0`).
- **Content Script Sandbox Fallback**: Includes storage fallback adapters to ensure reliable storage reads and prompt insertion in Firefox content script sandboxes.
- **Cross-Browser WebExtensions API**: Built using unified `browserAPI` helpers (`globalThis.browser ?? globalThis.chrome`).

---

## Features

### Prompt Library

- Save, edit, reorder, and delete prompts from the **sidebar panel** or an **in-page panel** on assistant sites
- **Tags** with search and filter — synced between the sidebar panel and in-page list; tag suggestions on create/edit forms
- Drag to reorder tags in Settings → **Tag management**
- **Variables** with `#variable#` syntax — fill in values before inserting
- **Import / export** full v2 backups (prompts, folders, tag order) as JSON
- **Copy to clipboard** from the sidebar panel or context menu — handy on unsupported sites
- Save selected text to your library via the **context menu**

### On Assistant Sites

- **Floating button** or **hot corner** launcher (choose in Settings)
- One-click insert into the chat input, with optional append mode
- **Custom keyboard shortcut** — record your own open/close combo (default: ⌘⇧P on Mac, Ctrl+M on Windows/Linux)
- **Custom websites** — pin any site's chat input from the sidebar panel
- Light and dark themes, with optional force-dark mode

### Open Prompt Database

Browse community prompts on the [Open Prompt Database](https://openpromptdatabase.com/) and add them to your library with one click.

- Stable `opd:` ids — re-import updates the same prompt when the catalog entry changes
- Duplicate detection — already in your library? The site shows “Already in library”
- Link from Settings → **Browse the community catalog**

---

## Supported Platforms

| ChatGPT | Claude | Google Gemini |
| :--- | :--- | :--- |
| **NotebookLM** | **DeepSeek** | **Microsoft Copilot** |
| **GitHub Copilot** | **Grok** | **Poe** |
| **Kimi** | **Mistral Le Chat** | **OpenRouter** |
| **Perplexity** | **Qwen** | **Google AI Studio** |
| **OpenAI Playground** | **ChatLLM (Abacus)** | **LMArena** |

Plus any site you configure as a **custom website**.

---

## Installation in Firefox

### Development / Temporary Add-on

1. Clone this repository and checkout the `main` branch:
   ```bash
   git checkout main
   ```
2. Open Firefox and navigate to `about:debugging#/runtime/this-firefox` in the address bar.
3. Click **Load Temporary Add-on...**
4. Select `src/manifest.json` (or `src/manifest.firefox.json`).
5. Open the Firefox sidebar (`Ctrl+Sidebar` or click the extension icon) and grant access to the assistant sites you use in **Settings → Permissions editor**.

---

## Repository Branch Directory

| Branch | Description | Primary Target | Manifest Configuration |
| :--- | :--- | :--- | :--- |
| **`main`** *(current)* | **Firefox Version** | Mozilla Firefox (AMO) | `manifest.firefox.json` (`sidebar_action`, `background.scripts`) |
| **`combined`** | **Cross-Browser Version** | Chrome & Firefox | Build tools (`npm run build:chrome`, `npm run build:firefox`) |
| **`chrome-only`** | **Original Chrome Version** | Google Chrome | Chrome MV3 (`service_worker`, `side_panel`) |

To switch branches:
```bash
# Switch to Cross-Browser branch
git checkout combined

# Switch to Original Chrome branch
git checkout chrome-only
```

---

## Keyboard Shortcuts

| Shortcut | Action |
| :--- | :--- |
| **⌘ + Shift + P** (Mac) / **Ctrl + M** (Win/Linux) | Open or close the in-page prompt panel |
| **↑ / ↓** | Navigate the prompt list |
| **Enter** | Select a prompt |
| **Esc** | Close the panel |

You can change the open/close shortcut in Settings → **Record shortcut**.

---

## Testing

Automated tests use **Puppeteer** and **Jest**. See [TESTING.md](TESTING.md) for setup and execution commands.

---

## Privacy

- Your prompt library is stored **locally** in the browser (`chrome.storage.local` / `browser.storage.local`)
- Nothing is sent to external servers unless **you** choose to import from the [Open Prompt Database](https://openpromptdatabase.com/) — that flow only pulls the prompt you selected into your local library
- Zero analytics or tracking

---

## License

MIT License — see [LICENSE](LICENSE) if present in the repository.

---

## Attributions

- **Hexodus** — bug reports and fixes
- **Abdallahheidar** — ideas, contributions, and teamwork
- **HideMaru** — extension icon ([Flaticon chatbot icons](https://www.flaticon.com/free-icons/chatbot))
