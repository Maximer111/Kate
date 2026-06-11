# Local SEO + Maps Double-Check (2026-06-11)

Audit of this repo's plans (files 02, 06, 10, 14, 15, 16, 17) against the seo-local and seo-maps skill methodology (Whitespark 2026, Sterling Sky, BrightLocal 2026 factor data), plus live Tier 0 checks: landing page fetch, brand search, Bing Maps lookup, OSM/Nominatim geocoding, and directory liveness tests.

**Capability tier: Tier 0 (free).** DataForSEO MCP is not connected, so no geo-grid rank scan, no SoLV score, no live GBP field-by-field audit, no review velocity API. What could be verified live was verified live; the rest is plan-vs-methodology validation.

## Verdict

The strategy is fundamentally sound and aligned with 2026 local ranking factors. The double-check found **2 critical issues** (a Canadian legacy identity still attached to the brand, and 6 dead/broken directories in the citations list), **2 high issues** (factual errors in the schema file, zero Kate presence on the GBP-linked landing page), and several smaller calibrations. Everything fixable in the repo was fixed today; the rest became action items below.

---

## Critical findings

### 1. The brand entity is still partly anchored to Innisfil, Ontario, Canada

Live search for "Kate Kanner permanent makeup" surfaces **"Kate Kanner Permanent Makeup Innisfil | Innisfil ON"** via the old Facebook slug on the same page ID the repo lists for Makati (61555188494978), including a stale Canadian phone (+1 647-446-1994) and old email (pmubykatya@gmail.com). The page itself is renamed to Makati (verified live), but the indexed legacy identity persists.

Why it matters: ChatGPT and Copilot source local data from the Bing index and social profiles, not GBP. Today, an AI asked about Kate Kanner may answer with Canada. Citation-related signals are 3 of the top 5 AI visibility factors (Whitespark 2026); a conflicting country-level identity undermines all of them.

Fix: new section **A3.5 in file 15** (FB About scrub, close any old Canadian GBP, audit old Canadian citations). The file 17 citation wave then buries the stale signal.

### 2. Six citation targets were dead or broken

Liveness check of every directory in file 06 (curl, real browser UA, 2026-06-11):

| Site | Result | Action taken |
|---|---|---|
| yellow-pages.ph | Unreachable (dead domain) | Replaced with **yellowpages.com.ph** (HTTP 200, official PH Yellow Pages) |
| philippineslisted.com | HTTP 500, then unreachable | Removed |
| filipinoyellowpages.net | Connection refused | Removed |
| pinoylisting.com | Loads, but SSL expired = unmaintained | Skip-listed |
| wazzuppilipinas.com | Unreachable | Removed |
| bizpages.org | Unreachable | Removed |
| hotfrog.ph, tupalo.com, cybo.com, storeboard.com, brownbook.net, findyello.com | 403 = alive, bot-blocked | Kept (work fine in a browser) |

Files 06 and 17 are corrected. Replacements added (see Medium finding 5): Yelp, Tripadvisor, OpenStreetMap.

---

## High findings

### 3. Schema file (10) had factual errors, now fixed

- Phone was `+639456675438`; canonical is `0917 186 9217` = **+639171869217**. A schema deployed with the old number would have created the exact NAP inconsistency file 06 warns against. Fixed.
- Geo coordinates were `14.5547, 121.0244` (generic Makati center, ~500m off, 4 decimals). Replaced with The Plaza Royale's actual OSM coordinates **14.55938, 121.02066** (5 decimals, per the skill's precision requirement). Fixed.
- FAQ schema claimed "open daily 10:00 AM to 9:00 PM", contradicting the canonical Shabbat-observant hours. Fixed.
- Remaining caution (note added to file 10): the schema names "Reverie Aesthetic and Hair Center" while the GBP linking to that page is "Kate Kanner Permanent Makeup". Two names on one address/page blurs the entity. Resolution path: katekanner.ph carries Kate-named schema and takes over the GBP website link (file 14, Task 15), Person schema for Kate in the meantime (Task 14).

### 4. The GBP-linked landing page contains zero "Kate"

Live fetch of `iconique.com.ph/r/lp/permanent-makeup`: no mention of Kate anywhere, no visible NAP, no JSON-LD, no tel: link, no maps embed. Title tag is "Permanent Make-Up | ICONIQUE Revolutionary Beauty | ICONIQUE Philippines" (no Makati, no Kate). Caveat: the page is JS-rendered (Next.js), so Google may see more than this fetch did, but the title tag alone confirms no local or personal-brand optimization server-side.

Why it matters: Google cross-references a GBP against its linked page. "Kate Kanner Permanent Makeup" links to a page that never says Kate. This validates file 14's low Local On-Page score (7/20) and makes Task 15 (katekanner.ph) the single highest-leverage build. Cheap interim ask to Iconique: add one line of text, "Kate Kanner, Permanent Makeup Artist, Salcedo Village Makati", plus a tel: link.

---

## Medium findings

### 5. Citations list was missing the platforms AI assistants actually read

ChatGPT does not access GBP; it sources from the Bing index, **Yelp**, **Tripadvisor**, BBB, and **Reddit**. The plans covered Bing well (file 14 Tasks 3) but had none of the others. BBB is US/Canada-only, skip. Added to files 06/17:

- **Yelp** (business.yelp.com): Makati has an active, indexed Permanent Makeup category
- **Tripadvisor** (Spas & Wellness category)
- **OpenStreetMap**: business node at The Plaza Royale; OSM feeds Apple Maps and hundreds of apps. Verified live: Kate is not on OSM today (Nominatim returns nothing for the business)
- **Reddit** (bonus table): genuine participation guidance, no link-dropping

### 6. Review-ask wording: make it gating-proof

File 14 Task 2's message ("If you loved your results, a quick Google review would mean the world") is sent to all clients, so it is not technically review gating, but the conditional phrasing lives close to the line (FTC fines per violation; Google fake-engagement policy). Safer wording the helper should use:

> "Thank you so much for coming in today! Your honest feedback helps other clients find me: [link]"

File 13's own safeguards are good (no verbatim copying, spread over 60-90 days, accept short reviews) and match the skill's fake-review detection signals. Keep following them exactly: the engineered keyword pattern (service + Kate + location in every review) is precisely what spam filters look for when texts cluster, so variety matters more than keyword coverage.

## Low findings

- **GBP website link nuance** (Sterling Sky diversity update): when katekanner.ph launches, linking GBP to the homepage may suppress that homepage in organic results for the same queries. For a 5-page brand site the map pack matters more, so homepage linking is still right; just don't panic if the homepage doesn't rank organically alongside the pack.
- **Secondary categories**: file 02 lists 5; BrightLocal's optimum is 4. "Tattoo shop" is the weakest fit and can attract wrong-intent queries. Suggest dropping it unless tattoo-removal queries prove valuable.
- **GBP Q&A**: correctly absent from the plans (deprecated Dec 2025, replaced by Ask Maps AI). The FAQ content belongs on katekanner.ph as on-page FAQ + FAQPage schema (file 10 already has it).
- **Saturday closure**: businesses open at search time rank higher, so Saturday searches will favor competitors. Nothing to change (Shabbat is non-negotiable and file 14 correctly frames it as a trust signal); just expect the pattern in the data.
- **"Bi-weekly" wording** in file 14 Task 6 meant twice-weekly; reworded to avoid the helper posting every two weeks.

---

## What the plans already get right (confirmed against skill data)

- Primary GBP category "Permanent make-up clinic" = the #1 local pack factor, correctly prioritized
- 18-day review velocity rule and the 10-review invisibility threshold, both in file 14, match Sterling Sky data
- Bing Places + Apple Business Connect as week-1 claims = the skill's top two quick wins (Bing powers ChatGPT/Copilot/Alexa; Apple usage doubled to 27%)
- Dedicated service pages on katekanner.ph (Task 15) = the #1 local organic factor and #2 AI visibility factor
- Spot.ph "best of" pitch (Task 13) = the #1 AI visibility citation factor
- Owner replies to every review in Kate's first-person voice (88% of consumers favor responding businesses)
- Photo plan with keyword captions, 20+ at launch (photos drive 45% more direction requests)
- Citations under Kate's name, not the clinic's = correct portable-brand architecture
- Canonical NAP discipline with character-identical copy blocks
- US-centric data aggregators (Data Axle, Neustar) correctly absent for a PH business

## Cross-platform presence snapshot (live, Tier 0)

| Platform | Status 2026-06-11 |
|---|---|
| Google Business Profile | Live, verified, 5.0 stars, 4 reviews (per file 14) |
| Bing Places | Not found. Claim is file 14 Task 3, unblocked |
| Apple Maps | Unknown (no public API); assume unclaimed. Task 4 |
| OpenStreetMap | Not present. Now row 14 in file 17 |
| Facebook | Live, renamed to Makati, legacy Innisfil identity still indexed (Critical 1) |
| Yelp / Tripadvisor | Not present. Now rows 12-13 in file 17 |

## Top 10 actions, re-prioritized after this check

1. Facebook Innisfil cleanup + verify no live Canadian GBP (file 15, A3.5) - this week
2. Past-client review push to break the 10-review threshold (file 14, Task 1) - this week
3. Claim Bing Places (Task 3) - this week
4. Claim Apple Business Connect (Task 4) - this week
5. Run the corrected citation Week 1 (file 17) with the gating-proof review wording
6. Ask Iconique for the one-line "Kate Kanner" text + tel: link on the landing page (interim fix for Finding 4)
7. Launch katekanner.ph with Kate-named schema using the corrected coordinates/phone (Tasks 14-15)
8. GBP posts twice weekly + photo upload plan (file 14, Task 6 + photo table)
9. Yelp + Tripadvisor + OSM listings (file 17, rows 12-14)
10. Spot.ph pitch after 15+ reviews exist (Task 13, sequenced after social proof is in place)

## Repo changes made during this check

- file 06: dead directories removed/struck, Yellow Pages domain corrected, Yelp/Tripadvisor/OSM added
- file 10: phone, geo coordinates, FAQ hours corrected; entity-name caution added
- file 14: Task 6 cadence wording fixed
- file 15: new section A3.5, Facebook legacy cleanup
- file 17: run sheet rebuilt around verified-alive sites, dead-site table added, Reddit row added
- file 18: this report

## Limitations of this check

- Tier 0: no geo-grid scan, so no SoLV/map-pack position heatmap; no live GBP field audit (categories/attributes/services were validated against the repo's screenshots and files, not the API); no review velocity or sentiment API data
- The landing page is JS-rendered; the fetch saw the server-side HTML only
- Directory liveness was tested from a non-PH IP; a site that geo-blocks foreign traffic could look dead. The helper should trust the dead-site table but may re-verify in a PH browser in seconds
- Web search results are US-localized; PH-localized SERPs may differ
- Installing the DataForSEO extension would unlock the geo-grid scan, competitor review intelligence, and an automated GBP audit (`/seo maps grid "permanent makeup" "Makati"`) once reviews and citations are in place; most valuable around Day 45-60
