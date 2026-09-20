# Schema — `recovery-glossary.csv`

**Resource name:** `recovery-glossary`
**Rows:** 125 terms
**Primary key:** `term` (`term_slug` is also unique and is the stable join key)
**Refresh cadence:** as needed; reviewed quarterly
**Encoding:** UTF-8, comma-delimited, header row

---

## What this file is

125 gambling-recovery and gambling-industry terms, each with a plain-English definition written at roughly an 8th-grade reading level, a stigma-preferred phrasing note where the common term carries stigma, and a source — or an explicit unsourced marker where no authoritative definitional source exists.

It is built for journalists, clinicians, researchers and product writers who need one defensible definition of a term like *chasing losses* or *self-exclusion*, and a defensible way to write about the people affected.

## Columns

| # | Column | Type | Notes |
|---|---|---|---|
| 1 | `term` | string | The term. In section D rows this is the **discouraged** term. Unique. |
| 2 | `preferred_term` | string | Section D only: the phrasing to use instead. Empty for sections A–C. |
| 3 | `section_letter` | string | `A` · `B` · `C` · `D`. |
| 4 | `section` | string | Human-readable section name. |
| 5 | `definition` | string | The definition. Markdown emphasis stripped; internal quotation marks preserved. Empty for most section D rows, where the row is guidance rather than a definition. |
| 6 | `preferred_phrasing_note` | string | What to say, what to avoid, and why. `safe to use as written` where the term carries no stigma. |
| 7 | `source_url` | string (uri) | First authoritative URL cited. Empty where unsourced. |
| 8 | `source_note` | string | The non-URL remainder of the source line, including the `[UNSOURCED — …]` marker and its stated reason. |
| 9 | `source_status` | string | `sourced` · `partial` · `unsourced` · `n/a - language pair`. |
| 10 | `term_slug` | string | Lowercase hyphenated slug, **stable across releases**, matching `https://betttr.net/glossary/<slug>/`. Use this as the join key, not `term`. |

## Sections

| Letter | Section | Terms |
|---|---|---|
| A | Recovery language | 39 |
| B | Industry and product terms | 41 |
| C | Regulators, programs, and clinical instruments | 23 |
| D | Stigma-preferred language pairs | 22 |

Section D rows have a different shape: `term` is what not to say, `preferred_term` is what to say instead, `preferred_phrasing_note` explains the harm in the discouraged phrasing, and `source_status` is `n/a - language pair` because these are editorial guidance, not defined terms. **Filter on `section_letter != 'D'` if you want definitions only.**

## Source status

| Value | Count | Meaning |
|---|---|---|
| `sourced` | 71 | An authoritative URL supports the definition. |
| `unsourced` | 25 | No authoritative definitional source was located. The definition reflects consistent common usage, and `source_note` says so explicitly. |
| `partial` | 7 | A source supports the harm framing or the underlying figures, but not the mechanical definition. |
| `n/a - language pair` | 22 | Section D. |

**32 of 125 entries carry a flag.** That is deliberate and it is published rather than hidden: sports-betting jargon has no authoritative definitional body, only consistent usage, and the honest move is to say so rather than attach a citation that does not support the sentence.

Source preference order used throughout: NCPG and state regulators (.org/.gov) → SAMHSA and APA → peer-reviewed literature → recognized recovery-language references such as the Recovery Research Institute's Addictionary. Where only a homepage is cited, that is deliberate — deep URLs are only cited where they have been opened and read.

## Known gaps

1. **21 of the 25 unsourced entries are in section B** (industry and product terms). Closing them is the first maintenance pass, and several may not be closable: there is no standards body that defines *tilt* or *reload bonus*.
2. **Two clinical instruments need a primary-source pass** — SOGS and Lie/Bet are widely described in the screening literature but no primary source was opened for this release. Both are marked `unsourced` with that reason in `source_note`. Do not cite this file as the authority for either instrument's properties.
3. **Derived-count discrepancy, stated plainly.** The prose source file counts *26 fully unsourced and 6 partial*. This CSV's rule-based classification yields *25 unsourced and 7 partial*, because one term (**hold**) carries both an `[UNSOURCED]` marker and a regulator URL, and the rule classifies any flagged entry with a URL as `partial`. The total flagged (32) agrees. Use `source_note` if you need the source file's own wording.
4. **Definitions are U.S.-centric.** Regulatory and program terms describe U.S. structures. A term like *self-exclusion* means something materially different in a jurisdiction with a national scheme.
5. **The helpline number in any downstream copy needs checking.** The National Problem Gambling Helpline™ is now **1-800-MY-RESET (1-800-697-3738)** — call or text, 24/7 — with chat at 1800myreset.org. 1-800-GAMBLER is operated independently of NCPG following a 2025 New Jersey ruling, and many state disclosure statutes still mandate it on operator advertising, so both numbers are in the wild and neither is "wrong." Only 1-800-MY-RESET is the NCPG National Problem Gambling Helpline™. Neither is a crisis line; for a crisis, 911 or 988.
6. **`definition` contains commas, quotation marks and em dashes.** Standard RFC 4180 quoting is used. Parse with a real CSV reader, not a split on commas.
7. **No term frequencies, no usage data.** This file says what words mean and which to prefer. It does not say how often they appear anywhere.

## Provenance

Compiled by Betttr LLC from the sources named per row. Each entry's source line is preserved across `source_url` and `source_note` without editorial smoothing.

## Corrections

**support@betttr.net.** Clinicians, regulators and people in recovery who think a definition or a preferred phrasing is wrong are the senders we most want to hear from. Corrections are dated on the page and in the next release.
