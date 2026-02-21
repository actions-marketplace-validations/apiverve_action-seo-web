# APIVerve SEO &amp; Web Action

> Extract metadata, scrape links, and analyze web pages for SEO

> **Beta Release** - This action is in beta. We'd love your feedback! [Open an issue](https://github.com/apiverve/action-seo-web/issues) if you encounter any problems.

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-SEO &amp; Web-blue?logo=github)](https://github.com/marketplace/actions/apiverve-seo-web)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**[Browse All APIs](https://apiverve.com/marketplace?utm_source=github&utm_medium=action&utm_campaign=seo-web)** | **[Get Free API Key](https://dashboard.apiverve.com/signup?utm_source=github&utm_medium=action&utm_campaign=seo-web)** | **[Documentation](https://docs.apiverve.com?utm_source=github&utm_medium=action&utm_campaign=seo-web)**

---

## What does this action do?

This action provides access to APIVerve's SEO &amp; Web APIs directly in your GitHub workflows:

- Extract metadata from web pages
- Scrape and validate links
- Get page titles for URLs
- Quick SEO analysis

### Available APIs

| API | Description |
|-----|-------------|
| `metadataextractor` | Metadata Extractor is a simple tool for extracting metadata from web pages. It returns the meta title, meta description, and more. |
| `linkscraper` | Link Scraper is a simple tool for scraping web page links. It returns all the links on a web page. |
| `urltitle` | URL Title is a simple tool for getting the title of a web page. It returns the title of the web page based on the URL provided. |
| `seoquickcheck` | seoquickcheck API |
| `websitereadability` | Website Readability is a simple tool for analyzing the readability of a website. It returns the readability score of the website provided. |

---

## Quick Start

```yaml
- name: SEO &amp; Web
  uses: apiverve/action-seo-web@v1
  with:
    api_key: ${{ secrets.APIVERVE_KEY }}
    api: metadataextractor
    params: '{&quot;url&quot;: &quot;https://example.com&quot;}'
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
- name: SEO &amp; Web
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
| `api` | API to use: `metadataextractor`, `linkscraper`, `urltitle`, `seoquickcheck`, `websitereadability` | No | `metadataextractor` |
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
    params: '{&quot;url&quot;: &quot;https://example.com&quot;}'

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
    params: '{&quot;url&quot;: &quot;https://example.com&quot;}'

- name: Use result
  run: echo "Result: ${{ steps.seo-web-1.outputs.data }}"
```


---

## Full Workflow Example

```yaml
name: SEO &amp; Web Workflow

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  seo-web:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run SEO &amp; Web
        id: result
        uses: apiverve/action-seo-web@v1
        with:
          api_key: ${{ secrets.APIVERVE_KEY }}
          api: metadataextractor
          params: '{&quot;url&quot;: &quot;https://example.com&quot;}'

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
