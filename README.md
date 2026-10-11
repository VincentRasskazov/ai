# Vincent AI Backend Infrastructure

This repository contains the core backend infrastructure for a multi-tenant B2B AI lead generation agency. The system is designed to deploy, manage, and monitor custom AI sales assistants for local service businesses without manual database intervention.

## Architecture Overview

The backend is built on Python and Flask, utilizing Server-Sent Events (SSE) to handle streaming responses from AI providers. It acts as a middleware layer between the client-facing chat widgets and the database, enforcing strict lead-capture rules before routing data to business owners.

The system is fully integrated with the Model Context Protocol (MCP), allowing the database to be manipulated directly via natural language from an authenticated Google Workspace environment.

## Core Features

* **Multi-Tenant Data Segregation:** Client knowledge bases, routing emails, and active states are securely isolated in Firebase Firestore. 
* **MCP Automation Pipeline:** Includes a custom `batch_process_clients` JSON-RPC tool. This allows an LLM to scrape business targets, format their data, and insert them directly into the production database in a single transaction while ignoring duplicates.
* **Anti-Spam Lead Catcher:** A regex-based interception engine scans the AI's output stream in real-time. When a lead (Name/Phone/Details) is detected, the stream is intercepted, the data is routed to the client via the Resend API, and a hard-lock prevents duplicate emails within the same session.
* **Telemetry & Logging:** Every interaction is logged in a hierarchical structure (`Client ID -> Conversation ID -> Messages`). This data feeds directly into a secure client dashboard to prove ROI and debug prompt hallucinations.
* **CORS & Pre-flight Bypass:** Engineered to handle strict cross-origin resource sharing requirements and reverse-proxy buffering, ensuring stable SSE connections from static HTML embeds on client websites.

## Tech Stack

* **Backend:** Python, Flask, Flask-CORS
* **Database:** Firebase Admin SDK (Firestore)
* **Email Routing:** Resend API, Cloudflare Email Routing
* **Transport:** Server-Sent Events (SSE)
* **Automation:** Model Context Protocol (MCP)

## Environment Setup

To run this server locally or deploy to production, the following environment variables are required:

* `PORT`: The port the server will bind to (default: 10000).
* `FIREBASE_SERVICE_ACCOUNT`: Stringified JSON of the Firebase Admin service account key.
* `RESEND_API_KEY`: API key for transactional lead emails.

## Deployment Notes

This application is optimized for deployment on Render. The server explicitly forces `X-Accel-Buffering: no` and `Cache-Control: no-transform` in the response headers to prevent Render's internal proxies from buffering the SSE stream and causing client-side timeouts.
