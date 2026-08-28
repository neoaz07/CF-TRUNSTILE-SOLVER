# GhostTrustile Solver API

Production-grade Cloudflare Turnstile solving service based on [Theyka/Turnstile-Solver](https://github.com/Theyka/Turnstile-Solver).

## Quick Start

```bash
export API_KEY="your_secret_key_here"
pip install -r requirements.txt
python -m patchright install chromium
python api_solver.py --headless true --useragent "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36" --thread 1 --port 5000
```

## Authentication

All endpoints require the `apikey` query parameter or `X-API-Key` header.

```
/solve?apikey=your_secret_key_here&sitekey=0x4AAAAAAC-pdVMpBJQaHL0Q&siteurl=https://unitool.ai/en/entry
```

Or via header:
```bash
curl -H "X-API-Key: your_secret_key_here" "http://localhost:5000/solve?sitekey=0x4AAAAAAC-pdVMpBJQaHL0Q&siteurl=https://unitool.ai/en/entry"
```

## API Endpoints

### `GET /`

Returns service info.

**Response:**
```json
{
  "name": "TRUSNSTILE SOLVER PRO",
  "credits": "NEOKEX",
  "message": "For API-KEY ask NEOKEX"
}
```

### `GET /solve`

Synchronous Turnstile solver. Returns token directly.

**Parameters:**
- `apikey` (required) - Your API key
- `sitekey` (required) - Turnstile site key
- `siteurl` (required) - Target site URL

**Response:**
```json
{
  "status": "success",
  "token": "1.xxx...",
  "time_taken": 3.232,
  "maintained_by": "NEOKEX"
}
```

### `GET /turnstile`

Asynchronous solver. Returns `task_id`, poll `/result?id=<task_id>`.

### `GET /result`

Get result by task ID.

## Docker

```bash
docker build -t turnstile-solver .
docker run -p 5000:5000 -e API_KEY="your_secret_key_here" turnstile-solver
```

## Deployment

### Render / Railway

- Set environment variable `API_KEY` to your secret key
- Set build command: `pip install -r requirements.txt && python -m patchright install chromium`
- Set start command: `python api_solver.py --headless true --thread 1 --port $PORT --host 0.0.0.0`
- Use the included `Dockerfile` for container deployment

## Maintained by

NEOKEX
