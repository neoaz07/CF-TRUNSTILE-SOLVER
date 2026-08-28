# GhostTrustile Solver API

Production-grade Cloudflare Turnstile solving service based on [Theyka/Turnstile-Solver](https://github.com/Theyka/Turnstile-Solver).

## Quick Start

```bash
pip install -r requirements.txt
python -m patchright install chromium
python api_solver.py --headless false --useragent "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36" --thread 1 --port 5000
```

## API Endpoints

### `GET /solve`

Synchronous Turnstile solver. Returns token directly.

```
/solve?sitekey=0x4AAAAAAC-pdVMpBJQaHL0Q&siteurl=https://unitool.ai/en/entry
```

**Response:**
```json
{
  "status": "success",
  "token": "1.xxx...",
  "time_taken": 3.232,
  "error": null,
  "maintained_by": "NEOKEX"
}
```

### `GET /turnstile`

Asynchronous solver. Returns `task_id`, poll `/result?id=<task_id>`.

### `GET /result`

Get result by task ID.

### `GET /health`

Health check.

## Docker

```bash
docker build -t turnstile-solver .
docker run -p 5000:5000 turnstile-solver
```

## Deployment

### Render / Railway

- Set build command: `pip install -r requirements.txt && python -m patchright install chromium`
- Set start command: `python api_solver.py --headless false --thread 1 --port $PORT --host 0.0.0.0`
- Use the included `Dockerfile` for container deployment

## Maintained by

NEOKEX
