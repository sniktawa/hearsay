# Hearsay

**Open-source product reviews for Shopify, built and shared by indie CPG brands.**

Hearsay is a community-owned alternative to paid review apps like Loox, Judge.me, and Yotpo. A group of about 15 consumer brands runs it on one shared server and splits the hosting bill. No per-store subscription, no lock-in, and your reviews stay exportable.

## What it does (MVP)

- **Review requests:** sends an email X days after an order is fulfilled, with a one-tap star rating and photo/video upload
- **Photo and video reviews:** stored on a CDN, with a moderation queue in the admin
- **Storefront widget:** star ratings, review list, and photo gallery as Shopify theme app blocks (no theme code edits)
- **SEO:** `AggregateRating` and `Review` JSON-LD, so stars can show in Google results
- **Imports:** CSV, plus migration from Loox, Judge.me, Yotpo, and Okendo exports
- **Verified buyer badges:** every review is tied to a real order

Later: Klaviyo integration, Q&A, Google Shopping reviews feed, review-to-ad UGC export, and lab-results (COA) display next to reviews.

## How it's hosted

One multi-tenant server runs every brand. Each brand connects its store through its own Shopify app config, so the group can skip public App Store review during the pilot. See [docs/architecture.md](docs/architecture.md).

## Stack

- [Shopify Remix app template](https://shopify.dev/docs/apps/build/build?framework=remix), Polaris admin UI
- Theme App Extension for the storefront widget
- Postgres + Prisma
- S3-compatible object storage (Cloudflare R2) for media
- Transactional email (Resend or SES)

## Getting started

See [CONTRIBUTING.md](CONTRIBUTING.md). The roadmap and open work live in [docs/roadmap.md](docs/roadmap.md) and the Issues tab.

## License

MIT. See [LICENSE](LICENSE).
