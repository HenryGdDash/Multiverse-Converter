# 🌌 Multiverse Converter
**Multiverse Converter** is a sleek, high-performance, and minimalist web application designed to perform instantaneous conversions across various numeral systems, character encodings, and historical scripts. 
Instead of using traditional forms with "Submit" buttons, this tool utilizes a reactive, bidirectional architecture: **type in absolutely any field, and every other system updates in real time.**
---
## ✨ Features
* **Bidirectional Live Conversion:** Real-time computation architecture. Whether you input a Binary stream, a Roman numeral, or plain Text, the application instantly decodes the source and encodes it into all other 7 formats simultaneously.
* **Aesthetic & Modern UI:** A beautifully spaced CSS Grid layout utilizing modern typography, subtle hover transitions, and staggered loading animations for individual cards.
* **Automatic Dark Mode:** Built with native CSS Custom Properties (`--variables`) that respect the user's system preferences (`@media (prefers-color-scheme: dark)`), switching seamlessly between a crisp Light theme and a deep Cyberpunk-esque Dark theme.
* **Smart Clipboard Integration:** One-click "Copy" buttons built natively into each card header. It includes custom micro-animations and contextual color-changing states (`emerald green`) to give clear user feedback upon a successful copy.
* **Input Sanitization:** Embedded JavaScript RegEx listeners that dynamically strip away invalid characters on the fly.
---
## 🎛️ Supported Universes (Systems)
The converter handles a wide array of representations, bridging the gap between core computer science, daily language, and ancient archaeology:

| Category | System | Input Example | Description |
| :--- | :--- | :--- | :--- |
| **Computational** | Decimal | `42` | Standard Base-10 positional notation. |
| **Computational** | Binary | `101010` | Base-2 language used natively by digital hardware. |
| **Computational** | Hexadecimal | `2A` | Base-16 system heavily utilized in memory addressing. |
| **Computational** | Octal | `52` | Base-8 system often seen in Unix file permissions. |
| **Historical** | Roman Numerals | `XLII` | Additive/substantive numeric system of ancient Rome. |
| **Historical** | Egyptian Numerals | `𓎆𓎆𓎆𓎆𓏽` | Hieroglyphic tallies (*Read-only display output*). |
| **Textual** | Plain Text / ASCII | `A` | Standard character strings translated via character codes. |
| **Signal** | Morse Code | `.-` | Telecommunication method using dots and dashes. |

---
## 🛠️ Technical Deep Dive
This project was intentionally built with **Zero Dependencies** to maximize raw performance, eliminate package vulnerabilities, and achieve an incredibly lightweight footprint.
### Frontend Architecture
* **HTML5:** Semantic architecture decoupling headers, container structures, and input grids.
* **CSS3:** Uses a fluid `repeat(auto-fit, minmax(280px, 1fr))` Grid layout. Includes custom `:focus-within` selectors to elevate active cards dynamically.
* **Vanilla JavaScript (ES6+):** Utilizes key-value mapping lookups for linear character-to-signal translation and algorithms for Roman/Egyptian numeral parsing.
---
## 📂 File Structure
```text
├── index.html     # Single-file architecture containing Layout, Styling, and Logic.
└── README.md      # Project documentation (This file).
