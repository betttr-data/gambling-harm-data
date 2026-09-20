# Schema — `gambling-harm-index.csv`

**Resource name:** `gambling-harm-index`
**Rows:** 51 (50 states + the District of Columbia), one per jurisdiction
**Primary key:** `state`
**Refresh cadence:** monthly, on the 15th at 9:00 a.m. Eastern
**Edition covered here:** 2026-10
**Encoding:** UTF-8, comma-delimited, header row, quoted where needed

---

## What this file is, and is not

It is a table of **how much help-seeking is visible** — how many people contacted a helpline, enrolled in self-exclusion, or entered treatment, as reported by whoever reports it.

It is **not** a measure of how much gambling harm exists in a state. Nothing published in the United States measures that.

There is no composite score. There is no "harm index number" per state, and there will not be one, because the inputs are not comparable enough to earn it.

## The two layers, and why they are kept apart

| Layer | Columns | Comparable across states? |
|---|---|---|
| **National helpline layer** | `helpline_contacts_2025`, `helpline_contacts_2024`, `helpline_rate_per_100k_2025`, `helpline_rate_per_100k_2024`, `helpline_yoy_change` | **Yes.** One publisher (NCPG, via the Omni Institute), one method, all 51 jurisdictions. |
| **State-published layer** | `state_published_indicator`, `state_published_latest_value`, `state_published_latest_period`, `state_publisher`, `state_source_url`, `machine_readable` | **No.** Each state counts a different thing over a different period under different rules. Never ranked. Adding these up would be wrong. |

## Columns

| # | Column | Type | Unit / values | Notes |
|---|---|---|---|---|
| 1 | `state` | string | — | Jurisdiction name. Unique. |
| 2 | `state_code` | string | 2-letter USPS | `DC` for the District of Columbia. Unique. |
| 3 | `helpline_contacts_2025` | integer | contacts | Calls, texts and chats, CY2025, NCPG Appendix A. |
| 4 | `helpline_contacts_2024` | integer | contacts | Same measure, CY2024. |
| 5 | `helpline_rate_per_100k_2025` | number | contacts per 100,000 residents | Taken **verbatim** from NCPG's published rate, not recomputed, so this file and NCPG always agree. |
| 6 | `helpline_rate_per_100k_2024` | number | contacts per 100,000 residents | Same, CY2024. |
| 7 | `helpline_yoy_change` | string | `increase, p<.001` · `decrease, p<.001` · `no significant change` · other NCPG wording | NCPG's own Poisson significance test, reproduced verbatim. Not recomputed by Betttr. |
| 8 | `state_funds_pg_services_fy2025` | string | `Yes` · `No` | Dedicated public funding for problem-gambling services, FY2025. |
| 9 | `publication_tier` | string | `A` · `B` · `C` · `U` | See tiers below. |
| 10 | `state_published_indicator` | string | free text | What the state publishes, in its own words, or `None published`. |
| 11 | `state_published_latest_value` | **string** | number-as-text **or** a marker | Deliberately a string: four non-numeric markers live in this column. **Not comparable across states.** |
| 12 | `state_published_latest_period` | string | `CY2025` · `FY2026` · `as of 9/2/2026` · `unknown` · `N/A` | No value appears in this file without a period. |
| 13 | `state_publisher` | string | free text | The agency, regulator, lottery or council that published it. |
| 14 | `state_source_url` | string (uri) | URL or `N/A` | Source for the state-published value. |
| 15 | `machine_readable` | string | `Yes` · `No` | Whether the state publishes this in CSV/JSON/API/extractable HTML rather than a PDF, image or viewer. |
| 16 | `notes` | string | free text | What was checked, what was blocked, and why a marker was used. |

## Publication tiers (column 9)

| Tier | Meaning |
|---|---|
| **A** | Publishes a recurring, dated count. |
| **B** | Publishes something stale or partial. |
| **C** | Publishes nothing we could find, after checking the state behavioral-health agency, the gaming regulator or lottery, and the state council where one exists. The checks are named in `notes`. |
| **U** | A series is believed to exist but could not be retrieved — the host blocked automated fetch, or the figure exists only as an image or inside a viewer with no text layer. **Not** a conclusion that the state publishes nothing. |

## Missing-value markers — these are not interchangeable

| Marker (in `state_published_latest_value`) | Meaning |
|---|---|
| `N/A - state publishes nothing` | We checked the three named surfaces and no recurring gambling-harm count is published. |
| `not extracted` | A series is believed to exist but retrieval was blocked or the value is not machine-extractable. |
| `not published in readable form` | The state produces the number and puts it where the public cannot extract it — a rasterized chart, an InDesign viewer, a slide in a hearing deck. |
| `not comparable` | A figure exists but its scope or period makes cross-state comparison invalid. Shown with its caveat, never ranked. |

**`N/A` in this file never means zero harm, and never means we did not look.**

## Normalization — what is and is not done

Done:
- Rates per 100,000 residents for the helpline layer, taken from NCPG rather than recomputed.
- A stated period on every value.
- A stated scope on every self-exclusion count (commercial casinos / online only / card rooms / sports wagering / all), and whether it is an active count or a cumulative-since-inception total. Scope lives in `notes` and `state_published_indicator`.
- A publication tier per jurisdiction.

Not done:
- No estimating, modelling, imputing or interpolating. Every number is a published number with a URL.
- No composite score.
- No ranking on the state-published layer.
- No adjustment for how much legal gambling a state has.

## Known gaps

1. **32 of 51 jurisdictions publish no recurring gambling-harm count at all** (tier C). That is the single largest finding in the file and it is a finding, not a defect.
2. **Tier U rows are unresolved.** Arizona is the worked example: all AZ gaming hosts return 403 to automated fetch, so a series known to exist is recorded as `not extracted` pending manual verification. Tier U rows are the first target of each monthly refresh.
3. **A monthly clock does not mean monthly data.** Most underlying sources are annual. Each monthly edition records what was *newly published* in the preceding month, restates the standing figures, and notes what changed. In a month where nothing new is published, the edition says so.
4. **Helpline volume is a help-seeking proxy, not a harm measure.** It moves with awareness campaigns, ad mandates, state funding and helpline marketing, not only with harm. NCPG's own year-over-year test is reproduced so readers can see which changes are statistically distinguishable from noise.
5. **The 1-800-GAMBLER / 1-800-MY-RESET transition affects interpretation.** The National Problem Gambling Helpline™ number is now **1-800-MY-RESET (1-800-697-3738)**; 1-800-GAMBLER is operated independently of NCPG following a 2025 New Jersey ruling, and 1-800-522-4700 remains an active NCPG access point. Contact volumes spanning the transition may reflect routing changes as well as demand changes. Treat 2025-to-2026 comparisons with that in mind.
6. **`state_published_latest_value` is a string column.** Parsers that coerce it to numeric will silently drop every marker. Filter on `publication_tier` first.
7. **Prevalence estimates are excluded from the current-indicator columns.** Where they exist they are recorded in `notes`; several are more than fifteen years old and none is treated as current.

## Provenance

- Helpline layer: NCPG's annual National Problem Gambling Helpline report, Appendix A, prepared by the Omni Institute — one publisher, one method, all 51 jurisdictions.
- State layer: per-row, in `state_source_url`. Every state-published figure has a URL or a marker explaining why it does not.
- Nothing in this file is sourced to a news article. Press-only figures with no primary source are excluded from the published-value columns entirely.

Any figure that could not be confirmed against a primary published source is marked unverified in `notes`.

## Corrections

Corrections go to **support@betttr.net**. State agencies, councils and regulators who believe their number, scope or period is wrong here are the most valuable senders; we correct on their word plus a source. Editions are permanent and never silently edited — corrections are appended, with the original struck through, and logged at `/harm-index/corrections/`.
