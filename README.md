# vps ddos protection: What "up to 600 Gbps" actually covers, what triggers a null route, and how to choose a plan

Most "DDoS protected VPS" listings lead with a big number. That number is usually the ceiling of a paid tier, not what your box gets the moment it boots. Two providers can both advertise "DDoS protected" and give you completely different things on day one — one filters quietly at the edge, the other null-routes your IP for an hour and calls it protection.

So before comparing mitigation capacity, find out three things: what's included free, what triggers a blackhole, and what happens to your traffic bill when an attack arrives. GoMami (a Hong Kong / Japan / Singapore provider aimed at mainland China routes) is a useful case study because its marketing page and its documentation answer those questions very differently.

> **Quick pick:** The EPYC 7763 **Mini at $39/month** (2 vCPU / 4GB / 40GB NVMe / 1TB traffic / 1Gbps port) covers most small sites and game servers, and it includes the same baseline DDoS filtering as the $199 plan. Go up to the **Ryzen 9 9950X Mini at $59** only if you need single-core speed or the 2Gbps port.
> 👉 [See all six GoMami plans and current monthly prices](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore)

## What does "DDoS protected VPS" actually include by default?

On GoMami, default protection is **best-effort basic scrubbing, free on every instance**. The 600 Gbps professional scrubbing is a **paid add-on**, and its price isn't published — the docs say to contact support or check the site.

That distinction matters. The homepage and ad banners say "up to 600 Gbps mitigation capacity," "operator-level joint scrubbing," "GoMami secondary scrubbing wall," "VIP one-on-one security service." The documentation splits it into two tiers:

| Tier | What you get | Cost |
| --- | --- | --- |
| Default | Best-effort basic traffic scrubbing, automatic, no configuration needed | Free, on all instances |
| Advanced | 600 Gbps professional DDoS scrubbing | Paid add-on, price not listed |

The free tier isn't nothing. According to GoMami's docs it covers UDP Flood, SYN Flood, ACK Flood, ICMP Flood, DNS Amplification, NTP Amplification — plus HTTP Flood, CC attacks and Slowloris at layer 7, with the caveat that L7 policy "may vary by node and protection tier." Detection and scrubbing are automatic; you don't configure anything.

What you don't get in writing is a guarantee. The docs use the phrase "best-effort" twice, and add that protection capability "depends on the attack size and network conditions." That's an honest sentence and also the most important one on the page.

## The null route clause that decides whether your site stays up

If an attack is big enough to affect other customers in the same subnet, GoMami automatically blackholes (null routes) your instance's IP for **30 to 60 minutes**. It unblocks automatically. No human can override it.

Read that again if you run a single-IP service. During the blackhole, all inbound and outbound traffic to that IP is dropped. Your server isn't down — the network path to it is. Billing continues, monitoring may go quiet, and there is no support ticket that gets it lifted early, because the trigger is automatic and the release is automatic.

For a blog, that's a 30–60 minute outage. For a game server, a live checkout flow, or an API other services depend on, it's the exact failure mode DDoS protection is supposed to prevent. The mitigation number on the ad doesn't tell you this. The docs do.

Practically, the question to ask any provider — GoMami included — is whether the advanced tier changes that behavior, and whether you can get more than one IP on a single instance. GoMami's documentation doesn't answer either question, and I'm not going to guess. Ask before you buy if the null route is a dealbreaker.

👉 [Ask GoMami about the 600 Gbps add-on while you're looking at plans](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore)

## Does a bigger mitigation number mean better protection?

No. A 600 Gbps ceiling tells you the size of the pipe at the scrubbing center. It says nothing about detection speed, false positives, whether layer-7 filtering is included, or whether your IP survives an attack that lands under the ceiling.

Four questions worth asking before comparing numbers:

1. **Is the number included or upsold?** On GoMami, 600 Gbps is the paid tier; default is best-effort.
2. **What triggers a blackhole, and for how long?** GoMami publishes 30–60 minutes and an automatic release. Many providers don't publish anything.
3. **Is layer-7 covered in the base price?** GoMami lists HTTP Flood, CC and Slowloris, but flags that policy varies by tier and node.
4. **Is traffic scrubbed before or after it reaches your NIC?** Edge filtering with clean-pipe delivery keeps junk off your interface. Scrubbing after the fact still burns your bandwidth quota.

Compare that with how other providers present the same category. MurmurHost's offshore VPS-4 lists 4 vCPU (AMD EPYC), 8GB DDR4 ECC, 120GB NVMe, 6TB monthly traffic and **20 Gbps** DDoS protection, with free weekly snapshots and provisioning in under five minutes — no price published in what I could verify. QuickServers sells DDoS-protected VPS in Phoenix and Miami with mitigation in front of both locations, also without published pricing in the material I could check. A 20 Gbps and a 600 Gbps headline aren't directly comparable until you know which tier the customer actually sits in.

## GoMami's full current lineup and prices

GoMami currently lists six plans on its site, across two hardware platforms, all billed **monthly in USD**. There's no annual option shown, no first-year discount, and no renewal markup to worry about — the monthly price is the price.

| Plan | Platform | vCPU / RAM / NVMe | Traffic | Port | Price/mo | Order |
| --- | --- | --- | --- | --- | --- | --- |
| EPYC Mini | EPYC 7763 (3.5GHz) | 2 / 4GB / 40GB | 1000GB | 1Gbps | $39 | [ Order EPYC Mini](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore) |
| EPYC Air | EPYC 7763 | 4 / 8GB / 60GB | 2000GB | 1Gbps | $79 | [ Order EPYC Air](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore) |
| EPYC Pro | EPYC 7763 | 8 / 16GB / 80GB | 5000GB | 3Gbps | $169 | [ Order EPYC Pro](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore) |
| Ryzen Mini | Ryzen 9 9950X (5.7GHz) | 2 / 4GB / 40GB | 1000GB | 2Gbps | $59 | [ Order Ryzen Mini](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore) |
| Ryzen Air | Ryzen 9 9950X | 4 / 8GB / 60GB | 2000GB | 2Gbps | $99 | [ Order Ryzen Air](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore) |
| Ryzen Pro | Ryzen 9 9950X | 6 / 16GB / 80GB | 5000GB | 5Gbps | $199 | [ Order Ryzen Pro](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore) |

Three Asia-Pacific locations are listed: Hong Kong, Japan and Singapore. GoMami quotes 6ms from Hong Kong, 30ms from Japan and 36ms from Singapore, measured as the fastest province per carrier on China Telecom / Unicom / Mobile, and says mainland round-trip latency stays under 50ms.

The network is the actual reason people pick this provider: CN2 GIA, AS9929 and CMIN2 on the China legs, with Hong Kong direct. If your users aren't in mainland China or East Asia, you're paying a routing premium for something you won't use.

## Ryzen vs EPYC: what the extra $20 buys

The gap is $20/month for Mini and Air, $30/month for Pro. You're buying clock speed and port bandwidth, not more cores — in fact the EPYC Pro has **more** cores than the Ryzen Pro (8 vCPU vs 6).

- **Mini:** $39 (1Gbps) vs $59 (2Gbps) — +$20 for double the port speed
- **Air:** $79 (1Gbps) vs $99 (2Gbps) — same +$20
- **Pro:** $169 (3Gbps, 8 vCPU) vs $199 (5Gbps, 6 vCPU) — +$30 for a faster port but two fewer cores

Annualized, the EPYC Mini is $468/year versus $708 for the Ryzen Mini. Over two years that's $480 apart, for two machines that share the same 1TB of traffic and the same 40GB of disk.

The Ryzen 9 9950X at 5.7GHz boost makes sense for databases with hot single-threaded queries (MySQL InnoDB, Redis), game server ticks, or PHP request latency where one core does most of the work. If you're running nginx serving static files or a wireguard relay, the 3.5GHz EPYC 7763 is fine and the $240/year saved buys you a lot of contingency.

👉 [Compare the $39 EPYC Mini and $59 Ryzen Mini side by side](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore)

## The two cost traps that aren't on the pricing table

**Traffic is billed one-way** on GoMami, according to a May 2026 third-party writeup on the Hong Kong plans — meaning only outbound counts against your quota, and each plan includes one IPv4. The same writeup notes the EPYC line runs 1–3Gbps and the Ryzen line 2–5Gbps, which matches the official specs.

**Overage throttles rather than suspends.** A third-party review states that once you hit the monthly traffic quota, bandwidth drops to **20 KB/s** and the server stays online until the next billing cycle. That's not an extra bill, and it's also not usable — 20 KB/s is roughly modem speed. If you're anywhere near 1TB a month, price the Air tier ($79, 2TB) from the start instead of discovering the throttle mid-month.

GoMami's own FAQ lists "What happens if I reach my traffic usage limit?" as a question but doesn't publish an answer in the visible text. The 20 KB/s figure comes from third-party testing, not the provider's own page — worth confirming at checkout if you're planning to run close to the cap.

## What GoMami's scrubbing doesn't do for you

Provider-level filtering handles the flood. It doesn't stop the smaller stuff that leaks past — half-open connections piling up, ICMP amplification, malformed packets hitting your stack. GoMami's own docs recommend three iptables rules alongside the network protection:


iptables -A INPUT -p tcp --syn -m limit --limit 1/s --limit-burst 3 -j ACCEPT
iptables -A INPUT -m state --state INVALID -j DROP
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT


Those cap SYN rate, drop invalid-state packets and rate-limit ping. On the kernel side, common hardening includes raising `net.core.somaxconn` to 65535, setting `net.ipv4.tcp_rfc1337 = 1` to stop RST packets from TIME_WAIT sockets, and `net.ipv4.icmp_echo_ignore_broadcasts = 1` to blunt Smurf-style reflection.

For an attack already in progress, the standard triage is: find the source in `netstat` or logs, `sudo ufw insert 1 deny from <IP>`, block the whole /16 if it's a range, temporarily drop nginx's request limit to 1–5 req/s, then open a ticket. Layer-7 floods are where a scrubbing tier earns its money — a CC attack that looks like legitimate traffic won't be stopped by rate limits alone.

## Who shouldn't buy this

GoMami starts at $39/month. If your budget is "a few dollars a month," this is not your provider, and no amount of DDoS protection changes that arithmetic.

It's also a poor fit if your audience isn't in mainland China or East Asia. You'd be paying for CN2 GIA / 9929 / CMIN2 routing and Hong Kong direct connections that don't help a European or US-only user base. European or US-focused buyers can look at something like MurmurHost's offshore plans (20 Gbps DDoS listed, 6TB traffic, specs as published, price not confirmed) or QuickServers' Phoenix and Miami locations — both geographically better positioned, neither with a price I could verify.

And if a 30–60 minute null route on your only IP is unacceptable, get an answer from support about the advanced tier before you pay. That's a question about policy, not a spec sheet, and this provider's docs don't answer it.

## Practical answers before you check out

**Is there a free trial or money-back window?** GoMami's FAQ includes "Can I try the product before purchasing?" but I couldn't find a published answer, and no refund period is stated on the pages I reviewed. Don't assume one exists — confirm with support first.

**Can I pay annually for a discount?** All six plans are listed at monthly prices. No annual, quarterly or prepaid option appeared in the material I checked.

**Is there a working promo code?** A May 2026 third-party writeup mentioned a 15% code, and I couldn't confirm it's still active. Treat any code you find as unverified until it applies at checkout.

**Does the advanced 600 Gbps tier cost extra?** Yes, it's a paid add-on. The price isn't published. Anyone quoting you a figure for it is guessing.

## Pick by situation, not by mitigation number

Running a small site, a bot, a proxy or a game server for a China-facing audience, and you'd rather not spend more than necessary → **EPYC 7763 Mini, $39/month**, 2 vCPU / 4GB / 1TB. The DDoS filtering is the same as on the $199 plan.

Single-threaded workload — Redis, MySQL, PHP, game ticks — where 3.5GHz is the bottleneck, or you want the 2Gbps port → **Ryzen 9 9950X Mini, $59/month**. The extra $240/year buys clock speed, not capacity.

Traffic is your constraint, not CPU → skip Mini entirely. The **Air tier** doubles both traffic (2TB) and RAM for $79, which is cheaper than getting throttled to 20 KB/s halfway through the month.

You need Windows, 180GB of disk and a 5Gbps port → the **Ryzen Pro** at $199, or ask about the Turin platform, which GoMami sells separately with 12 vCPU / 32GB / 220GB configurations.

One last thing to settle before paying: whether the 600 Gbps tier changes the blackhole policy, and how many IPs you can attach. If your service can't eat a 30-minute outage, that answer decides the purchase more than any spec table.

👉 [Start with the $39 EPYC 7763 Mini and see the full plan list](https://gomami.io/aff.php?aff=415&url=https%3A%2F%2Fgomami.io%2Fstore)
