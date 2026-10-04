# Changelog

All notable changes to **Gambling Harm Open Data**. Newest first.

Releases are permanent. Nothing is overwritten and no correction is silently substituted — a corrected value is published in a new release with a dated note naming what changed and why, and the prior release stays live at its tag and its version DOI.

Method changes are dated and listed, and **never applied retroactively to a published release**.

Format: [Keep a Changelog](https://keepachangelog.com/). Versioning: `YYYY.M.PATCH` — the year and month of the edition the data covers, plus a patch number for corrections within that edition.

---

## [2026.9.0] — 2026-09-21

First public release.

### Added
- `data/gambling-harm-index.csv` — 51 rows (50 states + DC), 16 columns. September 2026 baseline edition. Helpline layer from NCPG Appendix A (CY2024 and CY2025 contacts, rate per 100k, NCPG's own Poisson test). State-published layer with per-row source URL, period, publisher and publication tier.
- `data/sportsbook-rg-tools.csv` — 14 operators, 28 columns. 2026-Q3 edition. Documentation-only; no dated screenshots in this release.
- `data/recovery-glossary.csv` — 125 terms across four sections, 10 columns. 32 entries carry a source flag (25 unsourced, 7 partial) and say so.
- `data/quit-gambling-apps.csv` — 107 apps, 21 columns. Panel pulled 2026-09-20 from three seed searches against the Apple iTunes Search API.
- `data/self-exclusion-programs.csv` — 11 state programs + the multi-state NVSEP row, 8 columns. 2026-Q3.
- `data/schema/` — one plain-language column dictionary per dataset: every column, its units, its missing-value markers, and its known gaps.
- `datapackage.json` — Frictionless Data Package v2 descriptor with real field schemas for all five resources, byte sizes and SHA-256 hashes.
- `CITATION.cff` — CFF 1.2.0, `type: dataset`, organizational author, concept and version DOIs.
- `LICENSE` — CC BY 4.0 full legal text.

### Notes on this release
- **DOIs.** Concept DOI 10.5281/zenodo.22857767 (always the newest version); version DOI 10.5281/zenodo.22857768 for 2026.9.0. Minted by Zenodo on 2026-09-21 from the v2026.9.0 GitHub release; the README, CITATION.cff and datapackage.json were updated on `main` the same day (the archived v2026.9.0 zip carries the pre-DOI placeholders — cite the DOI, not the zip).
- **`self-exclusion-programs.csv` is not a 50-state census.** 11 jurisdictions verified. Absence of a state is absence of verification, not absence of a program. This is the largest open gap in the release.
- **`quit-gambling-apps.csv` is a panel, not a census.** The Apple search endpoint caps at 50 results per term. Every count derived from it is a floor.
- **No composite score anywhere**, and no ranking on the state-published layer, by design.
- **Betttr's own app is a row** in `quit-gambling-apps.csv`, classified by the same rule as every other app.

### Known issues carried into the next release
- Tier `U` rows in the Harm Index — states whose series exist but could not be retrieved (Arizona is the worked example: all AZ gaming hosts return 403 to automated fetch). First target of the November refresh.
- 25 unsourced glossary entries, 21 of them sports-betting jargon with no authoritative definitional body. Two clinical instruments (SOGS, Lie/Bet) need a primary-source pass and should not be cited from this file until they get one.
- Sportsbook RG Tools has no dated screenshots and no per-state parameter values; operators generally do not publish either.
- Self-exclusion durations and reinstatement rules are not yet captured.

## [2026.9.1] — 2026-09-23 — corrections (applied; the 2026.9.0 archive is unchanged) — version DOI 10.5281/zenodo.22908453
- `datapackage.json`: recomputed `bytes`/`sha256` for `gambling-harm-index.csv` (corrected rows) and `sportsbook-rg-tools.csv` (the 2026-09-21 Fanatics written-self-exclusion correction had left its hash stale).
- **Ohio (OH) — APPLIED 2026-09-23:** Commission publishes MONTHLY Time Out Ohio VEP statistics (Statistics tab, https://casinocontrol.ohio.gov/responsible-gambling/06-resources-reports-statistics) and FY totals in annual reports (https://casinocontrol.ohio.gov/about/ar/05-annual-reports). Our "self-exclusion not published" marker was wrong → add monthly VEP series; credit Ohio Casino Control Commission (Nabil Pervaiz, RG Manager, 2026-09-22).
- **Maryland (MD) — APPLIED 2026-09-23:** Monthly VEP enrollment is published inside Commission meeting records (https://www.mdgaming.com/commission/meeting-minutes-documents/, Managing Director of Gaming section) → add; decide/describe "published in meeting records" as a source class; credit Maryland Lottery and Gaming (Seth Elkin, 2026-09-22).
- **Virginia (VA) — APPLIED 2026-09-23:** Add the Virginia Partnership for Gaming & Health treatment/recovery dashboard (https://vpgh.vcu.edu/) as a treatment series; credit VPGH/VCU (Carolyn Hawley, 2026-09-22). Dashboard is a live Tableau view; recorded as a source, no static value.

## Pending for 2026.10.0 (noted 2026-09-24)
- Ohio: publisher rename — Ohio Department of Mental Health and Addiction Services (OhioMHAS) → **Ohio Department of Behavioral Health (DBH)**, dbh.ohio.gov. Verify the SFY2025 annual report URL still resolves after the domain move.
- Iowa: IDPH merged into Iowa HHS; SFY2023 is confirmed the newest published problem-gambling report (hhs.iowa.gov, checked 9/24).

## 2026.9.2 — 2026-09-24 corrections
- **Oklahoma: tier C → A.** Credit: Oklahoma Association on Problem Gambling and Gaming (Kenzie Simpson). OAPGG publishes an annual statewide new-self-exclusion series (2012–2025; 581 in 2025) with demographic breakdowns, and an annual requests-for-support count (763 in 2025) at oapgg.org/oklahoma-gambling-statistics. We had checked ODMHSAS only. ODMHSAS treatment counts remain unpublished (per OAPGG). Headline counts change: **17 jurisdictions publish no recurring count (was 18); 10 of those fund services (was 11).**
- **Iowa: verified.** Iowa Racing & Gaming Commission (Michael Poundstone, Compliance Officer) confirmed 2026-09-24 that the row's 2025 Annual Report figures match; note added that the active count moves daily with enrollments, 5-year expirations and revocations.
- Headline-count consumers to update: /harm-index/ page text, /data/ page, README, Kaggle description, gambling-helpline hub intro, every outreach template ('18 of 51' → '17 of 51'; '11 of those' → '10 of those').
- **Virginia: sources added** (2026-09-24, credit: Virginia DBHDS, Anne Rogers, Problem Gambling Prevention Coordinator): DBHDS annual report page; VASIS PGTS Fund reimbursement dashboard; VASIS All-Payer Claims problem-gambling dashboard. CSBs not yet reporting PG admissions. Virginia: 6 published indicators.
- **West Virginia: SFY25 annual report supplied by PGHN-WV** (Maricel Bernardo) as a private SharePoint link — figures + public URL requested before the row changes.
- **Arizona: tier U → A** (2026-09-24). Verified from a US browser after the Department of Gaming's public-affairs office replied: the Division of Problem Gambling publishes a monthly helpline intake series (2009–Feb 2025; 1,197 intake calls in 2024, 671 in 2023). Self-exclusion counts remain unpublished — public-records portal only. Headline: **Colorado is now the only unverified row.** Credit: Arizona Department of Gaming (publicaffairs@).
- **California: tier B → A** (2026-09-25, credit: California Council on Problem Gambling): CalPG publishes a monthly Helpline Interactive Data Dashboard (calpg.org/hidd), updated by the 20th of each month. We had checked CDPH only. CDPH's treatment report remains FY2015-16.
- **Arizona (addendum, 2026-09-25)**: the Department Annual Report (gaming.az.gov/resources/reports) carries annual self-exclusion figures (active casino, active EWFS, new, cumulative). Source added; figures queued for 2026.10.0 (next report imminent). Credit: Arizona Department of Gaming public affairs.
- **Pennsylvania: source added** (2026-09-28, credit: PA DDAP, Amy Hubbard): DDAP 2024-25 annual report for treatment admissions (SFY; DDAP-paid clients only). **Nevada: verified absence** — NGCB Records & Research states under NRS 239 it holds no responsive documents; the row's 'regulator publishes no SE/helpline count' stands as an official statement.

## Pending for 2026.10.0 (noted 2026-10-02, dataset audit)
- **`data/schema/gambling-harm-index.md` Known gaps corrected (applied 2026-10-02 on `main` and the iCloud working copy):** gap 1 said "32 of 51 publish no recurring count" — a pre-release draft number; the verified figure is 17 (18 at baseline). Gap 2 used Arizona as the tier-U example; Arizona was resolved on 2026-09-24 and Colorado is the only remaining tier-U row.
- **`data/self-exclusion-programs.csv` is contradicted by our own Harm Index.** The directory lists 11 state programs + NVSEP, but `gambling-harm-index.csv` records statewide self-exclusion programs with published counts in Arizona (Department of Gaming annual report), Iowa (statewide, active enrollees), Kansas (Casino VEP + Sports Wagering Exclusion Program), Maine (sports-wagering list), New Mexico (new statewide self-exclusions), Oklahoma (OAPGG annual series), Virginia (Voluntary Exclusion Program), Washington (card rooms) and the District of Columbia — none of which are in the directory. Missouri, Louisiana, West Virginia, Tennessee, Arkansas, Mississippi, North Carolina and Nevada-adjacent tribal compacts also need checking. Action for 2026.10.0: expand the CSV to every statewide program we can verify from a primary URL (enrollment method, agency, URL, scope), keep the "verified so far" framing until it is a census, and stop describing the directory as "every U.S. state program" anywhere (site title/meta/H1, outreach templates). The 11-state list mirrors the app's self-exclusion wizard, which is a product scope, not the national count.
- **Corrections count for outreach copy:** six states have had rows corrected with a dated note (OH, MD, VA on 9/23; OK, AZ, CA on 9/24–25). Iowa and Nevada were *verified* (no change); Pennsylvania and Virginia had sources *added*. Templates said "five" — use "six corrected, two verified, two expanded" or just "six."
- Repo `main` still trails the iCloud working copy by the 2026-09-28 Nevada/Pennsylvania note edits (`gambling-harm-index.csv` notes column + this CHANGELOG). Synced to the working tree 2026-10-02; **uncommitted — pending CC commit + push.** `.gitattributes` says `*.csv text eol=lf` but every CSV is CRLF in HEAD; `git status` shows all five as modified for that reason alone. Decide at 2026.10.0: normalize to LF and recompute `datapackage.json` hashes, or drop the eol rule.
- **NCPG attribution language added (2026-10-03, requested by Cait Huble, NCPG Director of Public Affairs, 2026-10-02):** README, `data/schema/gambling-harm-index.md`, the HF dataset card, and (via Replit #22) /harm-index/, /harm-index/methodology/ and /data/ now carry NCPG's required note that 1-800-GAMBLER traffic is included in NCPG reporting only 2023-06-01 → 2025-09-30, so post-2025-10-01 volume changes reflect methodology, not help-seeking. Credit: NCPG.
- **`data/self-exclusion-programs.csv` expanded 12 → 38 rows (2026-10-03, working copy for 2026.10.0).** 26 state programs added from official regulator/lottery pages (AZ, CA card rooms, DC, DE, GA lottery, IA, KS, KY, LA, ME, MO, MS, MT, NC, NE, NH, NM, OK, RI, SD, TN, VA, VT, WA, WV, WY); durations and removal rules recorded in `notes`; fields not confirmed on an official page are marked UNVERIFIED in `notes`. 13 jurisdictions documented as having no statewide program (schema Known gaps §1). This closes the "11 state programs" overclaim flagged 2026-10-02. Site page /self-exclusion/ follows via Replit #24.
