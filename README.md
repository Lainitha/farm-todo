# Farm Todo (Todo List)

A small full-stack Todo List app with a FastAPI backend (MongoDB) and a React frontend, packaged to run with Docker Compose. This project is a minimal, practical example for learning and demonstration purposes. ✅

---

## Contents
- **Backend**: Python (FastAPI) — `backend/`
- **Frontend**: React — `frontend/`
- **Nginx**: Simple reverse-proxy for frontend and API — `nginx/`
- **Compose**: Local orchestration — `compose.yaml`

---

## Features ✨
- Create, list, and delete todo lists
- Add, check/uncheck, and delete items inside a list
- Simple JSON REST API at `/api/*`
- Docker Compose setup with Nginx reverse proxy

---

## Quick Start (Docker) 🐳
1. Create a `.env` in the project root with at least:

```env
MONGODB_URI=mongodb://<user>:<pass>@<host>:<port>/<db>
```

2. Build and run with Docker Compose:

```bash
docker compose up --build
```

3. Open the app in your browser:

- App + proxy: http://localhost:8000
- Frontend direct (dev server): http://localhost:3000
- Backend (API): http://localhost:8001/api or via nginx at http://localhost:8000/api

---

## Local Development (without Docker) 🔧

Backend

1. Create a virtual environment and install dependencies:

```bash
python -m venv .venv
. .venv/bin/activate   # or .venv\Scripts\activate on Windows
pip install -r backend/requirements.txt
```

2. Set environment variables:

```bash
export MONGODB_URI="mongodb://..."  # Windows PowerShell: $env:MONGODB_URI = "..."
export DEBUG=true
```

3. Run the server:

```bash
python backend/src/server.py
```

API will be available at http://localhost:3001/api when run directly.

Frontend

1. Install dependencies and start:

```bash
cd frontend
npm install
npm start
```

The dev server runs on http://localhost:3000 by default.

---

## API (examples) 🧪

Get all lists:

```bash
curl http://localhost:8000/api/lists
```

Create a new list:

```bash
curl -X POST http://localhost:8000/api/lists -H "Content-Type: application/json" -d '{"name":"Groceries"}'
```

Add an item to a list (replace LIST_ID):

```bash
curl -X POST http://localhost:8000/api/lists/LIST_ID/items/ -H "Content-Type: application/json" -d '{"label":"Buy milk"}'
```

Toggle item checked state (PATCH):

```bash
curl -X PATCH http://localhost:8000/api/lists/LIST_ID/checked_state -H "Content-Type: application/json" -d '{"item_id":"ITEM_ID","checked_state":true}'
```

---

## Notes & Tips 💡
- `compose.yaml` maps nginx to host port **8000** and backend to **8001**. Use nginx (8000) to exercise the full stack.
- Compose expects a `.env` (it is required by the compose file). Add the `MONGODB_URI` before running compose.
- Backend uses Motor (async MongoDB driver) and Pydantic models for validation.

---

## Tests
- Frontend: `npm test` inside `frontend/` (React tests present).
- Backend: no tests included yet — contributions welcome.

---

## Contributing 🤝
Feel free to open issues or PRs. Ideas for improvement:
- Add unit & integration tests for the backend
- Add error handling & validation on the frontend
- Add user authentication

---

## License & Contact
This is a small example project — include a license of your choice if you plan to publish it (e.g., MIT).

If you want help extending the README or adding CI, testing, or deployment, tell me what you'd like next. 🔧
