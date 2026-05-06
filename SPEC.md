# Life Choices — Spam Shield (Working Title)

**One-line pitch:** A free, crowdsourced spam-call/text reporting service that auto-files complaints with the FTC, FCC, and CFPB on the user's behalf, builds a TCPA evidence packet they can hand to a lawyer, and publishes a community blocklist any phone or app can consume.

## Why this, why now
- SMS scam volume (loan offers, "we have up to $9M ready," political blasts) jumped after STIR/SHAKEN reduced spoofed *calls*; texts are the soft underbelly.
- Existing apps (Hiya, Truecaller, Robokiller) block but don't *report* — users who want to fight back have to fill out 3+ government forms per incident.
- TCPA pays $500–$1,500 per illegal text/call. Most victims never collect because evidence isn't packaged.
- Ministry/nonprofit angle: scams disproportionately hit elderly congregants. Free + trustworthy + faith-based distribution is a real moat against ad-supported competitors.

## Target user
1. **Primary:** US adults receiving 5+ unsolicited texts/calls per week who feel powerless.
2. **Secondary:** Ministry/nonprofit administrators distributing it to congregants and members.
3. **Tertiary (revenue):** Carriers, banks, dialer-compliance vendors, plaintiff law firms.

## Core features (MVP)
1. **One-tap report.** User forwards a spam SMS or pastes a number; we extract sender, timestamp, body, and category (loan, political, IRS, romance, etc.).
2. **Auto-file to authorities.** Single submission fans out to:
   - FTC (reportfraud.ftc.gov)
   - FCC consumer complaint
   - CFPB (when financial — like the 9M loan example)
   - Carrier short code 7726
   - State AG (when state-specific patterns detected)
3. **Crowdsourced blocklist.** Numbers flagged by N independent reporters within a window land on a public list (JSON + CSV feed). Reputation-weighted to resist abuse.
4. **TCPA evidence packet.** Per number, generate a downloadable PDF with timestamped messages, sender metadata, prior reports, and a cover letter — ready for a TCPA attorney.
5. **Mobile blocking.** iOS Call Directory Extension + Android CallScreeningService consume the blocklist. (Phase 2 — start with web + API.)

## Non-goals (for v1)
- No paid tier, no ads. Free forever for individuals.
- No automated lawsuits. We package evidence; lawyers handle legal action.
- No promises to "remove" a number from the internet — out of scope.

## Monetization (post-MVP, ranked)
1. **Data feed license** to carriers / banks / dialer compliance vendors (B2B, $$$).
2. **Lawyer referral revenue share** on TCPA cases that originate from our evidence packets.
3. **White-label** for ministries, credit unions, senior-living orgs ($X/yr per org).
4. **Optional donation** tier for individuals — never a paywall.

## Architecture sketch
- **Backend:** Python (FastAPI) or Node (Fastify). Postgres for reports, Redis for rate-limit/dedupe.
- **Reporter ingest:** REST API + email-to-report (forward spam to report@...) + web form + (later) iOS share sheet & Android intent.
- **Filers:** Per-authority adapter modules (FTC, FCC, CFPB, AG). Queue-backed, idempotent, with retries.
- **Blocklist publisher:** Cron-built JSON/CSV; signed; cache-friendly URL.
- **Abuse resistance:** Reporter reputation, N-of-M threshold to publish, appeal endpoint, never auto-block numbers belonging to known legitimate businesses (whitelist from public registries).

## Risks / open questions
- **Authority forms change.** FTC/FCC/CFPB forms aren't stable APIs; adapters will need monitoring.
- **Defamation exposure.** Publishing a number as "spam" can draw a complaint. Mitigation: only publish numbers that meet the reporter threshold; prominent appeal path; safe-harbor language.
- **Privacy.** Reports contain message bodies that may include personal info. Strip/redact before publication; store raw under access controls.
- **iOS/Android distribution.** App Store review for spam-blocker apps is doable but stricter than average — plan a 2–4 week review buffer.

## Phase plan
- **Phase 0 (1–2 weeks):** Spec lock, domain + brand, legal review of TCPA packet language.
- **Phase 1 (3–4 weeks):** Backend API, web report form, FTC + 7726 adapters, public blocklist feed.
- **Phase 2 (4–6 weeks):** FCC + CFPB adapters, evidence-packet PDF, email-in ingest.
- **Phase 3 (6–8 weeks):** iOS + Android apps consuming the blocklist.
- **Phase 4:** B2B data feed, lawyer partnerships, ministry white-label.

## Decision needed before code
1. Stack preference (Python/FastAPI vs Node/Fastify vs other)?
2. Hosting (AWS, Fly.io, Render, self-hosted)?
3. Brand: standalone name, or sub-brand under Hometown Ministries / Life Choices?
4. Start with **API-only** (Phase 1) or **API + web form** together?
