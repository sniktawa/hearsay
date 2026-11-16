# Contributing to Hearsay

Thanks for helping build this. You don't need to be a developer to contribute: bug reports, design feedback, and copy for the review emails all help.

## Ways to help

- **Pick up an issue.** Look for `good first issue` or anything in the current milestone. Comment on it before starting, so two people don't build the same thing.
- **Report a bug or ask for a feature.** Open an issue that says what store it happened on, what you expected, and what happened.
- **Test on your store.** Brands in the pilot group can try new builds on a development store before they ship to everyone.

## Dev setup

1. Install Node 20+, the [Shopify CLI](https://shopify.dev/docs/api/shopify-cli), and Docker (for local Postgres).
2. Create a free Shopify Partner account and a development store.
3. Clone the repo, run `npm install`, copy `.env.example` to `.env`, then run `shopify app dev`.

## Pull requests

- Branch from `main`, keep PRs small and focused, and link the issue they close.
- Every query that touches store data must be scoped by `shopId`. This is a shared server, so one brand must never see another brand's data. PRs that skip this won't be merged.
- Never commit secrets, customer data, or real store exports.
- Widget changes should stay light: no new third-party scripts on the storefront without discussion.

## Code of conduct

Be kind and assume good intent. We're all small brands helping each other.
