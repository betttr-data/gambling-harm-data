# Gambling Harm Open Data

[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.22857767-blue)](https://doi.org/10.5281/zenodo.22857767)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey)](https://creativecommons.org/licenses/by/4.0/)
[![Data Package](https://img.shields.io/badge/Frictionless-datapackage.json-green)](datapackage.json)

Five machine-readable datasets on gambling harm and gambling recovery in the United States, published together, refreshed on a stated clock, free, with no registration and no rate limit.

**Landing page:** https://betttr.net/data/
**Current release:** `2026.9.1` — 23 September 2026 (corrections to OH, MD, VA rows; see CHANGELOG)
**Contact and corrections:** support@betttr.net

Every source this project draws on is a PDF. If this were also a PDF it would have added nothing. The CSV is the point.

---

## What's in it

| File | Rows | What it is | Refresh |
|---|---|---|---|
| [`data/gambling-harm-index.csv`](data/gambling-harm-index.csv) | 51 | What every U.S. state and DC publishes about gambling harm, plus the one genuinely comparable 51-jurisdiction series that exists — NCPG helpline contacts and rate per 100k. | **Monthly**, the 15th, 9:00 a.m. ET |
| [`data/sportsbook-rg-tools.csv`](data/sportsbook-rg-tools.csv) | 14 | Which responsible-gambling tools each major U.S. sportsbook and DFS operator publishes — limits, cool-off, self-exclusion, closure path, and the navigation to reach them. Every claim carries the operator URL it came from. | **Quarterly** |
| [`data/recovery-glossary.csv`](data/recovery-glossary.csv) | 125 | Gambling-recovery and gambling-industry terms with a plain definition, a stigma-preferred phrasing, and a source or an explicit unsourced marker. | **As needed**, reviewed quarterly |
| [`data/quit-gambling-apps.csv`](data/quit-gambling-apps.csv) | 107 | A dated panel of quit-gambling apps on the U.S. iOS App Store — release and update dates, rating counts, classification. | **Monthly**, with the Index |
| [`data/self-exclusion-programs.csv`](data/self-exclusion-programs.csv) | 12 | How to enroll in self-exclusion by jurisdiction, plus the multi-state NVSEP and the states it reaches. | **Quarterly** |

Each file has a plain-language column dictionary in [`data/schema/`](data/schema/) documenting every column, its units, its missing-value markers, and its known gaps. Machine-readable field schemas for all five are in [`datapackage.json`](datapackage.json) ([Frictionless Data Package v2](https://datapackage.org/)).

### Stable raw URLs

```
https://raw.githubusercontent.com/betttr-data/gambling-harm-data/main/data/gambling-harm-index.csv
https://raw.githubusercontent.com/betttr-data/gambling-harm-data/main/data/sportsbook-rg-tools.csv
https://raw.githubusercontent.com/betttr-data/gambling-harm-data/main/data/recovery-glossary.csv
https://raw.githubusercontent.com/betttr-data/gambling-harm-data/main/data/quit-gambling-apps.csv
https://raw.githubusercontent.com/betttr-data/gambling-harm-data/main/data/self-exclusion-programs.csv
```

`main` always points at the newest release. For a frozen copy, use a tag: replace `main` with `v2026.9.1`, or cite the version DOI.

---

## How to cite

**APA 7**

> Betttr LLC. (2026). *Gambling Harm Open Data* (Version 2026.9.1) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.22908453

To cite the dataset in general rather than one release, use the concept DOI, which always resolves to the latest version:

> Betttr LLC. (2026). *Gambling Harm Open Data* [Data set]. Zenodo. https://doi.org/10.5281/zenodo.22857767

**BibTeX**

```bibtex
@dataset{betttr_gambling_harm_open_data_2026,
  author    = {{Betttr LLC}},
  title     = {Gambling Harm Open Data},
  year      = {2026},
  month     = {10},
  publisher = {Zenodo},
  version   = {2026.9.1},
  doi       = {10.5281/zenodo.22908453},
  url       = {https://doi.org/10.5281/zenodo.22908453}
}
```

**Citing one file.** Name it, so a reader can find the same numbers:

> Betttr LLC. (2026). Gambling Harm Index [Data file]. In *Gambling Harm Open Data* (Version 2026.9.0). Zenodo. https://doi.org/10.5281/zenodo.22857768

**In a news story,** this is enough: *Gambling Harm Open Data, Betttr LLC, September 2026* — with a link to https://betttr.net/data/. Journalists do not need to ask permission, and do not need to email us first.

GitHub's "Cite this repository" button reads [`CITATION.cff`](CITATION.cff) and will generate both formats for you.

---

## License

**[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)** — full text in [`LICENSE`](LICENSE). SPDX: `CC-BY-4.0`.

Free to use, including commercially, including in a product, including by a competitor. The only condition is credit and a link.

**Why this license.** Most of what is in these files is factual data, and in the United States facts are not copyrightable — so a data license here is closer to a norm and a courtesy than an enforceable claim. Given that, we picked the option that every reuser, repository and journal data policy already recognizes without needing a paragraph of explanation, and that covers the contents of the tables rather than only their structure. We want the data used. Credit is the point, and credit comes from the DOI and the citation block above far more than from the license text. If attribution is inconvenient for you, take the data anyway and cite us when you can.

---

## Provenance

| Dataset | Primary sources |
|---|---|
| Gambling Harm Index | NCPG's annual National Problem Gambling Helpline report, Appendix A (prepared by the Omni Institute) for the helpline layer — one publisher, one method, all 51 jurisdictions. State gaming regulators, lotteries, behavioral-health agencies and state councils for the state layer, with a per-row URL in `state_source_url`. |
| Sportsbook RG Tools | Operator-published help centres and responsible-gambling hubs, retrieved 2026-Q3. Every claim column has a matching `*_source` column. |
| Recovery Glossary | NCPG and state regulators → SAMHSA and APA → peer-reviewed literature → recognized recovery-language references. Per-row in `source_url`. |
| Quit-Gambling Apps | Apple iTunes Search API, U.S. iOS App Store, pulled 2026-09-20. |
| Self-Exclusion Programs | State regulator and agency pages, plus the NVSEP program site. |

**Rules we hold ourselves to:**

- **No estimating, modelling, imputing or interpolating.** Every number is a published number with a URL.
- **No composite score.** There is no single "harm number" for a state and there will not be one, because the inputs are not comparable enough to earn it.
- **No ranking on figures that are not comparable.** The state-published layer is never ranked.
- **No news articles as sources.** Press-only figures with no primary source are excluded from the published-value columns entirely. We do not launder an article into a dataset.
- **Missing means missing, and says which kind.** `N/A` never means zero and never means we did not look. Each file documents its markers in `data/schema/`.

---

## Funding

**Produced by Betttr LLC, maker of a recovery app; no operator or affiliate money.**

Betttr LLC is a Delaware limited liability company based in Sherman Oaks, California. Its revenue comes from people who use its app, and from nothing else. It has never accepted money, sponsorship, data, advertising, placement or in-kind support from a sportsbook, a casino, a lottery, a gambling operator, an affiliate marketer, a gambling trade association, or anyone acting for them, and it will not. If that ever changes it will be disclosed here and on https://betttr.net/data/ before the next release, and the change will be dated.

**We are in our own data.** The Betttr app is a row in `quit-gambling-apps.csv`, counted by the same rule as every other app, with no adjustment and no favorable placement. Any analysis of that file that ranks apps should say the publisher is in the ranking.

We have a stake in gambling harm being taken seriously. That is a reason to check our arithmetic, and it is why every number here carries the URL it came from.

---

## Corrections policy

Releases are permanent and are never silently edited.

- **Corrections are appended, not substituted.** A corrected release keeps the original value recoverable through the prior tag and the prior version DOI, and carries a dated note naming what changed and why.
- **Every correction appears in [`CHANGELOG.md`](CHANGELOG.md)**, newest first, with the release it affects, and in the running log at https://betttr.net/harm-index/corrections/.
- **Material corrections are flagged at the top of the affected release** and in the next release's notes.
- **Anyone can send one**, to **support@betttr.net**. State agencies, councils, regulators and operators who believe we have their number, scope or period wrong are the most valuable senders, and we correct on their word plus a source.
- **We publish corrections we find ourselves** the same way we publish corrections we are sent.
- **If a figure turns out to be unsupportable** rather than merely wrong, we remove it and say that we removed it. We would rather have a hole with an explanation than a number we cannot stand behind.
- **`self-exclusion-programs.csv` corrections ship out of band.** A dead enrollment URL can send someone in a bad moment to a dead end; those do not wait for the quarterly release.

A method change is dated, listed, and **never applied retroactively to a published release**.

---

## Refresh cadence

| Dataset | Cadence | When |
|---|---|---|
| Gambling Harm Index | Monthly | The 15th, 9:00 a.m. ET |
| Quit-Gambling Apps | Monthly | With the Index |
| Sportsbook RG Tools | Quarterly | First Index of the quarter |
| Self-Exclusion Programs | Quarterly | First Index of the quarter |
| Recovery Glossary | As needed | Reviewed quarterly |

A monthly clock does not mean monthly data. Most underlying sources are annual. Each monthly release records what was newly published in the preceding month, restates the standing figures, and notes what changed. **In a month where nothing new is published anywhere, the release says that** — and that is a real finding about the state of the field.

Every release is tagged (`v2026.9.0`), archived on Zenodo, and gets its own version DOI. Nothing is overwritten.

---

## Contributing

- **Corrections and source tips:** email **support@betttr.net**, or open an issue. A source URL makes it fast.
- **A state we've missed:** the biggest open gap is `self-exclusion-programs.csv`, which covers 11 jurisdictions and should cover all of them. Issues with a regulator URL are very welcome.
- **Pull requests to `data/*.csv` are not merged.** The files are generated from a sourcing process, not edited by hand; a PR would be overwritten at the next release. Send the correction instead and it will land in the next tagged version with your credit in the changelog if you want it.

---

## If gambling is a problem for you

The National Problem Gambling Helpline™ is **1-800-MY-RESET** (dial **1-800-697-3738**) — call or text, 24/7, free and confidential — or chat at [1800myreset.org](https://www.1800myreset.org).

It is not a crisis line. For a crisis, call **911 or 988**.

---

## Changelog

See [`CHANGELOG.md`](CHANGELOG.md).

| Version | Date | Summary |
|---|---|---|
| `2026.9.0` | 2026-09-21 | First public release. Five datasets, 309 rows, Frictionless descriptor, Zenodo DOI. |
