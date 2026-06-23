# Signals API

Retrieve competitor signals — detected changes across ads, search, content, and channels.

## Signal Object

A **signal** represents any detected competitor change:

```json
{
  "id": "sig_01h2x4z5a6",
  "competitor_id": "comp_01h2x3y4z5",
  "competitor_name": "Acme Corp",
  "channel": "google_ads",
  "type": "new_creative",
  "title": "Acme Corp launched a free trial angle",
  "description": "New ad copy clusters around 'no credit card required' — signaling a PLG push.",
  "severity": "medium",
  "change_pct": 24,
  "detected_at": "2026-06-23T08:15:00Z",
  "url": "https://followengine.com/signals/sig_01h2x4z5a6"
}
```

## Signal Types

| Type | Channel | Description |
|------|---------|-------------|
| `new_creative` | ads | New ad creative detected |
| `creative_change` | ads | Existing ad creative modified |
| `keyword_gain` | search | New keyword in top 20 |
| `keyword_loss` | search | Keyword dropped from top 20 |
| `ranking_change` | search | Significant ranking shift (>5 positions) |
| `new_content` | content | New video/post published |
| `content_theme_shift` | content | Content topic cluster changed |
| `pricing_change` | web | Pricing page updated |
| `feature_launch` | web | New feature/product page detected |
| `job_spike` | other | Unusual hiring activity |

## Severity Levels

| Level | Meaning |
|-------|---------|
| `low` | Routine change, informational |
| `medium` | Notable shift, review recommended |
| `high` | Significant move, action likely needed |
| `critical` | Major competitive event, immediate response |

## List All Signals

```http
GET /v1/signals
```

**Parameters:**

| Name | Type | Description |
|------|------|-------------|
| `severity` | string | Filter: `low`, `medium`, `high`, `critical` |
| `channel` | string | Filter by channel |
| `type` | string | Filter by signal type |
| `since` | datetime | Signals after this time (ISO 8601) |
| `until` | datetime | Signals before this time |
| `limit` | integer | Max 100, default 20 |
| `cursor` | string | Pagination |

**Response:**
```json
{
  "signals": [ ... ],
  "total": 245,
  "has_more": true,
  "next_cursor": "cur_nxt_page_abc123"
}
```

## Get Signal Detail

```http
GET /v1/signals/{id}
```

Returns full signal details including AI analysis and related signals.

---

[← Back to API Reference](../README.md) · [FollowEngine](https://followengine.com)
