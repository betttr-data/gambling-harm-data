# Changelog

All notable changes to **Gambling Harm Open Data**. Newest first.

Releases are permanent. Nothing is overwritten and no correction is silently substituted — a corrected value is published in a new release with a dated note naming what changed and why, and the prior release stays live at its tag and its version DOI.

Method changes are dated and listed, and **never applied retroactively to a published release**.

Format: [Keep a Changelog](https://keepachangelog.com/). Versioning: `YYYY.M.PATCH` — the year and month of the edition the data covers, plus a patch number for corrections within that edition.

---

## [2026.10.0] — 2026-10-15

First public release.

### Added
- `data/gambling-harm-index.csv` — 51 rows (50 states + DC), 16 columns. October 2026 edition. Helpline layer from NCPG Appendix A (CY2024 and CY2025 contacts, rate per 100k, NCPG's own Poisson test). State-published layer with per-row source URL, period, publisher and publication tier.
- `data/sportsbook-rg-tools.csv` — 14 operators, 28 columns. 2026-Q3 edition. Documentation-only; no dated screenshots in this release.
- `data/recovery-glossary.csv` — 125 terms across four sections, 10 columns. 32 entries carry a source flag (25 unsourced, 7 partial) and say so.
- `data/quit-gambling-apps.csv` — 107 apps, 21 columns. Panel pulled 2026-09-20 from three seed searches against the Apple iTunes Search API.
- `data/self-exclusion-programs.csv` — 11 state programs + the multi-state NVSEP row, 8 columns. 2026-Q3.
- `data/schema/` — one plain-language column dictionary per dataset: every column, its units, its missing-value markers, and its known gaps.
- `datapackage.json` — Frictionless Data Package v2 descriptor with real field schemas for all five resources, byte sizes and SHA-256 hashes.
- `CITATION.cff` — CFF 1.2.0, `type: dataset`, organizational author, concept and version DOIs.
- `LICENSE` — CC BY 4.0 full legal text.

### Notes on this release
- **DOI placeholders.** `CONCEPT_DOI_PLACEHOLDER` and `VERSION_DOI_PLACEHOLDER` appear in `README.md`, `CITATION.cff` and `datapackage.json`. Zenodo mints both DOIs only when the first tagged release is archived, so they are filled in immediately afterwards and shipped as `2026.10.1`. Anything citing `2026.10.0` should cite the concept DOI.
- **`self-exclusion-programs.csv` is not a 50-state census.** 11 jurisdictions verified. Absence of a state is absence of verification, not absence of a program. This is the largest open gap in the release.
- **`quit-gambling-apps.csv` is a panel, not a census.** The Apple search endpoint caps at 50 results per term. Every count derived from it is a floor.
- **No composite score anywhere**, and no ranking on the state-published layer, by design.
- **Betttr's own app is a row** in `quit-gambling-apps.csv`, classified by the same rule as every other app.

### Known issues carried into the next release
- Tier `U` rows in the Harm Index — states whose series exist but could not be retrieved (Arizona is the worked example: all AZ gaming hosts return 403 to automated fetch). First target of the November refresh.
- 25 unsourced glossary entries, 21 of them sports-betting jargon with no authoritative definitional body. Two clinical instruments (SOGS, Lie/Bet) need a primary-source pass and should not be cited from this file until they get one.
- Sportsbook RG Tools has no dated screenshots and no per-state parameter values; operators generally do not publish either.
- Self-exclusion durations and reinstatement rules are not yet captured.
