# CrowFind Alpha Test Server — v0.26.0-alpha

> This document describes the purpose, scope, and access policy of the CrowFind alpha test environment, deployed prior to the public demo release (v0.26.xx).

---

## Overview

The alpha server is a pre-demo environment designed to:

- Validate AI pipeline behavior and core features in a live cloud environment
- Collect early user feedback (article engagement, reactions, browsing patterns)
- Confirm infrastructure stability before the public demo launch

---

## Release Roadmap

Versions follow the format `{stage}.{year}.{update}`:

| Segment | Meaning | Example |
|---------|---------|---------|
| `stage` | Deployment tier (`0` = alpha/demo, `1` = production) | `0`, `1` |
| `year` | Year of the release cycle | `26`, `27` |
| `update` | Shared update counter across all tiers | `0`, `1`, `2` ... |

The `update` number is shared across alpha, demo, and production. Alpha always leads, and stable versions are promoted to demo then production with the same number.

### Example progression

```
0.26.0-alpha  →  test server initial deploy
0.26.2-alpha  →  test server updates
              →  0.26.2   demo launches (same update number)
0.26.7-alpha  →  test server updates
              →  0.26.7   demo updated
                   ↓  production launch decision
              [demo retired]  →  1.26.7   production launches
                                          (demo evolves into production)
0.26.8-alpha  →  test server updates
              →  1.26.8   production updated
```

> The demo does not run alongside production — it evolves into production. Once production launches, only two environments remain: the alpha test server and production.

---

## What's Different from the Demo

| Feature | Alpha `0.26.0-alpha` | Demo `0.26.xx` |
|---------|----------------------|----------------|
| **Payments** | None | PayPal / TossPay |
| **Article Access** | Full access — no login required | Block-level access control (Free / Premium) |
| **Content Masking** | Disabled | IMAGE, CHART, QUANT blocks locked for Free users |
| **Article Creation** | Admin only (role guard) | AI-exclusive (automated pipeline) |
| **Debate / Comments** | Admin only | Premium subscribers |
| **Likes** | Logged-in users | Logged-in users |
| **Lounge** | Logged-in users | Logged-in users |
| **Subscriptions** | Not available | Monthly plan via PayPal |

---

## Access Policy

**Reading is fully open.** All articles, AI-generated content, and quant blocks are accessible without login or subscription during the alpha phase.

**Writing is admin-only.** Article creation, comments, and lounge posts are restricted to admin accounts during this period.

This policy exists to ensure data quality and controlled testing before general public access.

---

## User Data Migration

User accounts created during the alpha phase will be carried over to the demo environment. All article, news, and market data will be retained.

There is no need to re-register when the demo launches.

---

## Infrastructure

The alpha server runs on the same cloud infrastructure planned for the demo deployment.

| Service | Platform |
|---------|----------|
| Web | Vercel |
| API | Google Cloud Run |
| AI Engine | Google Cloud Run |
| Database | Supabase (PostgreSQL) |

AI pipelines run on an automated schedule:
- News collection: every 4 hours
- Price collection: weekdays at 16:05 ET (after US market close)
