# Review collection flow

Goal: match Loox's collection flow step for step, then beat it on video. Loox's behavior below comes from its public help center (Nov 2026).

## The per-order flow

| Step | Loox default | Hearsay plan |
|---|---|---|
| Review request | 14 days after fulfillment. Trigger can be purchase, fulfillment, or delivery (1 to 70 days) | Same three triggers. Delivery uses Shopify `shipment_status`, falling back to fulfillment + N days when no delivery is reported |
| International orders | Separate timing option | `internationalDelayDays` setting |
| Reminders | Up to 2: +1 day, then +7 days after the first (each 1 to 30 days) | Same defaults, configurable |
| Send window | Customer's local work hours | Infer timezone from the shipping address and send 9am to 5pm local |
| Postpone | "Haven't received it yet" pushes the next reminder by 7 days | Same, as a link in every email and on the form |
| Thank you email | Right after submit; carries the discount code | Same |
| Photo/video nudge | 3 days after a text-only review (1 to 30) | Same, with a link that reopens the review to add media |
| Discount reminder | Reminds customers who haven't used their code | Later milestone |

One request per fulfillment covers every product in it. Fulfillments on different days each get their own request.

## Review form

- Star rating first, then a short text, then media. Rating can be prefilled from a star tapped in the email (one-tap stars).
- Up to 5 photos **or** 1 video (MOV/MP4, 2 seconds to 15 minutes, under 250 MB, same limits as Loox).
- Mobile-first: most customers open these on a phone.

## Video: where we beat Loox

- **Record in the browser** (MediaRecorder), not just upload, with a 3-second countdown and a 60-second cap.
- **Guided prompts** on screen while recording, set per brand: "Show us the product", "How do you use it?", "What changed for you?"
- **Auto poster frame + captions** generated on upload so videos autoplay muted on the product page.
- Transcode to a light MP4/HLS and serve from the CDN, so the widget never ships the original file.

## Incentives and compliance

- Optional next-purchase discount for photo or video reviews (percent or fixed), created through the Shopify Discounts API.
- The code goes out **whatever the rating**. Incentives tied to positive sentiment are banned under the FTC's 2024 fake reviews rule.
- Two email types, like Loox: **promotional** (may include the discount) for customers who accepted marketing, and **transactional** (no incentive) for everyone else.
- Incentivized reviews get a visible "Received a discount" note.

## Exclusions and extras

- `NOREVIEW` tag on a product (e.g. shipping protection), customer, or order skips it.
- Skip products the customer already reviewed.
- Backfill: request reviews for orders from the 90 days before install.
- Manual requests to a pasted list of customers.
- QR code / review link for package inserts: customer enters an email and gets a request for their latest order.
- Klaviyo: emit events so brands can send requests from their own flows (later milestone).

## Merchant side

- New-review notification email with approve/hide buttons and a reply box.
- Branded emails: logo, colors, and font set once and applied to every email.
- Test-send for every email template.
