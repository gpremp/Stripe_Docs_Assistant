# Stripe Docs Assistant

## Step 1: Crawl Stripe Docs into Markdown

This first stage fetches a single Stripe documentation page and saves its Markdown under `data/stripe_docs/`. Each file includes its source URL and fetch time. Output is written atomically so an interrupted crawl does not leave a partial document.

### Setup

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
crawl4ai-setup
```

### Run

```bash
python webCrawller
python webCrawller https://docs.stripe.com/payments/checkout
```

Only HTTPS URLs on `docs.stripe.com` are accepted. The crawler retries transient failures up to three times.

### Next stages

1. Discover documentation URLs from Stripe's sitemap and crawl them at a controlled rate.
2. Normalize and validate Markdown, then add focused tests for URL handling, retries, and persistence.
3. Chunk pages while keeping heading paths and source URLs as metadata.
4. Index chunks in a vector store and build retrieval with citations.
5. Add the assistant API, observability, and deployment configuration.
