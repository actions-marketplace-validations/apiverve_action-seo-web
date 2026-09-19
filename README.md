# APIVerve SEO & Web Action

> Extract metadata, scrape links, and analyze web pages for SEO

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-SEO_%26_Web-blue?logo=github)](https://github.com/apiverve/action-seo-web)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**[Browse All APIs](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=seo-web)** | **[Get Free API Key](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=seo-web)** | **[Documentation](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=seo-web)**

---

## What does this action do?

This action provides access to APIVerve's SEO & Web APIs directly in your GitHub workflows:

- Extract metadata from web pages
- Scrape and validate links
- Get page titles for URLs
- Quick SEO analysis

### Available APIs

| API | Description |
|-----|-------------|
| `metadataextractor` | Metadata Extractor extracts HTML metadata from any submitted URL, returning the page title, meta description, author, robots directives, and language. Paid tiers add Open Graph tags, JSON-LD schemas, and favicons. |
| `linkscraper` | Link Scraper extracts internal and external links from any webpage URL in real time. It resolves relative paths to absolute URLs, strips empty fragments, and returns anchor text with internal and external counts. |
| `urltitle` | URL Title fetches the HTML title tag of any web page in real time from a target URL. Paid plans also retrieve an array of every H1 heading tag found on the page. |
| `seovalidator` | SEO Quick Validator inspects live web pages for on-page SEO errors and tag issues. Pass any URL to inspect title lengths, meta descriptions, H1 headings, viewport and canonical tags, image alt text, and unverified external links. |
| `websitereadability` | Website Readability analyzes live web pages to score their reading difficulty and educational grade level. It returns Flesch Reading Ease, Flesch-Kincaid grade level, word count, sentence count, and estimated reading time. |

---

## Quick Start

```yaml
- name: SEO & Web
  uses: apiverve/action-seo-web@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: metadataextractor
    params: '{"url": "https://example.com"}'
```

---

## Setup

### 1. Get Your API Key

Sign up for a free account at [dashboard.apiverve.com/signup](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=seo-web) and create an API key.

### 2. Add Secret to Repository

Go to your repository **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

- Name: `APIVERVE_KEY`
- Value: Your API key from the dashboard

### 3. Use in Workflow

```yaml
- name: SEO & Web
  uses: apiverve/action-seo-web@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: metadataextractor
    params: '{"your": "parameters"}'
```

---

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api_key` | Your APIVerve API key (or set `APIVERVE_API_KEY` env var) | Yes* | - |
| `api` | API to use: `metadataextractor`, `linkscraper`, `urltitle`, `seovalidator`, `websitereadability` | No | `metadataextractor` |
| `params` | JSON parameters for the API | No | `{}` |
| `output_file` | Path to save binary output (images, PDFs) | No | - |
| `format` | Response format: `json`, `yaml`, or `xml` | No | `json` |
| `fail_on_error` | Fail workflow if API returns error | No | `true` |
*\*API key is required but can be provided via input OR `APIVERVE_API_KEY` / `APIVERVE_KEY` environment variable.*

## Outputs

| Output | Description |
|--------|-------------|
| `result` | Full API response as JSON |
| `data` | The `data` field from response as JSON |
| `status` | API status (`ok` or `error`) |
| `file` | Path to downloaded file (if `output_file` was used) |
---

## Examples

### Metadata Extraction

Extract metadata from a webpage

```yaml
- name: Metadata Extraction
  id: seo-web-0
  uses: apiverve/action-seo-web@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: metadataextractor
    params: '{"url": "https://example.com"}'

- name: Use result
  run: echo "Result: ${{ steps.seo-web-0.outputs.data }}"
```

### Link Scraping

Extract all links from a webpage

```yaml
- name: Link Scraping
  id: seo-web-1
  uses: apiverve/action-seo-web@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: linkscraper
    params: '{"url": "https://example.com"}'

- name: Use result
  run: echo "Result: ${{ steps.seo-web-1.outputs.data }}"
```


---

## Full Workflow Example

```yaml
name: SEO & Web Workflow

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  seo-web:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run SEO & Web
        id: result
        uses: apiverve/action-seo-web@v1
        with:
          api_key: ${{ secrets.APIVERVE_KEY }}
          api: metadataextractor
          params: '{"url": "https://example.com"}'

      - name: Show result
        run: |
          echo "Status: ${{ steps.result.outputs.status }}"
          echo "Data: ${{ steps.result.outputs.data }}"
```

---

## Related Actions

Looking for more APIVerve actions?

- [apiverve/action](https://github.com/apiverve/action) - Generic action for all 350+ APIs
- [apiverve/action-release-assets](https://github.com/apiverve/action-release-assets) - Generate QR codes, barcodes, and badges for your GitHub releases
- [apiverve/action-visual-testing](https://github.com/apiverve/action-visual-testing) - Capture screenshots and generate PDFs for visual regression testing and documentation
- [apiverve/action-dns-monitor](https://github.com/apiverve/action-dns-monitor) - Verify DNS configuration, check propagation, and validate DNSSEC after deployments

**[Browse all APIVerve Actions →](https://github.com/marketplace?query=apiverve)**

---

## Pricing

- **Free tier** - Get started with generous free limits
- **Pro plans** - Higher rate limits and priority support for production use

Check out [pricing details](https://apiverve.com/pricing?utm_source=github&utm_medium=action&utm_campaign=seo-web).

---

## Resources

- **API Documentation**: [docs.apiverve.com](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=seo-web)
- **API Marketplace**: [apiverve.com/marketplace](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=seo-web)
- **Issues & Support**: [GitHub Issues](https://github.com/apiverve/action-seo-web/issues)
- **Email**: support@apiverve.com

---

## License

MIT - see [LICENSE](LICENSE)

---

Built by [APIVerve](https://apiverve.com?utm_source=github&utm_medium=action&utm_campaign=seo-web) - 350+ APIs for developers
