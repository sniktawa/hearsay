# Architecture

## One server, many brands

Hearsay runs as a single multi-tenant app. Every table that holds store data carries a `shopId`, and every query is scoped by it.

```
Brand stores (15+)  ──OAuth/webhooks──▶  Hearsay server (Remix)  ──▶  Postgres
       ▲                                     │        │
       │  theme app blocks (widget)          │        └──▶  R2 (photos/video)
       └─────────── reviews JSON ◀───────────┘
                                             └──▶  Email (review requests)
```

## Connecting stores

**Pilot (now):** each brand gets its own Shopify app config (a separate `shopify.app.<brand>.toml`) pointing at the same server. Custom apps install on one store each, so this skips public App Store review.

**Later:** if the group grows, publish one public app (listed or unlisted) and retire the per-brand configs.

## Core flows

1. **Install:** the store completes OAuth, and a `Shop` row plus default settings are created.
2. **Order fulfilled:** the `orders/fulfilled` webhook schedules a `ReviewRequest` for N days later.
3. **Request sent:** a worker emails the customer a signed link (no login needed).
4. **Review submitted:** media uploads straight to R2 via presigned URL. The review lands as `pending` or `published`, depending on the shop's auto-publish rules.
5. **Storefront:** the theme app block fetches published reviews from a cached public endpoint and renders JSON-LD.

## Customer data

Hearsay stores customer names and emails, which falls under Shopify's protected customer data rules. We store the minimum, encrypt it at rest, delete it on `customers/redact` and `shop/redact` webhooks, and keep brands fully isolated. One named maintainer owns security for the shared server.

## Costs

The hosting bill is split across participating brands. The main drivers are video storage/bandwidth and email volume.
