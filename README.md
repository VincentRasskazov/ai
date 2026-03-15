# VincentAI | Temu ChatGPT

This project was built with **AI assistance** and is **not actively maintained**. Some parts may be messy, experimental, or contain sensitive configuration. Please avoid digging into or reusing internal secrets.

---

## 🚀 Features

* **Multi-Model Interface:** Access DeepSeek V3.2, Copilot, Llama 3.3, and more.
* **WebGPU Support:** Run models locally in your browser (Phi-3, Gemma, Mistral) using the GPU cache.
* **Customization:** Personalize the AI persona name, system instructions, accent colors, and background images.
* **Privacy First:** Includes an **Incognito / Temp Mode** where chats are not saved to history.
* **Authentication:** Google Sign-In integration for persistent chat history across sessions.
* **PWA Ready:** Includes service worker registration for offline capabilities and manifest support.

---

## 🛠️ Configuration

To get this project running fully, you need to update the following constants in the `<script>` section of the `index.html`:

1.  **Backend URL:** `const BACKEND_URL = "https://your-backend-api.com";`
2.  **Google Client ID:** `const GOOGLE_CLIENT_ID = "YOUR_GOOGLE_CLIENT_ID_HERE";`

---

## 📦 Tech Stack

* **Frontend:** HTML5, CSS3 (Custom Properties), Vanilla JavaScript.
* **Libraries:** * [FontAwesome](https://fontawesome.com) (Icons)
    * [Marked.js](https://marked.js.org/) (Markdown rendering)
    * [Highlight.js](https://highlightjs.org/) (Code syntax highlighting)
    * [WebLLM](https://webllm.mlc.ai/) (Local Browser AI)
* **Storage:** Browser `localStorage` for guest chats and settings.

---

## ⚖️ License

This project is licensed under the **MIT License**.

---

### ⚠️ Disclaimer
This is a "Temu-style" experimental interface. Use at your own risk. The local WebGPU models require a compatible browser (Chrome/Edge) and sufficient VRAM to function correctly.
