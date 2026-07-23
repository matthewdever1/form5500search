# Form 5500 Search

**Live at [form5500search.com](https://form5500search.com)**

![Next.js](https://img.shields.io/badge/Next.js-000000?logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![DuckDB](https://img.shields.io/badge/DuckDB-FFF000?logo=duckdb&logoColor=black)
![Apache Parquet](https://img.shields.io/badge/Apache_Parquet-50ABF1)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?logo=supabase&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?logo=stripe&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-0B0D0E?logo=railway&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?logo=cloudflare&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white)

A free search engine over ~2.9 million U.S. Department of Labor Form 5500 filings — the annual reports every employee benefit plan (401(k), pension, welfare) files under ERISA. Built for financial advisors prospecting retirement plans.

![Form 5500 Search homepage](screenshot.png)

## What it does

- **Search 2.9M filings** by company name, EIN, or plan name — free, no account required
- **Plan intelligence**: every plan gets a 0–100 health score, fee benchmarks vs. same-size peers, the full provider stack (recordkeeper, custodian, auditor, advisor), and year-over-year change detection
- **Fund holdings**: parses the Schedule of Assets out of each filing, so you can see every line item a plan owns — and reverse-lookup every plan holding a given fund family, ranked by dollars
- **Lead reports**: curated lists of plans that just changed recordkeeper or auditor, lost assets, or pay above-median fees — the highest-signal prospecting triggers
- **Decision-maker unlocks**: verified contacts (signer, CFO, HR, benefits) with email and LinkedIn, exportable to CSV
- **Programmatic SEO**: hundreds of thousands of indexable plan, company, provider, fund, state, and industry pages

## How it's built

- **Next.js (App Router)** serving a corpus of Parquet files queried in-process with **DuckDB** — no database server; the entire dataset is baked into the Docker image
- **Data pipeline**: monthly automated refresh from DOL EFAST2 (download, convert, canonicalize), plus a PDF-parsing pipeline (Gemini + Docling) that extracts itemized holdings from scanned Schedule H attachments
- **Supabase** for auth and billing state, **Stripe** for payments, **Railway** for hosting, **Cloudflare** for edge caching of SEO pages
- Fully automated deploys: GitHub Actions rebuilds the data, bakes a new image, deploys, purges the edge cache, pings IndexNow, and warms every hub page

*The source code is private. This repo is a project showcase.*
