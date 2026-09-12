# Croc-Chat (Web Crypto E2EE) 🐊🔒

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Status: Prototype](https://img.shields.io/badge/Status-Prototype-brightgreen.svg)

Croc-Chat is a browser-based, peer-to-peer (P2P) secure chat and file transfer application. It is heavily inspired by the brilliant [schollz/croc](https://github.com/schollz/croc) CLI tool, bringing the concept of secure, password-authenticated file transfers and messaging to the web without requiring any command-line knowledge or backend servers.

## ✨ Features

* **True End-to-End Encryption (E2EE):** Uses the browser's native Web Crypto API. All messages and files are encrypted locally using AES-256-GCM before transmission.
* **Peer-to-Peer (WebRTC):** Data travels directly between users via WebRTC Data Channels. No central server stores your messages or files.
* **Zero-Knowledge Signaling:** Uses a public signaling server to connect peers, but the server only sees encrypted noise and random routing IDs. 
* **Secure File Transfers:** Send files up to 100MB directly browser-to-browser. Files are chunked, encrypted, and streamed securely.
* **Ephemeral Messaging (Self-Destruct):** Set timers (15s, 1m, 5m) on your messages and files. They are automatically deleted from memory and the UI once the timer expires.
* **No Accounts or Databases:** No sign-ups, no phone numbers, and no persistent databases. When you close the tab, the session is permanently gone.
* **Modern UI:** Clean, responsive, Apple-inspired interface with built-in Light and Dark modes.

## 🚀 How It Works (The Cryptography)

Croc-Chat simulates a Password-Authenticated Key Exchange (PAKE) tailored for the web:

1. **The Code Phrase:** The host generates a phrase like `swift-eagle-123-brave-moon`.
2. **Public Routing:** The first half (`swift-eagle-123`) is used as a public room ID to find the other peer on the signaling server (via PeerJS).
3. **Private Key Derivation:** The *entire* phrase is used as a master password. It is run through `PBKDF2` with 100,000 iterations to derive a military-grade 256-bit AES-GCM session key.
4. **Secure Pipe:** Even if a malicious actor guesses the public routing ID and intercepts the connection, they cannot decrypt the data without the secret back-half (`brave-moon`) of the phrase.

## 🛠️ Usage

Because Croc-Chat uses WebRTC and native Web APIs, there is **zero installation or backend setup required**.

1. Simply open the `index.html` file in any modern web browser.
2. **Host:** Click "Generate New Code" and share the resulting code phrase with your friend securely.
3. **Join:** The friend enters the code phrase into their client and clicks "Connect".
4. Chat and share files securely!

## 🌐 Hosting on GitHub Pages

Since this is a single-file application, you can host it entirely for free using GitHub Pages:

1. Fork or clone this repository.
2. Ensure the main HTML file is named `index.html`.
3. Go to your repository **Settings** > **Pages**.
4. Select the `main` branch as the source and click **Save**.
5. Your secure chat is now live at `https://[your-username].github.io/[repository-name]`!

## 🙏 Credits & Inspiration

* **[schollz/croc](https://github.com/schollz/croc):** The core inspiration for the connection flow, PAKE-style security, and code phrase generation.
* **[PeerJS](https://peerjs.com/):** For simplifying WebRTC signaling.
* **Tailwind CSS:** For the rapid UI styling.

---
*Disclaimer: This is a prototype demonstrating Web Crypto and WebRTC capabilities. While it uses strong cryptographic primitives, it has not undergone a formal security audit. Use for educational and everyday private communication purposes.*
