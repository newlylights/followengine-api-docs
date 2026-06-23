# Competitors API

Manage the competitors you monitor on FollowEngine.

## List Competitors

```http
GET /v1/competitors
```

Returns all competitors being monitored.

**Parameters:**

| Name | Type | Description |
|------|------|-------------|
| `status` | string | Filter: `active`, `paused`, `error` |
| `limit` | integer | Max 100, default 20 |
| `cursor` | string | Pagination cursor |

**Response:**
```json
{
  "competitors": [
    {
      "id": "comp_01h2x3y4z5",
      "name": "Acme Corp",
      "domain": "acmecorp.com",
      "channels": ["google_ads", "meta_ads", "youtube", "tiktok"],
      "status": "active",
      "tags": ["enterprise", "saas"],
      "created_at": "2026-01-15T10:00:00Z",
      "last_signal_at": "2026-06-23T08:15:00Z"
    }
  ],
  "total": 12,
  "has_more": false,
  "next_cursor": null
}
```

## Add Competitor

```http
POST /v1/competitors
```

Start monitoring a new competitor.

**Request:**
```json
{
  "domain": "competitor.com",
  "name": "Competitor Inc",
  "channels": ["google_ads", "meta_ads", "search", "youtube"],
  "tags": ["b2b", "mid-market"]
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `domain` | ✅ | Primary domain to monitor |
| `name` | | Display name (defaults to domain) |
| `channels` | | Channels to monitor. All if omitted. |
| `tags` | | Custom labels |

**Available Channels:**

| Channel | Tracks |
|---------|--------|
| `google_ads` | Google Search & Display ads |
| `meta_ads` | Facebook & Instagram ads |
| `tiktok_ads` | TikTok ad campaigns |
| `youtube` | YouTube channel content |
| `tiktok` | TikTok channel content |
| `search` | Google SERP visibility |
| `web` | Website & pricing changes |

## Get Competitor

```http
GET /v1/competitors/{id}
```

Returns full details for a single competitor.

## Update Competitor

```http
PATCH /v1/competitors/{id}
```

Update channels, tags, or pause monitoring.

```json
{
  "channels": ["google_ads", "search"],
  "status": "paused",
  "tags": ["enterprise"]
}
```

## Remove Competitor

```http
DELETE /v1/competitors/{id}
```

Stop monitoring. Returns `204 No Content`.

## Competitor Signals

```http
GET /v1/competitors/{id}/signals
```

Get signals for a specific competitor. Supports `channel`, `severity`, `since`, and `limit` filters.

---

[← Back to API Reference](../README.md) · [FollowEngine](https://followengine.com)
