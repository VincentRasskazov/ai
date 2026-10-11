# Vincent AI - Frontend Interfaces

Lightweight, vanilla JavaScript frontend for the Vincent AI B2B lead generation platform. 

This repository contains the static client-facing web apps. There is no build step, no framework bloat, and no package manager required. It relies entirely on native browser APIs and Server-Sent Events (SSE) to stream markdown-formatted responses in real-time from the Python/Flask backend.

## Architecture

* **Framework:** Vanilla HTML / CSS / JS
* **Markdown Parsing:** Marked.js (via CDN)
* **API Communication:** `fetch` API handling chunked SSE streams
* **State Management:** URL Parameters + Local JS Memory

## Core Files

### 1. demo.html (The Chat Widget)
The primary interactive interface for prospective customers. It is designed to act as a standalone landing page or an embeddable iframe. 

**Routing:**
Requires a valid `client` URL parameter to initialize. 
`[https://vincentrasskazov.com.au/ai/demo.html?client=smith-plumbing](https://vincentrasskazov.com.au/ai/demo.html?client=smith-plumbing)`

**Mechanics:**
* Generates a unique `conversation_id` on page load to group session data.
* Intercepts standard form submissions to prevent page reloads.
* Reads chunked data from the backend stream and dynamically updates the DOM using `requestAnimationFrame` for high-performance text rendering.
* Handles 403 Forbidden errors if the requested client ID is inactive or missing from the Firestore database.

### 2. logs.html (The Client Dashboard)
A secure, read-only dashboard for business owners to review their AI's chat transcripts and verify captured leads.

**Routing:**
Requires a `client` parameter. Optionally accepts a `conv` parameter to auto-focus a specific session.
`[https://vincentrasskazov.com.au/ai/logs.html?client=smith-plumbing&conv=sess_abc123](https://vincentrasskazov.com.au/ai/logs.html?client=smith-plumbing&conv=sess_abc123)`

**Mechanics:**
* Fetches the 20 most recent conversations from the backend REST API.
* Constructs a two-pane UI (sidebar for sessions, main panel for transcripts).
* Parses raw database timestamps into localized `en-AU` formats.

## Deployment

These files are designed to be statically hosted via GitHub Pages (or any basic web server). 

Because the architecture is entirely decoupled, all environment variables and database credentials live exclusively on the backend server. The frontend only needs to know the public URL of the REST API (currently hardcoded to the Render production environment).

## Development Setup

To run locally for testing or CSS modifications, simply serve the directory using Python's built-in HTTP server:

```bash
python -m http.server 8000
```

Then open your browser to:
`http://localhost:8000/demo.html?client=test-client`
