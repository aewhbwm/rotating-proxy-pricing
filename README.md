# buy rotating residential proxies: per-GB vs per-IP pricing, rotation settings worth testing, and where cheap pools actually hold up

Most people searching this phrase aren't window shopping. They have a scraper that just started returning 403s, or they're staring at five pricing tabs that quote numbers in units that can't be compared — $3.50 per GB on one page, $0.02 per IP on another, "unlimited bandwidth" on a third. The shopping part is easy. The expensive mistakes happen after you pay.

Here's the uncomfortable part first: the headline rate you see is rarely the rate you pay. Per-GB billing punishes image-heavy crawls, per-IP billing punishes jobs that need thousands of fresh addresses for a single request each, and monthly plans reset the bandwidth you didn't use. So before comparing providers, figure out which of those two wounds you're actually exposed to.

## What you're buying, in plain terms

Rotating residential proxies route your traffic through IP addresses assigned by real ISPs to real household connections, and the gateway hands out a different address on each request — or holds one for a set number of minutes in sticky mode. That's it. The pool behind the gateway is what you're renting.

Two billing axes cover almost the entire market:

- **Per GB.** You buy a block of traffic, generate as many proxy endpoints as you like, and rotation is managed by the gateway. Good when each request is small and you need wide IP spread.
- **Per IP.** You buy addresses rather than bandwidth, and traffic through those addresses isn't metered. Good when you hold one identity across a long session or push heavy payloads through few connections.

The arithmetic matters more than the branding. A typical HTML page without images runs around 60 KB, so roughly 15,000 pages fit in a gigabyte. At $1/GB that's about 7 cents per 1,000 pages. At the $4/GB that sits near the middle of the market, it's closer to 27 cents. Four times the cost for the identical crawl — from a billing decision, not a network one.

## What rotating residential proxies cost right now

Published vendor rates, as of the pricing pages and comparison data available in late 2026:

| Provider | Published rotating/residential rate |
| --- | --- |
| Infatica | $4/GB |
| SOAX | from $4/1GB |
| Decodo | from ~$4/GB |
| NetNut | $99/28GB (~$3.45/GB) |
| CatProxies | from $2.50/GB |
| Rayobyte | $3.50/1GB, non-expiring |
| Oxylabs | $30/5GB (~$6/GB) |
| IPBurger | $5.90/GB (10GB) down to $4.48/GB (60GB) |
| IPRoyal | $7/1GB, non-expiring |
| Webshare | $1.75/1GB |
| DataImpulse | $1/GB, non-expiring |
| MarsProxies | from $1.65/GB |
| ProxyEmpire | from $0.75/GB |
| QuantumProxies | $1.00/GB at 25GB, $0.80/GB at 1,000GB |

Several of those per-GB numbers for Decodo, Oxylabs, SOAX, NetNut, Webshare, IPRoyal, DataImpulse, Rayobyte and Infatica come from a May 2026 rotating-proxy benchmark roundup that cites Proxyway's test data. One comparative tracker puts the median pay-as-you-go residential rate at around $4/GB across 11 providers, with a range spanning roughly $1 to $8.

The spread is real, but note what sits underneath it: monthly subscriptions reset, balance-based credits usually don't. A $1/GB pack that expires in 30 days can cost more than a $2/GB pack valid for six months if your work comes in bursts.

Where 9Proxy lands on this curve: GB packs run $3.00/GB at the 5 GB entry tier down to $0.68/GB at 10,000 GB, and the per-IP side starts at $0.24/IP falling to $0.018/IP at 500,000 IPs — with unlimited bandwidth attached to each address.

## Per-GB or per-IP? The decision that decides your bill

9Proxy is one of the few providers that sells both models from the same account, which makes it a decent place to run your own numbers before committing.

**Choose per-GB if:**
- Your requests are small and independent (SERPs, listings, price feeds, API polling)
- You want thousands of exit IPs without thinking about address inventory
- Your usage is spiky and month-to-month subscriptions feel like waste

**Choose per-IP if:**
- You hold a session open — logged-in dashboards, carts, multi-account work with an antidetect browser
- Your payloads are heavy and unpredictable in size, so metered traffic is a gamble
- You want addresses sitting in your account that don't burn down while idle

The mechanics differ too. On the GB side, endpoints are generated straight from the dashboard — unlimited of them, with username/password or IP-whitelist authentication, targeting by country, state, city, ZIP and ISP, and traffic valid for 180 days (unlimited on Enterprise). On the IP side, each address stays live anywhere from a few hours to about 24 hours, requires the desktop app for local port forwarding, and rotation comes from the app's auto-rotation feature running on a timer you set per port. Unused IPs never expire.

That app dependency is the thing people miss. If you want to run per-IP residential proxies on a headless cloud box, the GB model is the one that behaves.

## Rotation settings worth testing before you pay

Rotation is configured in the proxy username rather than in code, which is convenient once you know the format. For 9Proxy's GB-based proxies, the structure looks like this:

`subaccount-country-us-st-ohio-city-newyork-isp-as22773_Cox_Communications_Inc.-sst-15-ssid-device1`

Reading that: `country` sets the exit country, `st` and `city` narrow it further, `isp` filters by network, `sst` is sticky session time in minutes, and `ssid` gives each parallel sticky session its own IP so ten browser profiles don't share one address. Drop `sst` and `ssid` entirely and you get a fresh IP per request.

Four things to test on a trial before you buy volume:

1. **Per-request rotation speed.** Country-only targeting is the fastest. Stack state + city + ISP filters and you shrink the available pool.
2. **Sticky session length.** 15 minutes is a sane default for account work; some providers cap sticky sessions at 30 minutes, so if you need multi-hour persistence, verify it on your target rather than trusting a comparison table.
3. **Geo granularity against your real targets.** City and ISP targeting is where cheap providers commonly thin out. Test the specific city you care about, not just the country.
4. **Concurrency.** Rotation is worthless if the gateway throttles you at ten parallel threads. Push it before committing to a bigger tier.

> A narrow filter looks like precision until it costs you success rate. If a job fails on `country + city + ISP`, retest with country alone before blaming the pool.

Protocols are standard HTTP/HTTPS and SOCKS5, so anything that accepts a proxy URL — requests, httpx, Scrapy, Playwright, Puppeteer, curl — works without a custom integration.

## The full 9Proxy plan list

Everything currently on the vendor's pricing structure, across all three product lines:

| Package | Model | What you get | Price | Effective rate | Get it |
| --- | --- | --- | --- | --- | --- |
| 100 IPs | Per IP | Residential IPs, unlimited bandwidth, no expiry on unused IPs | $24 | $0.24/IP | [ Start with 100 IPs](https://bit.ly/9-Proxy) |
| 500 IPs | Per IP | Same model, larger pool | $72 | $0.144/IP | [ Take the 500-IP tier](https://bit.ly/9-Proxy) |
| 1,000 IPs + 500 bonus | Per IP | 1,500 addresses total | $126 | $0.084/IP | [ Order the 1,500-IP package](https://bit.ly/9-Proxy) |
| 2,500 IPs | Per IP | Budgeted for steady multi-project use | $210 | $0.084/IP | [ Check the 2,500-IP plan](https://bit.ly/9-Proxy) |
| 5,000 IPs | Per IP | Agency-scale address inventory | $360 | $0.072/IP | [ See the 5,000-IP package](https://bit.ly/9-Proxy) |
| 15,000 IPs | Per IP | Regional teams, high parallelism | $720 | $0.048/IP | [ Unlock 15,000 IPs](https://bit.ly/9-Proxy) |
| 25,000 IPs | Per IP | Reseller / automation-lab volume | $863 | $0.035/IP | [ Compare the 25,000-IP plan](https://bit.ly/9-Proxy) |
| 50,000 IPs | Per IP | Platform-level operations | $1,438 | $0.029/IP | [ Get the 50,000-IP tier](https://bit.ly/9-Proxy) |
| 100,000 IPs | Per IP (Business) | Enterprise wholesale pricing | $2,300 | $0.023/IP | [ Request the 100,000-IP package](https://bit.ly/9-Proxy) |
| 200,000 IPs | Per IP (Business) | Large-scale reseller stock | $4,140 | $0.021/IP | [ See the 200,000-IP package](https://bit.ly/9-Proxy) |
| 500,000 IPs | Per IP (Business) | Lowest published per-IP rate | $8,625 | $0.018/IP | [ Price the 500,000-IP package](https://bit.ly/9-Proxy) |
| 5 GB | Per GB | Rotating endpoints, 180-day validity | $15 | $3.00/GB | [ Buy the 5 GB pack](https://bit.ly/9-Proxy) |
| 50 GB + 5 bonus | Per GB | Most popular entry tier | $105 | $2.10/GB | [ Grab the 55 GB pack](https://bit.ly/9-Proxy) |
| 100 GB | Per GB | Regular multi-target automation | $150 | $1.50/GB | [ Take the 100 GB plan](https://bit.ly/9-Proxy) |
| 200 GB | Per GB | Mid-size scraping and monitoring | $200 | $1.00/GB | [ Order 200 GB](https://bit.ly/9-Proxy) |
| 1,000 GB | Per GB | Daily SERP and retail monitoring | $800 | $0.80/GB | [ Check the 1,000 GB tier](https://bit.ly/9-Proxy) |
| 2,000 GB | Per GB | Multi-tool, multi-region teams | $1,500 | $0.75/GB | [ See the 2,000 GB package](https://bit.ly/9-Proxy) |
| 3,000 GB | Per GB (Enterprise) | Validity never expires, team mode (1 owner + 5 members) | $2,160 | $0.72/GB | [ Compare Enterprise 3,000 GB](https://bit.ly/9-Proxy) |
| 6,000 GB | Per GB (Enterprise) | Shared non-expiring team bandwidth | $4,200 | $0.70/GB | [ Get Enterprise 6,000 GB](https://bit.ly/9-Proxy) |
| 10,000 GB | Per GB (Enterprise) | Lowest published per-GB rate | $6,800 | $0.68/GB | [ Price Enterprise 10,000 GB](https://bit.ly/9-Proxy) |
| Starter bundle | IP + GB | 100 IPs + 5 GB, 180-day traffic validity | $30 | — | [ Buy the Starter bundle](https://bit.ly/9-Proxy) |
| Popular bundle | IP + GB | 1,500 IPs + 50 GB | $180 | — | [ Take the Popular bundle](https://bit.ly/9-Proxy) |
| Pro bundle | IP + GB | 5,000 IPs + 500 GB | $720 | — | [ Order the Pro bundle](https://bit.ly/9-Proxy) |

Two notes on that table. First, 9Proxy adjusted IP-based and bundle pricing on 1 June 2026 while leaving GB-based prices untouched — the per-GB tiers have been stable, the per-IP tiers are the ones that moved. Second, a few of the mid-volume per-IP totals are rounded, so treat the per-IP figure as the reliable number and confirm the cart total at checkout.

## Which tier actually fits which job

The cheapest package is usually the right first purchase, because both unused GB (180 days on standard tiers) and unused IPs carry over. Buying small and topping up costs you nothing extra for several weeks, whereas buying 25,000 IPs for a workload that burns 2,000 is money parked in an account.

- **One scraper, one target list:** the 100-IP pack at $24 or the 5 GB pack at $15. If you don't know which model suits your workload, the $15 pack is the cheaper way to find out.
- **Light ongoing scraping plus SEO checks:** the 55 GB pack at $105 lands at $2.10/GB, comfortably below the ~$4/GB market median.
- **Multi-account work with antidetect browsers:** per-IP, because the address stays put and bandwidth isn't metered. 500 IPs at $72 covers a lot of profiles.
- **Retail or travel monitoring at volume:** 200 GB at $1.00/GB is the point where per-GB pricing stops being a rounding error in your budget.
- **Agency or team with mixed workloads:** a bundle, since some jobs want fixed addresses and others want cheap rotation. Enterprise adds shared non-expiring bandwidth across five members.

## Signing up, invite codes, and paying

9Proxy runs an invite-code sign-up model, and its affiliate terms offer referred users a 5% discount, so the entry point matters more than usual here — the code you register with is what tags the discount to your account. A limited free trial exists for new users and depends on availability; if you ask for one, specify whether you want the IP-based or GB-based version.

Payment options are broader than most proxy shops: credit and debit cards, bank cards, crypto (USDT, BTC, ETH, LTC, DOGE and others), Alipay, Apple Pay and Google Pay. Reseller and wholesale plans are available separately with dedicated support.

[👉 Create your account and claim the referred-user discount](https://bit.ly/9-Proxy)

## Where 9Proxy is the wrong tool

Twenty million IPs across 90+ countries is a mid-market pool. Enterprise networks advertise 100M+ to 175M+ addresses across 195 countries, and that difference shows up on hard targets.

One published comparison places success rates at 95%+ on lightly protected sites and 85–92% on moderately protected ones, and advises against using budget providers for Amazon, high-volume Google SERP work, or LinkedIn. The same comparison flags limited city-level targeting. That's consistent with how the per-GB market works generally: you're trading per-request reliability on heavily defended sites for a much lower per-gigabyte price.

Also worth knowing before you commit: user feedback on the platform is mixed rather than uniformly glowing. A listing that aggregates user ratings shows an average in the low 4s with comments praising stability in Dolphin Anty and AdsPower setups, alongside at least one report of a period when the service was unreachable. If your workflow can't tolerate an outage, that's a reason to keep a second provider configured rather than a reason to skip testing this one.

## The short version

Figure out whether you're paying for bandwidth or for addresses before you compare a single price. Heavy sessions and account work point at per-IP; wide, light, independent requests point at per-GB. Then test the one thing you can't read off a pricing page — how the pool behaves against your specific target, in your specific city, at your specific concurrency.

Both 9Proxy models run from one account with no subscription, non-expiring IP balances, and GB traffic valid for six months, which makes it a low-commitment way to run that test. Start on the 5 GB pack or the 100-IP tier, measure your real success rate and your real cost per thousand pages, and scale only the side that earned it.

[👉 Start with the smallest package and test it against your own targets](https://bit.ly/9-Proxy)
