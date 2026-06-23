# AI Briefs API

AI-generated competitive strategy briefs. FollowEngine compresses competitor signal clusters into actionable intelligence.

## Brief Object

```json
{
  "id": "brief_01h2x5y6z7",
  "competitor_id": "comp_01h2x3y4z5",
  "competitor_name": "Acme Corp",
  "period": "last_7_days",
  "title": "Weekly Brief: Acme Corp",
  "summary": "Acme Corp increased Google Ads spend 24% and shifted messaging toward PLG positioning. Their YouTube content shows a new focus on enterprise case studies.",
  "what_changed": [
    "Google Ads spend +24% with new free-trial creative angle",
    "Pricing page updated with new enterprise tier",
    "LinkedIn hiring 3 senior sales roles — potential market expansion"
  ],
  "what_repeated": [
    "Meta Ads creative theme of 'no-code integration' continues for 3rd week",
    "Weekly blog publishing cadence maintained (2 articles/week)",
    "TikTok product demo format remains consistent"
  ],
  "what_to_copy": [
    "Test the free-trial CTAs in our own ad copy for competitive deals",
    "Evaluate enterprise pricing tier positioning and gaps",
    "Monitor their new sales hires' territories for market entry signals"
  ],
  "signal_count": 18,
  "generated_at": "2026-06-23T10:00:00Z"
}
```

## List Briefs

```http
GET /v1/briefs
```

**Parameters:**

| Name | Type | Description |
|------|------|-------------|
| `competitor_id` | string | Filter by competitor |
| `period` | string | `last_7_days`, `last_30_days`, `last_quarter` |
| `limit` | integer | Max 20, default 10 |

## Generate Brief

```http
POST /v1/briefs/generate
```

Generate a new AI brief on demand.

```json
{
  "competitor_id": "comp_01h2x3y4z5",
  "period": "last_30_days",
  "channels": ["google_ads", "meta_ads", "search", "youtube"]
}
```

Returns `202 Accepted`. The brief is generated asynchronously. Poll `GET /v1/briefs` or subscribe to `brief.generated` webhook.

**Period options:**

| Period | Coverage |
|--------|----------|
| `last_7_days` | Past week |
| `last_30_days` | Past month |
| `last_quarter` | Past 90 days |

## Get Brief

```http
GET /v1/briefs/{id}
```

Full brief with all what_changed / what_repeated / what_to_copy items.

---

[← Back to API Reference](../README.md) · [FollowEngine](https://followengine.com)
