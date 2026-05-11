<div align="center">

# 🌍 Multilingual Companion
### Real-Time NLP Translation & Text-to-Speech Desktop Application

*Bridging languages through an intuitive, voice-enabled desktop experience.*

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Tkinter](https://img.shields.io/badge/GUI-Tkinter-orange)
![googletrans](https://img.shields.io/badge/NLP-googletrans-4285F4?logo=googletranslate&logoColor=white)
![gTTS](https://img.shields.io/badge/TTS-gTTS-red)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Stable-brightgreen)

</div>

---

## 📌 Overview

**Multilingual Companion** is a lightweight Python desktop application that performs **real-time text translation across 100+ languages** and converts the translated output into **natural-sounding speech**. It combines a clean Tkinter GUI with the Google Translate and Google Text-to-Speech engines to deliver a single, unified workflow: *type → translate → hear*.

The goal was to remove friction from multilingual communication and language learning by collapsing several common tasks (translation, pronunciation lookup, audio playback) into one interface.

---

## 🧩 Problem Statement

Most everyday translation workflows require switching between multiple tools — one tab for translation, another for pronunciation, another to play the audio. For language learners, travelers, and accessibility users (especially visually-impaired users who depend on speech output), this fragmentation slows comprehension and limits usability.

There is a need for a **single, offline-launchable desktop tool** that:

- Translates text between a wide range of languages instantly.
- Speaks the translation aloud in the target language’s pronunciation.
- Stays simple enough for non-technical users to operate.

---

## 💡 Solution Overview

Multilingual Companion solves the above by integrating three components into one Tkinter-based GUI:

1. **NLP Translation Layer** — `googletrans` handles source-to-target language conversion across the full Google Translate language set.
2. **Speech Synthesis Layer** — `gTTS` (Google Text-to-Speech) converts the translated text into an MP3 audio stream in the destination language.
3. **Audio Playback Layer** — `pygame.mixer` streams the generated MP3 in real time, with controls to stop playback and reset the session.

The result is a focused, single-screen application where a user enters text, picks a source and target language, and gets both the translated text and its audio rendering with one click.

---

## ✨ Key Features

- **🌐 100+ Language Support** — Source and target languages dynamically populated from the `googletrans.LANGUAGES` dictionary.
- **🔊 Integrated Text-to-Speech** — Translated text is auto-rendered as speech in the destination language’s native accent.
- **⚡ Real-Time Translation Pipeline** — Translation, MP3 generation, and audio playback all execute in a single click.
- **🪟 Clean Tkinter GUI** — Color-themed, dual-pane layout with source/destination text areas and dropdown language selectors.
- **🔁 Session Reset Flow** — Built-in dialog asks the user whether to continue or exit, cleanly stopping audio and clearing buffers.
- **🛡️ Robust Error Handling** — Network failures, API errors, file permission issues, and audio playback faults are caught and logged gracefully.
- **♿ Accessibility Use-Case** — Audio output makes the tool usable by visually-impaired users and language learners alike.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Python 3.8+ |
| **GUI Framework** | Tkinter, ttk |
| **NLP / Translation** | googletrans (Google Translate API wrapper) |
| **Speech Synthesis** | gTTS (Google Text-to-Speech) |
| **Audio Playback** | pygame.mixer |
| **File I/O** | os (MP3 read/write & cleanup) |
| **Version Control** | Git, GitHub |

---

## 🏗️ Architecture & Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                  Tkinter GUI (User Interface)                   │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────────┐     │
│  │  Source Text │   │ Lang Dropdowns│   │ Destination Text │    │
│  └──────┬───────┘   └──────┬───────┘    └────────▲─────────┘    │
└─────────┼──────────────────┼─────────────────────┼──────────────┘
          │                  │                     │
          ▼                  ▼                     │
   ┌────────────────────────────────────┐          │
   │   Translation Engine (googletrans) │──────────┘
   │   src_lang → dest_lang             │
   └──────────────┬─────────────────────┘
                  │ translated_text
                  ▼
   ┌────────────────────────────────────┐
   │   Speech Synthesis (gTTS)          │
   │   → output.mp3                     │
   └──────────────┬─────────────────────┘
                  ▼
   ┌────────────────────────────────────┐
   │   Audio Playback (pygame.mixer)    │
   │   → speaker output                 │
   └──────────────┬─────────────────────┘
                  ▼
        Session reset / cleanup
```

**Workflow:**
1. User types text into the source pane and selects source + destination languages.
2. On **Translate and Speak**, `change()` calls `Translator().translate()` to produce the translated string.
3. Translated text is written to the destination pane and passed to `text_to_speech()`, which generates `output.mp3` via gTTS.
4. `play_audio()` initializes `pygame.mixer` and plays the MP3 until completion.
5. `ask_to_use_again()` prompts the user — clearing text boxes and deleting `output.mp3` on continue, or exiting cleanly on dismiss.

---

## ⚙️ Installation

### Prerequisites
- Python 3.8 or higher
- pip
- An active internet connection (googletrans and gTTS hit Google’s endpoints)

### Setup

```bash
# 1. Clone the repository
git clone https://github.com/sumedhbetgeri/multilingual-companion.git
cd multilingual-companion

# 2. (Recommended) Create a virtual environment
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install -r requirements.txt
```

### `requirements.txt`

```
googletrans==4.0.0-rc1
gTTS>=2.3.0
pygame>=2.5.0
```

> **Note:** `googletrans==4.0.0-rc1` is required because the stable release has known API-breakage issues. Tkinter ships with Python by default on Windows/macOS; on Linux, install via `sudo apt install python3-tk`.

---

## ▶️ Usage

```bash
python main.py
```

1. The Translator window opens.
2. Enter text into the **Source Text** box.
3. Pick a **source language** and **destination language** from the dropdowns.
4. Click **Translate and Speak** — translated text appears below and the audio plays automatically.
5. When prompted, choose to continue (clears the session) or close the app.

---

## 📸 Screenshots

> _Add screenshots/GIFs into a `/screenshots` folder and reference them here._

| Main Interface | Translation in Action | Audio Playback |
|---|---|---|
| ![Main UI](screenshots/main_ui.png) | ![Translation](screenshots/translation_demo.png) | ![Audio](screenshots/audio_playback.gif) |

---

## 🔭 Future Improvements

- **Speech-to-Text Input** — integrate `SpeechRecognition` so users can speak the source text instead of typing.
- **Offline Translation Mode** — fall back to a local model (e.g., `argos-translate` or a fine-tuned MarianMT) when the network is unavailable.
- **Modern UI** — migrate from Tkinter to `customtkinter` or `PyQt6` for a contemporary look.
- **Conversation Mode** — two-way back-and-forth translation for live bilingual conversations.
- **Web Deployment** — port the core pipeline to a Flask/Streamlit web app for cross-platform access.
- **Voice Cloning / Multiple Voices** — replace gTTS with a richer TTS engine (Coqui TTS, ElevenLabs API) for natural prosody.
- **History & Favorites** — local SQLite store of past translations with export to CSV.
- **Packaging** — bundle as a standalone `.exe` / `.app` via PyInstaller.

---

## 🎯 Learning Outcomes

Building this project deepened my hands-on understanding of:

- **NLP fundamentals** — language detection, source/target language pairs, and the practical limits of API-based translation.
- **Speech synthesis pipelines** — generating, persisting, and streaming audio output programmatically.
- **GUI engineering with Tkinter** — layout management with `Frame`/`grid`, ttk widgets, event-driven design, and modal dialogs.
- **Exception-safe design** — wrapping network and file I/O in granular try/except blocks for production-grade robustness.
- **Resource lifecycle management** — ensuring audio files are released by `pygame.mixer` before deletion to avoid `PermissionError` on Windows.
- **API integration** — working with third-party Python wrappers (googletrans, gTTS) and reasoning about version pinning.

---

## 📁 Project Structure

```
multilingual-companion/
├── main.py                  # Main application entry point
├── requirements.txt         # Python dependencies
├── README.md                # Project documentation
├── LICENSE                  # MIT License
├── .gitignore               # Ignored files (venv, __pycache__, *.mp3)
├── screenshots/             # UI screenshots and demo GIFs
│   ├── main_ui.png
│   ├── translation_demo.png
│   └── audio_playback.gif
└── docs/                    # Supplementary documentation
    └── architecture.md
```

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/awesome-feature`)
3. Commit your changes (`git commit -m 'Add awesome feature'`)
4. Push to the branch (`git push origin feature/awesome-feature`)
5. Open a Pull Request

For major changes, please open an issue first to discuss what you’d like to change.

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Sumedh Betgeri**
Computer Science Engineering — KLS Gogte Institute of Technology
🔗 [LinkedIn](https://linkedin.com/in/sumedhbetgeri) • [GitHub](https://github.com/sumedhbetgeri) • 📧 sumedhbetgeri@gmail.com

---

<div align="center">

⭐ **If you found this project useful, consider giving it a star — it helps a lot!** ⭐

</div>
