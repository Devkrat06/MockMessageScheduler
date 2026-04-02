# WhatsApp Message Scheduler (API-Based)

A production-grade message scheduling system built with a Chrome Extension + Node.js backend

A backend-driven message scheduling system built with a Chrome Extension and Node.js.

This project allows users to schedule messages for future delivery using a reliable queue system. It is designed to avoid modifying WhatsApp Web or relying on fragile browser automation.

---

## Overview

This system enables users to create scheduled messages through a Chrome extension. The backend handles storage, scheduling, and execution using a queue and worker model. Messages are currently processed in a mock mode for safe development.

---

## Features

* Schedule messages for a specific time
* Backend-based scheduling (no reliance on browser timers)
* Persistent storage using PostgreSQL
* Queue-based execution using Redis and BullMQ
* Retry handling with exponential backoff
* Chrome Extension interface for creating and managing schedules
* Mock messaging mode for safe testing

---

## What This Project Does Not Do

* Does not modify or inject into WhatsApp Web
* Does not automate clicks or simulate user behavior
* Does not bypass WhatsApp platform restrictions
* Does not support bulk or spam messaging
* Does not function as a personal WhatsApp automation tool

---

## Architecture

```
Chrome Extension (UI)
        ↓
Backend API (Node.js)
        ↓
PostgreSQL (data storage)
        ↓
Redis + BullMQ (job queue)
        ↓
Worker (job execution)
        ↓
Messaging Service (Mock or API)
```

---

## How It Works

1. A user schedules a message through the extension
2. The extension sends the request to the backend
3. The backend stores the schedule in the database
4. A job is added to the queue
5. The worker processes the job at the scheduled time
6. The messaging service handles delivery (mock or API)

---

## Technologies Used

* Node.js (Express)
* PostgreSQL with Prisma ORM
* Redis with BullMQ
* Chrome Extension (Manifest V3)

---

## Messaging Mode

By default, the system runs in mock mode:

```
WHATSAPP_PROVIDER=mock
```

In this mode, messages are not sent to WhatsApp. Instead, they are logged by the backend to simulate delivery.

---

## Optional Integration

The system can be extended to use the official WhatsApp Business API:

WhatsApp Business Platform

This requires:

* A verified business account
* An approved phone number
* Pre-approved message templates
* User opt-in

---

## Limitations

* Cannot send standard personal chat messages through WhatsApp
* Requires templates for real message delivery via API
* Extension operates independently of WhatsApp interface
* No real message delivery in mock mode

---

## Development Challenges

* Handling Chrome Extension Manifest V3 service worker limitations
* Designing reliable scheduling without browser timers
* Implementing retry and idempotency logic
* Managing local development with Docker, PostgreSQL, and Redis
* Resolving file locking issues on Windows environments
* Understanding constraints of the WhatsApp Business API

---

## Advantages

* Compliant with platform guidelines
* Stable and maintainable architecture
* Fault-tolerant execution with retries
* Clear separation between UI, backend, and messaging layer
* Extensible for production use

---

## Trade-offs

* Does not integrate directly into WhatsApp interface
* Requires backend infrastructure
* Real message delivery is constrained by API rules
* Initial setup complexity is higher than simple scripts

---

## Setup

### Backend

```
cd backend
npm install
npx prisma migrate dev
npm start
```

### Services

```
docker compose up -d
```

### Extension

1. Open Chrome and go to `chrome://extensions/`
2. Enable Developer Mode
3. Click "Load Unpacked"
4. Select the `extension/` folder

---

## Notes

This project is intended for learning system design, backend architecture, and safe API integration. It is not designed for bypassing platform restrictions or automating personal messaging.

---

## Author

Developed as a full-stack project demonstrating queue-based scheduling, backend systems design, and structured application architecture.

---

