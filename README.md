# VincentAI — Advanced Web Chat Interface

VincentAI is a custom AI chat interface built in pure HTML, CSS, and JavaScript.  
It supports multiple AI models, Google login, conversation history, file uploads, and a polished UI inspired by modern chat systems.

This project focuses on frontend engineering, API integration, and building a smooth chat experience without relying on heavy frameworks.

---

## 🚀 Features

### 🧠 Multi‑Model Support
Choose between several AI models (configured in the frontend), including:

- DeepSeek  
- Llama  
- Qwen  
- GPT‑4o mini  
- Gemma  
- Other backend‑exposed models

The model selector updates dynamically and displays the active model in the header.

---

### 💬 Chat System

- Clean, modern chat layout  
- AI messages on the left, user messages on the right  
- Markdown rendering (via `marked.js`)  
- Syntax‑highlighted code blocks (via `highlight.js`)  
- Smooth animations and auto‑scrolling  
- “Stop generating” button using `AbortController`

---

### 📁 File Upload Support

Attach a file to your message and its contents are included in the prompt context.

- Displays a file chip in the UI  
- Reads text files using `FileReader`  
- Injects file content into the backend request

---

### 🔐 Google Login (OAuth)

- Google Identity Services integration  
- Saves user profile (name + avatar)  
- Shows user info in the sidebar  
- Supports sign‑out  
- Stores user sessions in `localStorage`

---

### 🗂️ Conversation History

- Local chat history stored per user  
- Rename or delete conversations  
- Sidebar with all past chats  
- Auto‑generated titles  
- Restores state on reload

---

### 🎨 UI & Styling

- Fully custom dark theme  
- Responsive layout  
- Sidebar + main chat area  
- Smooth transitions  
- JetBrains Mono + Inter fonts  
- Font Awesome icons

---

## 🧩 Project Structure

```text
ai/
├── index.html        # Main application UI + logic
├── sitemap.xml
├── robots.txt
├── LICENSE
└── google*.html      # Google site verification
```

All logic is contained inside `index.html` for simplicity.

---

## 🔧 Backend Requirements

The frontend expects a backend endpoint:

```http
POST /chat
```

With JSON body:

```json
{
  "id": "<uuid>",
  "token": "<sha256 signature>",
  "message": "<full prompt>",
  "model": "<model-id>"
}
```

Token generation (server‑side) uses something like:

```
SHA-256(id + SECRET_SALT)
```

The backend URL is configured in the script, for example:

```js
const BACKEND_URL = "https://backendai-ablv.onrender.com";
```

---

## 🛠️ Technologies Used

- HTML5  
- CSS3  
- Vanilla JavaScript  
- Google Identity Services  
- Marked.js (Markdown parsing)  
- Highlight.js (code highlighting)  
- Font Awesome  
- LocalStorage  
- Fetch API + AbortController  

---

## 📌 Roadmap

- Add true streaming responses  
- Add settings page (model defaults, system prompts, etc.)  
- Add custom themes  
- Add export/import chat history  
- Add backend rate‑limit / status indicators  

---

## 📄 License

This project is licensed under the MIT License.

---

## ✨ Author

**Vincent**  
13‑year‑old developer exploring AI interfaces, automation, and systems thinking.
