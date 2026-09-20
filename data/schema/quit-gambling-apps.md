# Schema — `quit-gambling-apps.csv`

**Resource name:** `quit-gambling-apps`
**Rows:** 107 unique apps (63 classified gambling-specific)
**Primary key:** `track_id`
**Pull date:** 2026-09-20
**Refresh cadence:** monthly, with the Gambling Harm Index
**Encoding:** UTF-8, comma-delimited, header row

---

## What this file is

A **dated panel** of apps surfaced on the U.S. iOS App Store by three seed searches:

- `quit gambling` (50 results)
- `gambling blocker` (49 results)
- `gambling addiction recovery` (50 results)

Endpoint: `https://itunes.apple.com/search?term={term}&entity=software&country=us&limit=50`

107 unique apps across the three queries, of which 63 are classified gambling-specific harm-reduction tools after hand review.

## It is a panel, not a census — read this before using any count

The Apple search endpoint returns **at most 50 results per term**. This file is what those three searches surface on one day, not everything on the store. **Treat every count derived from it as a floor, never as a total.** Any sentence of the form "there are N quit-gambling apps" is unsupported by this file; "at least N appear in these three searches" is supported.

## Betttr is in this dataset

Betttr's own app is in this panel, pulled by the same query, classified by the same rule, with no adjustment and no favorable placement. We are in our own dataset and we say so every time.

## Columns

| # | Column | Type | Unit / values | Notes |
|---|---|---|---|---|
| 1 | `track_id` | integer | — | Apple's numeric app identifier. Stable across releases; the join key. |
| 2 | `app_name` | string | — | Title as listed on the pull date. |
| 3 | `seller_name` | string | — | As Apple publishes it. Often an individual's name for solo-developer apps; reproduced as published, not normalized. |
| 4 | `bundle_id` | string | — | Reverse-DNS bundle identifier. |
| 5 | `app_store_url` | string (uri) | — | Canonical U.S. listing URL. |
| 6 | `release_date` | date | `YYYY-MM-DD` | First store appearance, UTC, truncated to the day. |
| 7 | `current_version_release_date` | date | `YYYY-MM-DD` | Ship date of the listed version, UTC, truncated to the day. |
| 8 | `app_version` | string | — | Version string on the pull date. |
| 9 | `months_since_update` | number | months, 1 decimal | `current_version_release_date` to the pull date. |
| 10 | `launched_last_12_months` | string | `Y` · `N` | Derived from `release_date` against the pull date. |
| 11 | `stale_6mo` | string | `Y` · `N` | Derived from `months_since_update >= 6`. |
| 12 | `user_rating_count` | integer | ratings | All versions, U.S. store. |
| 13 | `user_rating_count_current_version` | integer | ratings | Current version only. |
| 14 | `average_user_rating` | number | stars, 0–5 | Full published precision. **Meaningless at low counts** — see gaps. |
| 15 | `primary_genre` | string | — | Apple's primary genre. |
| 16 | `genres` | string | `; `-separated | All Apple genres. |
| 17 | `app_store_category` | string | `harm-reduction` · `gambling-product` · `not-gambling` · `other` | Betttr's hand-assigned classification. |
| 18 | `content_advisory_rating` | string | e.g. `17+` | Apple age rating. |
| 19 | `minimum_ios_version` | string | e.g. `16.4` | Minimum OS the listing requires. |
| 20 | `gambling_specific` | string | `Y` · `N` | See classifier rule below. |
| 21 | `matched_search_terms` | string | `; `-separated | Which of the three seed searches returned this app. |

## The classifier rule (`gambling_specific`, column 20)

`Y` requires **all** of:

1. Listed on the U.S. iOS App Store in at least one of the three searches;
2. **Not** in the Games/Casino category — which removes real-money and social-casino apps; and
3. Gambling-specific: the app name **or the first 300 characters of its own description** names gambling, betting, a sportsbook, a casino or wagering.

General addiction and sobriety apps that merely mention gambling in a list of behaviours are excluded and named: *Gambless: Addiction Recovery, Gambulance: Addiction Tools, Quit Bad Habits & Addiction, SMART Recovery, Sanad — Recovery Companion, Sober Today — Day Counter*.

Hand-reviewed for the 2026-10 edition.

## Classification breakdown (`app_store_category`, column 17)

| Value | Rows | Meaning |
|---|---|---|
| `harm-reduction` | 69 | A quit-gambling or gambling-recovery tool. |
| `gambling-product` | 21 | A real-money or social-casino product returned by the search. |
| `not-gambling` | 16 | Unrelated to gambling. |
| `other` | 1 | Reviewed, none of the above. |

Note that `app_store_category = harm-reduction` (69) and `gambling_specific = Y` (63) are **different tests** and do not agree row-for-row. Column 17 is the editorial category; column 20 is the mechanical classifier. Use column 20 for reproducible counts, column 17 for reading.

## Panel-level figures from the pull (2026-09-20)

- 42 of 107 launched in the last 12 months
- 13 not updated in 6+ months
- 15 with zero ratings; 42 with fewer than 10
- **Median rating count: 3**
- Of the 63 gambling-specific apps: 67% launched in the last 12 months, 21% not updated in 6+ months, 67% under 10 ratings

The headline that follows from those figures is churn, not choice: this is a category of very new, very small, largely unrated apps, a fifth of which have already been abandoned by their developers.

## Known gaps

1. **50-result cap per query.** Counts are floors. See above.
2. **Three seed terms only.** Apps that describe themselves in other language (*sports betting addiction*, *stop betting*, *bet blocker* as one word) may be missed. The seed list is fixed across editions so the series stays comparable; adding a term would be a versioned method change, dated and noted.
3. **iOS only, U.S. store only.** No Android, no other storefronts.
4. **`average_user_rating` is unusable at these counts.** The median app has 3 ratings. Do not rank on it, do not average it across the panel, and do not compare a 5.0 from 2 ratings with a 4.4 from 4,000.
5. **One-day snapshot.** App Store metadata changes continuously; every value is as of 2026-09-20. Each monthly edition is kept at its own URL so the series can be differenced.
6. **No pricing or monetization columns.** Price and formatted-price fields exist in the upstream API response and are deliberately excluded from this published file. Business-model comparisons cannot be made from it.
7. **`seller_name` is not a company registry.** It is the App Store seller string, which is sometimes an individual, sometimes a trading name, and is not deduplicated across apps by the same developer.
8. **No download or revenue estimates.** Apple publishes none, and this file does not model any.
9. **Self-interest disclosure.** Betttr's app is a row in this file. Any analysis that ranks apps should say the publisher is in the ranking.

## Provenance

Apple iTunes Search API, U.S. iOS App Store, pulled 2026-09-20. The raw API response is retained. Classification (column 17) and the gambling-specific flag (column 20) are Betttr's, applied by the published rule and hand-reviewed.

## Corrections

**support@betttr.net.** Developers who believe their app is misclassified should say so; we correct on their word plus the listing, and the correction is dated in the next monthly edition.
