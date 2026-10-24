# Residential Proxies Pricing: What a GB Really Costs, How Credit-Based APIs Change the Math, and Where ScraperAPI Fits

If you're searching "residential proxies pricing," you probably want one number: what does a gigabyte actually cost? The short answer for 2026 is that published entry rates for rotating residential proxies run from roughly €2.90 to $8 per GB, and drop to $0.70–$5 per GB at the largest self-serve tiers. But there's a second pricing model you should know about before you commit: credit-based scraping APIs like ScraperAPI, where you pay per request rather than per GB — and which can be dramatically cheaper depending on what you're scraping.

This article covers both: the real per-GB market rates from major providers, how ScraperAPI's credit system works (including the multipliers almost nobody mentions upfront), and how to figure out which model costs you less.

> **Quick take:** If your traffic is dominated by heavily protected sites (Google, LinkedIn, anti-bot pages), ScraperAPI's credit plans starting at $49/month often cost less than buying residential bandwidth separately. If you're moving bulk bandwidth to ordinary sites, a per-GB provider is more economical. 👉 [See ScraperAPI's current plans and prices](https://www.scraperapi.com/pricing?fp_ref=coupons)

## What residential proxies actually cost per GB right now

Entry-tier published rates in October 2026 range from €2.90 to $8 per GB. At the 100 GB/month mark, published plans land between roughly $2 and $4 per GB with current discounts applied. All rates below are verified from the providers' own pricing pages; monthly plans are marked as such, and one-off purchases stay one-off:

| Provider | Entry rate | ~100 GB tier | Lowest published rate |
| --- | --- | --- | --- |
| Bright Data | $8/GB (no commitment; page coupon halves it to $4) | $499 for 141 GB ($3.50/GB with coupon) | $2.50/GB (798 GB) |
| Oxylabs | $6/GB ($30 for 5 GB) | $500 for 125 GB ($4/GB), monthly plan | $2.50/GB (1 TB) |
| IPRoyal | $7.35 for 1 GB | $5.51/GB at 10 GB | $1.84/GB (10 TB+) |
| SOAX | $5/GB (US, sandbox) | $300 for 100 GB (US), monthly Builder plan | $0.85/GB (US, $3,000 tier) |
| Decodo | $4/GB wallet | $275 for 100 GB ($2.75/GB), monthly plan | $2/GB (1 TB) |
| Webshare | $3.50 for 1 GB | $225 for 100 GB ($2.25/GB), monthly | $1.40/GB (3,000 GB) |
| Rayobyte | $3.50/GB (1–49 GB) | $200 for 100 GB ($2/GB), one-off | $0.70/GB (one-off 1,000+ GB) |

At the same 100 GB/month usage, the cheapest and most expensive published plans differ by $300 per month — $3,600 a year. Comparison shopping genuinely pays here.

Two billing details worth knowing before you sign anything. First, Bright Data counts every byte in both directions — request headers, request body, response headers, response body — so your effective GB consumption is higher than the payload you care about. SOAX additionally bills partial responses, retries, and interrupted connections. Second, some "cheap" plans carry restrictions: Rayobyte's aggressive $0.015/GB Scale Residential plan limits you to one concurrent request per $1 of plan, has no geo-targeting, and requires a compliance review before access.

## ScraperAPI pricing: seven plans, priced in credits

ScraperAPI takes a different approach. Instead of buying bandwidth, you buy API credits, and the service handles proxies, browser rendering, CAPTCHA solving, and retries for you. Here's the full current lineup from their pricing page:

| Plan | Monthly price | Annual price | Credits | Threads | Geo-targeting | Link |
| --- | --- | --- | --- | --- | --- | --- |
| Hobby | $49 | $44.10 | 100,000 | 20 | US & EU only | [ Start with Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | US & EU only | [ View Startup plan](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | Country-level | [ See Business plan](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling (most popular) | $475 | $427.50 | 5,000,000 | 200 | Country-level | [ Check Scaling plan](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | Country-level | [ See Professional plan](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | Country-level | [ View Advanced plan](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom | Custom | 22,000,000+ | 500+ | Country-level | [ Contact for Enterprise pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |

All plans include JS rendering, premium residential/mobile IPs, automatic JSON parsing, CAPTCHA bypass, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee. Annual billing takes 10% off across the board. There's a 7-day trial with 5,000 credits (no credit card required), plus a permanently free tier with 1,000 credits and a maximum of 5 concurrent connections.

That Hobby price of $44.10/month billed annually buys 100,000 credits — and what a credit buys is where things get interesting.

## The credit math nobody explains clearly (but should decide your choice)

A "credit" is not a request. This is the single most important thing to understand about ScraperAPI's pricing, and it's the detail most comparison articles gloss over.

The base rates from ScraperAPI's own documentation and pricing page:

- **Standard request: 1 credit.** A typical page on an unprotected site.
- **Amazon pages: 5 credits.** Google and Bing search URLs (including subdomains): 25 credits. LinkedIn: 30 credits.
- **Premium residential/mobile pool** (`premium=true`): **10 credits** per successful request — 10× the normal rate.
- **Premium pool + JS rendering:** 25 credits.
- **Ultra-premium pool** (`ultra_premium=true`, for the toughest anti-bot targets): 30 credits per request, or 75 with rendering. Ultra-premium is paid plans only, and can't be combined with custom headers.
- **Anti-bot bypass triggered by a site** (Cloudflare, Datadome, PerimeterX): +10 credits on top.

So the practical cost varies enormously by target. Using the official credit rates, 100,000 credits on the Hobby plan buys either 100,000 standard pages, or 20,000 Amazon pages, or about 4,000 Google search results, or about 3,300 LinkedIn pages. The pricing page itself puts it this way: $49 gets you 100,000 URLs — or up to 3,000 heavily protected pages.

Before assuming that's expensive, translate it into the residential-proxy equivalent. Google and LinkedIn pages are exactly the targets where raw residential proxies burn bandwidth through repeated CAPTCHA failures, blocked retries, and fingerprinting losses. A per-GB provider charges you for every failed attempt's bytes; ScraperAPI only charges credits on successful requests (failed requests after automatic retries don't bill credits). On hard targets, "per successful request" pricing can come out well ahead of per-GB pricing — on easy targets, it's usually the reverse.

ScraperAPI gives you a tool to check this before committing: the Domain Cost Estimator in the dashboard shows the exact credit cost for any URL you plan to scrape. You can also set a `max_cost` parameter to cap what any single request can spend. If you want to price your own workload before signing up, 👉 [run your target URLs through the free 7-day trial](https://www.scraperapi.com/pricing?fp_ref=coupons) — no credit card needed, so the estimate costs nothing.

A few plan-level limits that only show up in the fine print, verified from the pricing page and docs:

- Hobby and Startup only offer US & EU exits; country-level targeting starts at Business.
- Analytics dashboards on Hobby/Startup show only the last 30 days; unlimited history starts at Business.
- Exceeding your thread limit returns a 429 — the request is rejected, not queued, and not billed.
- When credits run out, scraping pauses by default until renewal. On mid and upper tiers you can enable auto-upgrade (move up a tier for the rest of the month) or pay-as-you-go overage at a fixed per-credit rate with a self-set monthly cap. PAYG is available on Scaling and above.
- Annual subscribers can renew early to bank a fresh batch of credits.
- You can cancel your subscription at any time from the dashboard without being charged for cancelling.

## Which model should you pay for?

A simple decision rule based on your target mix:

- **Mostly easy, ordinary pages at volume** → a per-GB residential provider. Standard requests at 1 credit are comparatively expensive vs. bulk bandwidth at $2–4/GB, and you don't need managed CAPTCHA solving.
- **Google SERP, LinkedIn, Amazon, or sites behind Cloudflare/Datadome** → ScraperAPI's credits. Managed retries, rendering, and anti-bot bypass bundled in, and you don't pay for failed attempts. The bundled Amazon, Google, and Walmart structured-data endpoints (returning ready-made JSON) remove another layer of parsing work.
- **One-off bulk projects with no ongoing need** → IPRoyal-style single purchases with no expiry, or Rayobyte's one-off tier pricing.

One more reason the decision matters: proxy supply risk. In July 2026, NetNut customers lost their proxy networks entirely after an FBI seizure tied to the Popa botnet — over 2 million compromised devices. An established vendor with clear compliance practices (ScraperAPI states 100% CCPA & GDPR compliance) is a safer long-term bet than the cheapest per-GB rate on a lesser-known network. If the credit model sounds like a fit after checking your targets, 👉 [compare ScraperAPI's plan tiers side by side](https://www.scraperapi.com/pricing?fp_ref=coupons) before deciding between monthly and annual billing.

## FAQ

**How much does ScraperAPI cost for residential proxies?**
Plans start at $49/month ($44.10 billed annually) for 100,000 credits on Hobby. Requests using the premium residential/mobile pool cost 10 credits each; with JS rendering, 25 credits. So $49 covers roughly 10,000 residential-pool pages or 4,000 residential + rendered pages per month.

**Do failed requests consume ScraperAPI credits?**
No. Only successful requests count against your monthly limit. ScraperAPI retries automatically before a request is billed. However, when a site triggers anti-bot protection and ScraperAPI bypasses it, the successful response costs 10 extra credits.

**Is there a free trial?**
Yes — 7 days with 5,000 credits, no credit card needed, plus a permanent free tier of 1,000 credits (5 concurrent connections max).

**How do I estimate costs for my specific targets before buying?**
Use the Domain Cost Estimator in your dashboard after signing up: it shows the exact credit cost for any URL, and you can set a per-request `max_cost` cap. Run your real target list through the free trial first — that gives you a precise monthly credit budget instead of a guess.

## Bottom line: pick by your target list, not the headline number

Before you buy anything, do two things. First, list your actual targets and classify them: ordinary pages, e-commerce, search engines, or anti-bot-protected sites. Second, price your workload under both models — per-GB at the tier sizes above, and in credits via ScraperAPI's free trial with the Domain Cost Estimator.

If your workload is heavy on Google, Amazon, LinkedIn, or protected sites, ScraperAPI's plans are the better-value route, and annual billing saves you the 10%. If you're shipping bulk traffic to easy targets, a $2–4/GB plan from the per-GB table above will be cheaper — no subscription needed. 👉 [Start ScraperAPI's free trial and check your domain costs](https://www.scraperapi.com/pricing?fp_ref=coupons)
