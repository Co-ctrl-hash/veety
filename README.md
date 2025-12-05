# Vetty Crypto Market API — Short README

A compact, single-file guide for the **Vetty Crypto Market API** — a small production-style FastAPI service that fetches live crypto market data from CoinGecko and exposes JWT-protected endpoints (prices in **INR** & **CAD**).

---

## Quick features
- Live market data (INR & CAD)
- Filter by coin id(s) or category
- JWT-protected endpoints (demo credentials included)
- Health (`/health`) & version (`/version`) endpoints
- Swagger UI at `/docs`
- Unit tests with `pytest`
- `Dockerfile` included

---

## Quick start (short)
1. Create & activate venv:
```bash
python3 -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
```
2. Install deps:
```bash
pip install -r requirements.txt
```
3. Run server:
```bash
uvicorn app.main:app --reload
```
Open `http://127.0.0.1:8000/docs` for interactive API docs.

---

## Auth (demo)
- POST `/auth/token` with form fields `username=demo`, `password=demo` → returns JWT.
- Use header: `Authorization: Bearer <token>` for protected endpoints.

---

## Important endpoints (examples)
- `GET /coins?page_num=1&per_page=10` — paginated list of coins (id, symbol, name)
- `GET /coins/markets?ids=bitcoin,ethereum` — market prices in INR & CAD
- `GET /categories` — CoinGecko categories
- `GET /health` — basic health
- `GET /version` — app name & version

---

## Tests
```bash
pytest
```
Tests cover authentication, health/version and basic protected endpoint behavior (uses monkeypatch to avoid external calls).

---

## Docker
```bash
docker build -t vetty-crypto-api .
docker run --rm -p 8000:8000 vetty-crypto-api
```

---

## Notes
- Replace JWT secret & demo credentials in `.env` before publishing.
- Service is stateless; data comes live from CoinGecko (observe their rate limits).


