# Scraper API Free Tier: What 1,000 Monthly Credits Actually Get You, How the 7-Day Trial Stacks, and When Upgrading Makes Sense

Most people searching for a scraper API free tier want to know one thing before signing up: is the free allowance big enough to actually test my target sites, or is it a demo that dies after ten requests? With ScraperAPI, the answer is unusually concrete. You get two free allowances that stack: a permanent free plan with 1,000 API credits per month, and a 7-day trial that adds 5,000 credits on top in your first week. Neither requires a credit card. The catch is not the volume — it's the credit pricing. A plain HTML page costs 1 credit, but a JavaScript-rendered page on a protected site can burn 20 or more per request, which turns 1,000 monthly credits into a very different number depending on what you scrape. This guide covers exactly what the free tier includes, what each request really costs, the limits that only show up in the docs, and how to decide whether the paid plans (from $49/month) are worth it.

> **Quick pick:** Start with the 7-day trial — 5,000 credits, no card, enough to run your real targets through the API rather than toy examples. If your sites load fine on standard requests, the free plan's 1,000 monthly credits may be all you need. 👉 [Start the 7-day free trial with 5,000 credits](https://www.scraperapi.com/signup?fp_ref=coupons)

## What the ScraperAPI free tier actually includes

The free tier comes in two parts, and understanding the split matters because they behave differently.

The **permanent free plan** gives you 1,000 API credits every month with a maximum of 5 concurrent connections. It renews, so it's a workable long-term option for genuinely small jobs — think a few hundred plain pages a month, or a daily check on a handful of URLs. The **7-day trial** adds 5,000 free requests during your first week after signup, explicitly designed for testing the API at a larger scale before committing.

Feature-wise, the free plan is not crippled. You get the core stack: rotating proxy pools, premium proxies, JavaScript rendering, JSON auto-parsing, CAPTCHA and anti-bot detection, custom headers, desktop and mobile user agents, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee. You're limited on volume and concurrency, not on capability.

The limits that do apply, and that most signup pages don't spell out:

- **Ultra-premium proxies are excluded from the free tier.** If your target sits behind serious bot protection, requests that would succeed on a paid plan may fail here.
- **Geotargeting is restricted to US and EU locations** on lower tiers. Country-level targeting outside those regions starts at Business ($299/month).
- **Exceed 5 concurrent connections and you get a 429 response.** Nothing queues, nothing waits — your request is simply refused, so your code needs retry-with-backoff logic.
- **When credits run out, scraping pauses** until the next monthly renewal. With no card on file, there's nothing to overcharge.

One more thing worth knowing: if 1,000 plus 5,000 credits genuinely isn't enough to evaluate your workload, ScraperAPI's support team can grant additional test credits on request. That's stated in their own pricing FAQ and billing docs, so it costs you one email to ask before writing the service off.

## Full plan and pricing table

Here's the complete current lineup, including the free plan, with monthly pricing and the annual-billing equivalent (annual plans get 10% off the monthly rate):

| Plan | Monthly price | Annual (per month) | Credits | Concurrent threads | Get started |
| --- | --- | --- | --- | --- | --- |
| Free | $0 | — | 1,000 / month | 5 | [ Claim the free plan](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Hobby | $49 | $44.10 | 100,000 | 20 | [ Start with Hobby](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | [ Start with Startup](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | [ Start with Business](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Scaling | $475 | $427.50 | 5,000,000 | 200 | [ Start with Scaling](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | [ Start with Professional](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | [ Start with Advanced](https://www.scraperapi.com/signup?fp_ref=coupons) |
| Enterprise | Custom | — | 22,000,000+ | 500+ | [ Contact sales](https://www.scraperapi.com/contact-sales/?fp_ref=coupons) |

A few structural points the table can't show:

- **Hobby and Startup are limited to US/EU geotargeting** and a 30-day analytics window. From Business up, you get country-level geotargeting anywhere and unlimited analytics history.
- All paid plans include the full feature set — JS rendering, premium residential and mobile IPs, advanced anti-bot bypass, structured data endpoints, DataPipeline, the crawler, and pay-as-you-go eligibility where noted.
- The billing docs also list a **Student** monthly plan, though no public price is shown on the pricing page; students would need to ask support directly.
- If you burn through credits mid-cycle, behavior depends on the plan: monthly plans from Hobby to Professional can opt into **auto-upgrade** (automatically bumps you to the next tier, which the docs note often works out cheaper per credit), and from Scaling up you get **pay-as-you-go** — continuing at a fixed per-credit rate with a monthly spending cap you set. The cap is a limit, not a pre-charge.

Worth factoring in before any paid decision: ScraperAPI offers a **7-day no-questions-asked refund policy**, and you can cancel anytime from the dashboard at no charge. That takes most of the risk out of trying Hobby for a real workload. 👉 [Try Hobby risk-free with the 7-day refund window](https://www.scraperapi.com/signup?fp_ref=coupons)

## The credit math nobody puts on the pricing page

Here's the single most important thing to understand about any scraper API free tier: the number of credits and the number of pages you can fetch are completely different numbers. ScraperAPI's own FAQ is refreshingly direct about this — a standard page costs 1 credit, but harder targets are priced differently:

| Request type | Credit cost |
| --- | --- |
| Standard HTML page | 1 |
| JavaScript rendering (`render=true`) | +10 |
| Amazon pages | 5 |
| Google or Bing (including subdomains) | 25 |
| LinkedIn | 30 |
| Sites behind Cloudflare, Datadome, or PerimeterX (when bypassed) | +10 per request |

These stack. A rendered request to a protected site can cost 30, 50, even 75 credits for a single page. One independent review worked through the implication: on Amazon search results with JS rendering enabled, 1,000,000 credits might only cover 40,000–100,000 actual pages, not a million. The headline price per credit looks cheap until you multiply by the real per-page cost of your workload.

Two tools keep this from ambushing you:

1. **Domain Cost Estimator** — in your dashboard, paste any URL and it tells you the exact credit cost before you run the job.
2. **`max_cost` parameter** — set a ceiling per request so a misconfigured scrape can't silently drain your balance.

Run both during the free trial. If your targets are plain e-commerce catalog pages, the free tier and the entry plans are generous. If they're Google SERPs with rendering, budget for a 25–35x multiplier from day one.

## How to actually test during the free trial

Seven days goes fast, so sequence the work. A practical order:

1. **Sign up and grab your API key** — it's issued immediately, no card needed.
2. **Run the Domain Cost Estimator** on every target URL you care about. This tells you whether your workload is a 1-credit workload or a 30-credit one before you spend anything.
3. **Test the hard cases first** — the protected domain, the JS-heavy page. Standard pages will work; you want to know where the walls are while you still have 5,000 credits.
4. **Watch your concurrent count** in the dashboard. On the free plan you have 5 threads, and hitting the ceiling produces 429s, so tune your worker count accordingly.
5. **Set `max_cost`** on your test jobs to keep any single expensive request bounded.

One behavior to plan around: response times vary with difficulty. Simple pages return in seconds, but protected domains can take up to 60 seconds — the official docs recommend a 70-second client timeout. For volume work, the Async API exists precisely for this, returning results via callbacks instead of blocking.

If the trial goes well and you're deciding between free and paid, the honest framing is this: the free plan survives on plain pages. The moment your jobs routinely cost 10+ credits each, 1,000 monthly credits equals fewer than 100 requests a month, which is below the threshold of any real project. That's the point where Hobby's 100,000 credits for $49 stops looking optional.

## Who each plan actually fits

Match the plan to the workload, not to the credit number:

- **Free plan (1,000 credits/month):** plain-HTML targets, low frequency — a daily price check on 20–30 product pages, a weekly status scrape. Also the right home for ongoing experimentation after your trial ends.
- **Hobby ($49/month, 100K credits, 20 threads):** the sweet spot for solo developers and small teams doing price monitoring, SERP rank tracking, or lead-gen against standard e-commerce and search targets at roughly 20,000–200,000 pages a month, assuming mostly plain requests.
- **Startup ($149/month, 1M credits, 50 threads):** same profile, roughly 10x the volume. Still US/EU-only geotargeting.
- **Business ($299/month, 3M credits, 100 threads):** the minimum tier for country-level geotargeting outside US and EU. If "scrape this site as if from Japan or Brazil" is part of your requirement, start here.
- **Scaling and up:** production volume with pay-as-you-go headroom. Scaling is marked "Most popular" on the pricing page — that label matters mainly if you regularly blow past plan limits and want PAYG to absorb the spikes.

Where ScraperAPI is the wrong tool, third-party reviews converge on the same cases: heavy scraping of LinkedIn, Instagram, or aggressively protected e-commerce, where the ultra-premium multipliers make it costlier than bandwidth-billed residential proxies; and anything needing long-lived sessions for ad verification or account workflows — sticky sessions are short-lived (reviews place the window between 15 minutes and an hour), and you can't pin specific IPs or ASNs by design.

## How the free tier compares to other providers

If a permanent free allowance is your filter, the field narrows fast. Based on a 2026 comparison of major scraping providers:

| Provider | Starting price | Free plan | Free trial |
| --- | --- | --- | --- |
| ScraperAPI | $49/month | Yes (1,000 credits/month) | Yes (7 days, 5,000 credits) |
| Apify | $29/month | Yes | No |
| Oxylabs | $30/month | No | Yes |
| Zyte | $100/month | No | Yes |
| Bright Data | $499/month | No | No |

Only ScraperAPI and Apify offer both a recurring free plan and a trial. The trade-off differs: Apify's model centers on pre-built scrapers and hosted runs, which suits people who'd rather not write code; ScraperAPI's single-endpoint API suits developers who already have scraper code and just want the blocking, rendering, and proxy rotation handled. Oxylabs and Zyte give you trials but no recurring free allowance, and Bright Data's entry point is aimed well above the individual-developer budget.

The practical takeaway: if your criterion is "test for free, then keep a small free allowance running indefinitely," ScraperAPI's combination is the more complete one in this set.

## FAQ

**Do I need a credit card for the ScraperAPI free tier?** No. Both the permanent free plan and the 7-day trial work without a card, which also means nothing can auto-charge you when the trial ends.

**What happens when I run out of free credits?** Scraping pauses until credits renew on the next cycle. On the free plan there's no auto-upgrade or pay-as-you-go — you either wait, request extra test credits from support, or move to a paid plan.

**Can I use JavaScript rendering on the free plan?** Yes — rendering is included, but each rendered request costs about 10 extra credits, so rendering drops your effective monthly page count from roughly 1,000 to under 100.

**What if I exceed 5 concurrent connections?** The API returns a 429 response and refuses the request rather than queueing it. Handle retries with backoff in your code.

**Is there a refund if a paid plan doesn't work out?** Yes — a 7-day no-questions-asked refund, handled through support, plus cancel-anytime with no fees.

## The bottom line for your situation

If your targets are plain HTML and your monthly volume fits in a few hundred pages, the free plan alone may cover you permanently — sign up, run the Domain Cost Estimator, and see. If the trial showed your real workload costs 10–30 credits per page, Hobby at $49 (or $44.10 on annual billing) is the realistic entry point, and the 7-day refund means you can point it at production traffic before fully committing. If you need non-US/EU geotargeting, skip straight to Business. And if you're scraping LinkedIn or heavy anti-bot targets at scale, the honest advice from the reviews is to price out your real per-page cost first, because that multiplier — not the plan price — determines what you'll actually spend. 👉 [Sign up and test your targets with 5,000 free trial credits](https://www.scraperapi.com/signup?fp_ref=coupons)
