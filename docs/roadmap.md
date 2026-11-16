# Roadmap

## Milestone 1: Foundations
- Scaffold the Remix app with the Shopify CLI, Prisma, and Postgres
- Multi-tenant data model + shop install/uninstall
- GDPR webhooks (customers/data_request, customers/redact, shop/redact)

## Milestone 2: Collect reviews
- `orders/fulfilled` webhook → scheduled review requests
- Review request email + signed review form (stars, text, photo/video)
- Media uploads to R2 with presigned URLs
- Admin moderation queue (approve, hide, reply)

## Milestone 3: Show reviews
- Theme app blocks: star badge, review list, photo gallery
- JSON-LD for AggregateRating
- Cached public reviews endpoint

## Milestone 4: Switch from other apps
- CSV import/export
- Importers for Loox, Judge.me, Yotpo, and Okendo exports

## Later
- Klaviyo integration (send requests from Klaviyo flows)
- Q&A
- Google Shopping product reviews feed
- UGC export for paid social
- COA / lab results shown beside reviews
