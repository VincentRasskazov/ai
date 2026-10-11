# Vincent AI - Multi-Tenant B2B Sales Engine

A full-stack, multi-tenant AI infrastructure designed to deploy and manage hyper-personalized support agents for local service businesses. The system intercepts after-hours web traffic, qualifies leads in real-time, and routes them directly to business owners, operating as an automated B2B sales pipeline.

## System Architecture

The project is split into a scalable Python backend and lightweight frontend client portals, utilizing a custom Model Context Protocol (MCP) server for automated outbound sales.

* **Backend:** Python / Flask (Hosted on Render)
* **Database:** Firebase Firestore (Multi-tenant document structure)
* **Email Infrastructure:** Resend API & Cloudflare Email Routing
* **AI Integration:** Google Gemini Pro via custom SSE MCP Server
* **Frontend:** Vanilla HTML/JS/CSS (No build step required)

## Core Features

* **Multi-Tenant Database:** A single backend scales across infinite clients. Each client has a unique `client_id` controlling their specific business knowledge base, API keys, active status, and chat logs.
* **MCP Automation Pipeline:** A built-in Server-Sent Events (SSE) MCP server allows Gemini to interact directly with the production database. It batch-processes web-scraped business data, checks for existing records, injects new clients into Firestore, and drafts highly personalized cold outreach emails in a single transaction.
* **Intelligent Lead Capture:** The backend streaming engine parses AI responses in real-time. When a customer provides their contact information, the system intercepts the secure tracking tag, blocks it from the user-facing chat, and instantly dispatches a lead notification to the business owner.
* **Client Dashboards:** Unique, parameterized chat transcript portals (`logs.html?client=id&conv=id`) allow business owners to review AI performance, debug interactions, and verify ROI.


