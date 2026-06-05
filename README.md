# 🌍 AI Language Translation Tool

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.x-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![deep_translator](https://img.shields.io/badge/deep__translator-1.x-00B894?style=for-the-badge)
![langdetect](https://img.shields.io/badge/langdetect-NLP-6C5CE7?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)
![API Key](https://img.shields.io/badge/API%20Key-Not%20Required-0984E3?style=for-the-badge)

**A smart, real-time language translation web app supporting 22+ languages — with automatic language detection, translation history, session statistics, and a clean dark-themed UI. No paid API key required.**

[🚀 Quick Start](#getting-started) · [✨ Features](#features) · [🏗️ Architecture](#architecture) · [📸 Screenshots](#screenshots) · [🌐 Supported Languages](#supported-languages)

</div>

---

## 📌 Project Overview

Built as **Task 01** of the AI Internship at **CodeAlpha** to explore Natural Language Processing (NLP), automatic language detection, and interactive Python web application development.

This tool wraps Google Translate's free tier via `deep_translator` and pairs it with `langdetect` for automatic source-language identification — delivering a polished, production-quality translation experience entirely in Python, with zero API billing.

| | Details |
|---|---|
| **Developer** | Rashid Ahmad |
| **Internship** | CodeAlpha — AI Internship Task 01 |
| **Domain** | Natural Language Processing (NLP) |
| **Backend** | Python + deep_translator + langdetect |
| **Frontend** | Streamlit (dark-themed UI) |
| **Languages** | 22+ (see full list below) |
| **API Key** | ❌ Not required |

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔤 **Real-Time Translation** | Instant text translation across 22+ languages as you type |
| 🔍 **Auto Language Detection** | Automatically identifies the source language using `langdetect` |
| 🔁 **Source ↔ Target Swap** | One-click swap of source and target languages |
| 📜 **Translation History** | Scrollable log of all translations within the session |
| 📊 **Session Statistics** | Live count of total translations, characters processed, and unique languages used |
| 🔢 **Character Counter** | Real-time character count on input and output fields |
| 🌙 **Dark-Themed UI** | Clean, readable dark interface built with Streamlit's theming system |
| 💾 **No API Key Needed** | Uses `deep_translator`'s free Google Translate integration |

---

## 🏗️ Architecture

```
User Input (Text)
        │
        ▼
┌─────────────────────────────────┐
│         langdetect              │
│  detect(text) → language code   │
│  e.g. "en", "fr", "ar", "ur"   │
└──────────────┬──────────────────┘
               │  detected source lang
               ▼
┌─────────────────────────────────┐
│       deep_translator           │
│  GoogleTranslator(             │
│    source = detected_lang,      │
│    target = user_selected_lang  │
│  ).translate(text)              │
└──────────────┬──────────────────┘
               │  translated string
               ▼
┌─────────────────────────────────┐
│        Streamlit UI             │
│  • Output text box              │
│  • History log append           │
│  • Session stats update         │
│  • Character count refresh      │
└─────────────────────────────────┘
```

### Component Breakdown

```
ai_language_translator/
│
├── app.py                  # Main Streamlit application entry point
│
├── core/
│   ├── translator.py       # deep_translator wrapper + error handling
│   ├── detector.py         # langdetect wrapper with fallback logic
│   └── languages.py        # Supported language map {name: code}
│
├── ui/
│   ├── components.py       # Reusable Streamlit UI components
│   └── styles.py           # Custom CSS for dark theme
│
├── utils/
│   └── history.py          # Session history manager
│
├── requirements.txt
└── README.md
```

---

## 🌐 Supported Languages

| # | Language | Code | # | Language | Code |
|---|----------|------|---|----------|------|
| 1 | English | `en` | 12 | Turkish | `tr` |
| 2 | Urdu | `ur` | 13 | Dutch | `nl` |
| 3 | Arabic | `ar` | 14 | Polish | `pl` |
| 4 | French | `fr` | 15 | Swedish | `sv` |
| 5 | Spanish | `es` | 16 | Danish | `da` |
| 6 | German | `de` | 17 | Finnish | `fi` |
| 7 | Chinese (Simplified) | `zh-CN` | 18 | Greek | `el` |
| 8 | Japanese | `ja` | 19 | Hebrew | `he` |
| 9 | Korean | `ko` | 20 | Indonesian | `id` |
| 10 | Russian | `ru` | 21 | Malay | `ms` |
| 11 | Italian | `it` | 22 | Thai | `th` |

> Total: **22+ languages** supported. `deep_translator` supports 100+ — easily extendable by adding entries to the language map.

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or higher
- pip

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/rashidahmad/ai-language-translator.git
cd ai-language-translator

# 2. (Optional but recommended) Create a virtual environment
python -m venv venv
source venv/bin/activate        # Linux / macOS
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the app
streamlit run app.py
```

The app opens automatically at `http://localhost:8501`

### Google Colab

```python
!pip install streamlit deep_translator langdetect pyngrok -q

# Run with public URL via pyngrok
from pyngrok import ngrok
import subprocess

proc = subprocess.Popen(["streamlit", "run", "app.py", "--server.port", "8501"])
public_url = ngrok.connect(8501)
print(f"🌍 App running at: {public_url}")
```

---

## 📦 Requirements

```
streamlit>=1.28
deep-translator>=1.11
langdetect>=1.0.9
```

```bash
pip install -r requirements.txt
```

---

## 🔬 How It Works

### 1. Automatic Language Detection

```python
from langdetect import detect

detected_lang = detect(user_input_text)
# Returns ISO 639-1 code: "en", "fr", "ar", "ur", etc.
```

`langdetect` is a Python port of Google's language detection library. It uses a Naive Bayes classifier trained on Wikipedia data to identify the language of a given string. Accuracy is high for texts longer than ~20 characters.

### 2. Translation

```python
from deep_translator import GoogleTranslator

translated = GoogleTranslator(
    source=detected_lang,   # or "auto"
    target=target_lang_code
).translate(text)
```

`deep_translator` wraps Google Translate's free web endpoint — no API key, no billing, no rate-limit registration. Suitable for personal projects and internship-scale usage.

### 3. Source ↔ Target Swap

When the user clicks the swap button:
1. The current target language becomes the new source
2. The translated output becomes the new input text
3. A fresh translation is triggered automatically

### 4. Session Statistics

Streamlit's `st.session_state` persists data across reruns within a session:

```python
st.session_state.total_translations += 1
st.session_state.total_characters   += len(input_text)
st.session_state.languages_used.add(target_language)
st.session_state.history.append({
    "source" : detected_lang,
    "target" : target_lang,
    "input"  : input_text,
    "output" : translated_text,
    "time"   : datetime.now().strftime("%H:%M:%S")
})
```

---

## 📸 Screenshots

```
┌──────────────────────────────────────────────────────────┐
│  🌍 AI Language Translation Tool          [Dark Theme]   │
├──────────────────────────────────────────────────────────┤
│  Source Language: [Auto Detect ▼]  ⇄  Target: [Urdu ▼]  │
│                                                          │
│  ┌──────────────────────┐  ┌──────────────────────────┐ │
│  │ Enter text here...   │  │ ترجمہ یہاں ظاہر ہوگا   │ │
│  │                      │  │                          │ │
│  │ Detected: English    │  │                          │ │
│  │ 0 / 5000 chars       │  │ 0 chars                  │ │
│  └──────────────────────┘  └──────────────────────────┘ │
│                                                          │
│  [🔄 Translate]  [🔁 Swap]  [🗑️ Clear]                  │
│                                                          │
│  📊 Session Stats                                        │
│  Translations: 0 | Characters: 0 | Languages Used: 0    │
│                                                          │
│  📜 Translation History                                  │
│  ──────────────────────────────────────────────────────  │
└──────────────────────────────────────────────────────────┘
```

---

## 🧪 Experiment Ideas

| Idea | How to Try |
|------|-----------|
| Translate a poem | Paste Urdu/Arabic poetry — observe how structure carries across |
| Detection accuracy | Input mixed-language text — see how `langdetect` handles code-switching |
| Round-trip translation | Translate EN→FR→DE→EN — measure semantic drift |
| Extend languages | Add `"Swahili": "sw"` to the language map — zero other changes needed |
| Batch translation | Modify `translator.py` to accept a list of strings for bulk processing |

---

## ⚠️ Limitations

- `langdetect` requires at least ~20 characters for reliable detection; very short strings may misclassify
- `deep_translator` uses the free Google Translate tier — subject to Google's unofficial rate limits under heavy use
- Translation quality matches Google Translate, which can be imperfect for low-resource languages
- No offline mode — an active internet connection is required for translation

---

## 🗺️ Roadmap

- [ ] Text-to-speech output (gTTS integration)
- [ ] File upload support (`.txt`, `.pdf`)
- [ ] CSV export of translation history
- [ ] Confidence score display from `langdetect`
- [ ] Support for 50+ languages via expanded language map
- [ ] Offline mode via `argostranslate`

---

## 📚 References

- Nakatani, S. (2010). *langdetect — Language Detection Library for Java.* (Python port by Mimino666)
- `deep-translator` — [pypi.org/project/deep-translator](https://pypi.org/project/deep-translator/)
- Streamlit Documentation — [docs.streamlit.io](https://docs.streamlit.io)

---

## 📄 License

MIT License — free to use, modify, and distribute with attribution.

---

## 🙏 Acknowledgements

- **CodeAlpha** for the AI Internship framework and task structure
- The `deep-translator` open-source contributors
- The `langdetect` Python port maintainers

---

<div align="center">

**Developed by Rashid Ahmad · CodeAlpha AI Internship · Task 01**

*"Language is the road map of a culture. It tells you where its people come from and where they are going." — Rita Mae Brown*

</div>
