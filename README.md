# 🔐 CryptoViz — AES Mode Visualizer

> An interactive browser-based tool that visually demonstrates the differences between AES encryption modes: **ECB**, **CBC**, and **CTR** — using real image encryption.

---

## 👥 Team Members

- **Rajab** — Project Lead & Architecture
- **Anas** — Frontend Development
- **Ahmad** — Encryption & Cryptography
- **Zain** — UI/UX & Testing

---

## 📌 What It Does

Upload any image, enter a password, and watch how three different AES modes encrypt it in real-time. This tool lets you:

- **Encrypt** images using ECB, CBC, and CTR modes simultaneously
- **See why ECB fails** — patterns leak through, revealing the original image structure
- **Analyze block patterns** — identical blocks get highlighted with matching colors
- **Review pixel histograms** — strong encryption creates a perfectly flat distribution
- **Test randomness quality** using an AI-powered analyzer with statistical metrics
- **Run the Avalanche Effect** — change 1 bit and observe the cascading byte changes
- **Verify decryption** — confirm all three modes decrypt back to the original

---

## 🧠 The Core Concept

| Mode | How It Works | Security |
|------|-------------|----------|
| **ECB** | Each 16-byte block encrypted independently | ❌ Weak — identical blocks produce identical ciphertext |
| **CBC** | Each block XOR'd with previous ciphertext before encryption | ✅ Good — requires random IV |
| **CTR** | AES used as a keystream generator with a counter | ⭐ Best — parallelizable, no padding needed |

ECB's weakness is visible to the naked eye — the structure of the original image leaks through the encryption. CBC and CTR produce visually random output.

---

## 🗂️ Project Structure

```
├── index.html          # Main UI — all sections and canvases
├── style.css           # Dark theme styling (JetBrains Mono + Syne fonts)
├── js/
│   ├── app.js          # Main integration — event handlers, state, orchestration
│   ├── crypto.js       # AES-ECB, AES-CBC, AES-CTR encrypt/decrypt + key generation
│   ├── block.js        # Block pattern analysis and color-coded canvas rendering
│   ├── histogram.js    # Pixel frequency histogram using Chart.js
│   └── image.js        # Image upload, canvas rendering, RGB extraction
│   └── entropy.js      # AI randomness analyzer
```

---

## 🚀 How to Run

This is a pure frontend project — no build process required.

1. Clone or download the repository
2. Serve the project locally (ES modules need an HTTP server):

```bash
# Option 1: Using Python
python3 -m http.server 5500

# Option 2: Using Node.js
npx serve .
```

3. Open your browser and visit `http://localhost:5500`

> **Important:** Must run over HTTP — the Web Crypto API and ES modules require a secure server context.

---

## 🔑 How the Encryption Key Works

```
Your Password
    ↓
SHA-256 Hashing
    ↓
256-bit AES Key (displayed as hexadecimal)
    ↓
ECB Mode  →  No IV, each block encrypted independently
CBC Mode  →  Unique random IV generated per session
CTR Mode  →  Unique random nonce generated per session
```

**Security:** Your password never leaves the browser. All encryption happens client-side using the native Web Crypto API.

---

## 📦 Dependencies

| Library | Version | Purpose |
|---------|---------|---------|
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Real-time pixel histogram visualization |
| Web Crypto API | Native | AES encryption/decryption engine |
| Google Fonts | Latest | JetBrains Mono & Syne typography |

**Note:** No npm installation required — all external libraries are loaded via CDN.

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 🤝 Contributing

This is a collaborative project by our team. For questions or suggestions, feel free to reach out to any team member!

```
MIT License

Copyright (c) 2025 CryptoViz Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🔒 Security Note

This tool is built for **educational purposes only**. The ECB mode implementation simulates ECB using Web Crypto's CBC with a zero IV — this is intentionally insecure to demonstrate ECB's weaknesses. Do not use this code in production cryptographic systems.
