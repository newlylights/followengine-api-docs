# Webhooks API

Receive real-time notifications when FollowEngine detects competitor activity.

## Event Types

| Event | Trigger |
|-------|---------|
| `signal.new` | New competitor signal detected |
| `signal.escalated` | Signal severity upgraded (e.g., medium → high) |
| `competitor.added` | New competitor added to monitoring |
| `competitor.status_changed` | Competitor paused, resumed, or errored |
| `brief.generated` | AI brief generation complete |

## Webhook Payload

All webhooks follow this format:

```json
{
  "event": "signal.new",
  "timestamp": "2026-06-23T08:15:00Z",
  "data": {
    "signal_id": "sig_01h2x4z5a6",
    "competitor_id": "comp_01h2x3y4z5",
    "competitor_name": "Acme Corp",
    "channel": "google_ads",
    "type": "new_creative",
    "title": "Acme Corp launched a free trial angle",
    "severity": "medium",
    "url": "https://followengine.com/signals/sig_01h2x4z5a6"
  }
}
```

## Signature Verification

Each webhook includes a `X-FollowEngine-Signature` header for verification:

```python
import hmac, hashlib

def verify_signature(payload, signature, secret):
    expected = hmac.new(
        secret.encode(),
        payload.encode(),
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(f"sha256={expected}", signature)
```

## List Webhooks

```http
GET /v1/webhooks
```

```json
{
  "webhooks": [
    {
      "id": "wh_01h2x6y7z8",
      "url": "https://your-app.com/webhooks/followengine",
      "events": ["signal.new", "signal.escalated"],
      "active": true,
      "created_at": "2026-01-15T10:00:00Z"
    }
  ]
}
```

## Create Webhook

```http
POST /v1/webhooks
```

```json
{
  "url": "https://your-app.com/webhooks/followengine",
  "events": ["signal.new", "signal.escalated", "brief.generated"],
  "secret": "whsec_your_webhook_secret"
}
```

## Delete Webhook

```http
DELETE /v1/webhooks/{id}
```

Returns `204 No Content`.

---

[← Back to API Reference](../README.md) · [FollowEngine](https://followengine.com)
