# FollowEngine API Documentation

> Official API reference for FollowEngine — the competitor growth intelligence platform.

**Base URL:** `https://api.followengine.com/v1`

---

## Authentication

All API requests require an API key passed as a Bearer token:

```bash
Authorization: Bearer YOUR_API_KEY
```

Get your API key at [followengine.com/dashboard/settings](https://followengine.com).

---

## Quick Start

```bash
# List monitored competitors
curl https://api.followengine.com/v1/competitors \
  -H "Authorization: Bearer fe_l...xxx"

# Add a competitor to monitor
curl -X POST https://api.followengine.com/v1/competitors \
  -H "Authorization: Bearer fe_l...xx" \
  -H "Content-Type: application/json" \
  -d '{"domain":"competitor.com","channels":["google_ads","search"]}'
```

---

## API Reference

- **[Competitors](docs/competitors.md)** — Manage monitored competitors: list, add, update, remove
- **[Signals](docs/signals.md)** — Retrieve detected competitor signals and changes
- **[AI Briefs](docs/briefs.md)** — AI-generated competitive strategy briefs
- **[Channels](docs/channels.md)** — Channel configuration: ads, search, content, social
- **[Webhooks](docs/webhooks.md)** — Real-time event notifications
- **[Analytics](docs/analytics.md)** — Usage metrics and reporting

---

## Endpoints at a Glance

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/v1/competitors` | List monitored competitors |
| `POST` | `/v1/competitors` | Start monitoring a competitor |
| `GET` | `/v1/competitors/{id}` | Get competitor details |
| `PATCH` | `/v1/competitors/{id}` | Update competitor config |
| `DELETE` | `/v1/competitors/{id}` | Stop monitoring |
| `GET` | `/v1/competitors/{id}/signals` | Signals for a competitor |
| `GET` | `/v1/signals` | List all recent signals |
| `GET` | `/v1/signals/{id}` | Get signal details |
| `GET` | `/v1/briefs` | List AI briefs |
| `POST` | `/v1/briefs/generate` | Generate a new brief |
| `GET` | `/v1/webhooks` | List webhooks |
| `POST` | `/v1/webhooks` | Create webhook |
| `DELETE` | `/v1/webhooks/{id}` | Remove webhook |
| `GET` | `/v1/analytics/usage` | Usage statistics |

---

## SDKs

| Language | Package | Install |
|----------|---------|---------|
| Python | `followengine` | `pip install followengine` |
| Node.js | `@followengine/sdk` | `npm install @followengine/sdk` |
| Ruby | `followengine` | `gem install followengine` |
| cURL | — | Built-in |

---

## Rate Limits

| Plan | Requests/min | Burst |
|------|-------------|-------|
| Free | 30 | 5 |
| Starter | 300 | 50 |
| Growth | 1,000 | 100 |
| Enterprise | Custom | Custom |

Headers: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`

---

## Errors

| Code | Meaning |
|------|---------|
| 200 | Success |
| 400 | Bad request |
| 401 | Invalid API key |
| 403 | Insufficient permissions |
| 404 | Not found |
| 429 | Rate limited |
| 500 | Server error |

All errors return:

```json
{
  "error": {
    "code": "invalid_api_key",
    "message": "The API key provided is invalid.",
    "docs": "https://api.followengine.com/docs#authentication"
  }
}
```

---

## OpenAPI Spec

Machine-readable API specification: [openapi.yaml](openapi.yaml)

Use with Swagger, Postman, or any OpenAPI-compatible tool.

---

## Need Help?

- **Documentation**: [followengine.com/docs](https://followengine.com)
- **Status**: [status.followengine.com](https://followengine.com)
- **Email**: api@followengine.com

---

*FollowEngine — Follow competitors. Copy what works.*
