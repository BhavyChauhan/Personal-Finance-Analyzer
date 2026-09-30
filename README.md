# SciFiVerse

A living digital universe for communication — Flask + SQLite + Flask-SocketIO
backend, JWT auth, and a single-file vanilla HTML5/CSS3/JS frontend.

## Run it

```bash
pip install flask flask-socketio pyjwt werkzeug eventlet
python3 main.py
```

Then open **http://localhost:5000**.

The SQLite database (`scifiverse.db`) and JWT secret (`.secret`) are created
automatically in the same folder on first run.

## What's inside

- **`main.py`** — Flask + Flask-SocketIO backend: JWT authentication, a REST
  endpoint for every screen, WebSocket events for live messages / typing /
  presence / notifications, the full SQLite schema (users, profiles,
  friends, messages, signals, portals, communities, posts, achievements,
  projects, notifications, settings, uploads), rate limiting, input
  validation, and a provider-agnostic AI Copilot placeholder
  (`generate_ai_reply()` — swap in a real OpenAI or local-LLM call whenever
  you're ready).
- **`index.html`** — the entire SPA frontend in one file: realistic starfield
  canvas, glassmorphism, a circular navigation dock, and all 11 screens —
  Universe, Signals, Quantum Chat, Portals, Explore Universe, Planet
  Profile, Solar Systems, AI Copilot, Notifications, Create, and Settings.
  All CSS and JavaScript live inside this file, as specified.

## Notes on scope

- "AES-256 encryption" is **simulated** for this demo (see
  `simulate_aes_encrypt()` in `main.py`) — genuine end-to-end encryption
  needs keys generated on-device that the server never sees. The UI treats
  messages as encrypted and the Quantum Encryption Dashboard is transparent
  that this is a demo status display, not a security guarantee.
- Signal/Portal/file "uploads" are tracked as metadata (filename, kind,
  size) rather than real binary storage, to keep the footprint to the
  requested `main.py` + `index.html` + SQLite stack.
- The AI Copilot ships with canned, provider-agnostic placeholder replies —
  point `generate_ai_reply()` at OpenAI or a local LLM to make it real.
- Two users can message each other in real time immediately after both are
  registered — friend/follow is auto-accepted in this build to keep the
  Universe view populated quickly for a demo; swap in a request/accept flow
  if you want gated connections.
