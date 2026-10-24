# instagram data scraper: What It Can Pull, What It Costs, and the Login-Wall Limits to Check Before You Pay

An instagram data scraper API does one specific job: you send a username, post URL, or hashtag along with an API key, and you get parsed JSON back — follower counts, bios, captions, hashtags, business contact fields — without running your own proxies, headless browsers, or CAPTCHA solvers. There are two routes to this. A general scraping API handles any site including Instagram; a dedicated Instagram scraper API gives you purpose-built endpoints for profile, post, follower, and hashtag data. The differences that actually matter are pricing structure, what happens with login-walled data, and how much each request costs you.

Quick summary if you're deciding right now:

> The dedicated Instagram scraper API starts free (1,000 requests, all endpoints, 10 concurrent connections). The main ScraperAPI plans start at **$49/month for 100,000 API credits**, with a 7-day trial of 5,000 credits that needs no credit card, and a 7-day no-questions-asked refund on paid plans either way. Most light-to-medium users — a few thousand profile or hashtag pulls a month — fit the free or $19–$49 tiers. 👉 [Claim the 7-day free trial (5,000 credits, no card required)](https://www.scraperapi.com/signup?fp_ref=coupons)

## What an instagram data scraper actually returns

It returns structured JSON from dedicated endpoints, and the endpoint list tells you most of what you need to know about fit. The Instagram Scraper API covers nine data types through one REST base URL: email & lead, profile & account, follower, image & photo, reels/stories/video, comment, post, hashtag, and search. One `api_key` authenticates everything — no Facebook app, no linked Business account, no app review process.

The quickstart is genuinely one line:

bash
curl "https://api.instagramscraperapi.com/api/v1/instagram/profile?username=nasa&api_key=YOUR_API_KEY"


Median response time sits at 2.6 seconds. Every request gets a fresh IP from rotating residential and datacenter pools, with built-in verification handling and JS rendering. Billing follows a rule worth internalizing early: you're charged only for successful requests. Failed requests retry automatically across proxy pools and never bill — if an error persists, you don't pay for it.

## The login wall nobody mentions until it matters

Here's the limit that separates a good scraping project from a stalled one: **follower lists and comments are gated**. Instagram serves both only through app endpoints that require a logged-in session. A logged-out request hits a login or checkpoint wall, no matter which scraper you use.

The API handles this honestly — it resolves the IDs, calls the correct endpoints, and reports the actual auth status when data is gated rather than returning a fabricated feed. Profiles and business contact fields are available logged-out, though many large accounts withhold contact data regardless. So before you buy anything, map your requirements against this: if your project depends on bulk follower lists or full comment threads, test that path with the free tier first. If you need profiles, posts, hashtags, and reels data, the logged-out endpoints cover you.

Status codes make the rest predictable. A `402` means you've hit your plan limit (top up or upgrade), `404` means the resource genuinely doesn't exist — deleted or private content — and `429` means you've exceeded your plan's rate limit and should slow down or move up a tier.

## Instagram scraper API pricing

The dedicated Instagram product uses per-request pricing, published in four tiers:

| Plan | Price | Monthly requests | What's included |
| --- | --- | --- | --- |
| Free | $0 | 1,000 | All endpoints, structured JSON, anti-bot + rotating proxies, 10 concurrent |
| Vibe | $19/mo | 27,000 | Everything in Free, higher concurrency, email support |
| Pro | $49/mo | 82,000 | Priority request routing, priority support |
| Custom | $100+/mo | 200,000–4,000,000+ | From $0.50 per 1,000 requests, 500+ concurrency, SLA + dedicated support |

Pay-as-you-go top-ups run $0.90 per 1,000 successful requests if you'd rather not commit to a monthly plan. 👉 [Check current Instagram scraper pricing and start free](https://www.scraperapi.com/?fp_ref=coupons)

A quick cost-per-request comparison makes the tiers easier to read: Vibe works out to roughly $0.70 per 1,000 requests, Pro to about $0.60, and Custom drops to $0.50 or lower. The free tier is enough to validate every endpoint you actually need before spending anything.

## ScraperAPI main plans: the full comparison table

The main ScraperAPI subscription is a broader product — it scrapes any URL, not just Instagram — and it bills in API credits. The official pricing page currently shows seven tiers, with annual billing discounted 10%:

| Plan | Credits/month | Monthly | Annual (per month) | Concurrency | Get started |
| --- | --- | --- | --- | --- | --- |
| Hobby | 100,000 | $49 | $44.10 | 20 threads | [ View Hobby pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | 1,000,000 | $149 | $134.10 | 50 threads | [ View Startup pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | 3,000,000 | $299 | $269.10 | 100 threads | [ View Business pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | 5,000,000 | $475 | $427.50 | 200 threads | [ View Scaling pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | 10,500,000 | $975 | $877.50 | 300 threads | [ View Professional pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | 21,500,000 | $1,975 | $1,777.50 | 500 threads | [ View Advanced pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | 22,000,000+ | Custom | Custom | 500+ threads | [ Contact sales for Enterprise](https://www.scraperapi.com/?fp_ref=coupons) |

Every plan includes JS rendering, premium proxies, JSON auto-parsing, CAPTCHA and anti-bot handling, custom headers and sessions, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee.

Two numbers worth computing before you pick. First, the annual commitment: Hobby costs $588 monthly-billed versus $529.20 on the annual plan — a $58.80 saving. At Business level the gap widens to $358.80 per year ($3,588 vs $3,229.20), and Advanced saves $2,370. Second, the effective per-credit cost: Hobby's $49 for 100,000 credits works out to $0.49 per thousand, while Business's $299 for 3 million credits is about $0.10 per thousand — a 5x drop. If your monthly volume exceeds roughly 500,000 credits, upgrading pays for itself in unit cost alone.

## How credits actually get charged

The credit system is the part most comparison articles skip, and it's where surprise bills come from. A standard page costs 1 credit, but multipliers stack depending on the target and parameters:

- Amazon, Walmart, eBay: 5 credits
- Google and Bing (all subdomains): 25 credits
- LinkedIn: 30 credits
- Cloudflare, DataDome, PerimeterX, or Akamai bypass: +10 credits per scrape
- `premium=true` or `render=true`: +10 credits each (25 combined)
- `ultra_premium=true`: +30 credits, paid plans only (75 with rendering)

Geolocation, custom sessions, device type, and output format add nothing. Billing only applies to status codes 200 and 404, plus requests you cancel yourself within 70 seconds. The response headers include a `sa-credit-cost` field showing exactly what each request consumed, and you can set a `max_cost` parameter to cap any single request. There's also a cost-lookup endpoint that tells you a URL's price before you spend anything.

> Run the cost check on your target URLs before committing to a plan. A project you assume costs 1 credit per page can quietly cost 25 or 35 if it involves search engines or protected domains.

When credits run out, the default behavior is a pause until renewal — not an overage charge. Hobby through Professional plans can opt into auto-upgrade to jump to the next tier automatically; Scaling and above support pay-as-you-go continuation at a fixed per-credit rate, protected by a monthly spending cap you set yourself. 👉 [Test your targets' real credit cost with the free trial](https://www.scraperapi.com/signup?fp_ref=coupons)

## How it compares with the alternatives

The Instagram scraping market splits into three camps. Bright Data runs a mature Instagram Scraper API returning structured JSON with profile fields, follower counts, and verification status — an enterprise-grade option when you need massive volume and a large compliance team behind you. AntsData takes a no-code approach: enter a username or post ID, get clean JSON/CSV/Excel output, no developer account or anti-bot code required — sensible if you'd never touch a `curl` command. At the free end, open-source options like Python scraper libraries and browser extensions (one popular Chrome extension converts profiles into LLM-ready Markdown locally) cost nothing but carry no SLA, no automatic retry infrastructure, and break whenever Instagram changes something — you become the maintenance team.

Where the dedicated API approach earns its price is operational: verified endpoints tested against live Instagram pages, honest reporting on gated data, and billing that stops when the scraping stops.

## FAQ

**Is scraping Instagram data legal?** Scraping publicly available data is broadly permitted in many jurisdictions, and US courts have declined to treat collecting public profile data as unauthorized access. The caveats are real, though: Instagram's terms restrict automated collection, much of the data is personal data covered by GDPR and CCPA, and content behind a login sits in different legal territory. Stick to public fields and get your own legal advice for your specific use case.

**Do I need the official Instagram API?** Not for public data. The Instagram Graph API only returns data for accounts you own or manage, and requires a Facebook app, a linked Business or Creator account, and app review. Reading arbitrary public profiles, posts, or hashtags requires a scraper API.

**What happens if I exceed my plan?** On the main ScraperAPI plans, scraping pauses by default until your credits renew — no surprise charges. You can enable auto-upgrade or pay-as-you-go with a self-set monthly cap. On the Instagram product, a `402` status tells you to top up or upgrade, and you can choose per-request pay-as-you-go at $0.90 per thousand.

**Can I get a refund?** Yes — ScraperAPI offers a 7-day, no-questions-asked refund policy on paid plans, and you can cancel anytime from the dashboard at no charge.

## Which setup fits your project

Match the tool to your volume and scope. If you're pulling a few thousand Instagram profiles, posts, or hashtags per month, start with the dedicated Instagram product's free tier and move to Vibe ($19) or Pro ($49) as volume grows. If you're scraping Instagram alongside other sites — e-commerce, SERPs, LinkedIn — the main ScraperAPI plans make more sense, with Hobby ($49) as the entry point and Business ($299) as the sweet spot once you cross roughly half a million credits monthly, thanks to the 5x better per-credit rate.

Two things to confirm before ordering: first, whether the data you need is login-walled (follower lists, full comment threads) — test that exact endpoint on the free tier; second, your real monthly request count, since the tier jump from Vibe to Pro only pays off above about 55,000 requests. The 7-day refund window backstops both mistakes. 👉 [Start the free trial and run your first scrape today](https://www.scraperapi.com/signup?fp_ref=coupons)
