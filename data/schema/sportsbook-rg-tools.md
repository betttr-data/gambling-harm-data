# Schema — `sportsbook-rg-tools.csv`

**Resource name:** `sportsbook-rg-tools`
**Rows:** 14, one per operator
**Primary key:** `operator`
**Refresh cadence:** quarterly (2026-Q3 is the first edition)
**Encoding:** UTF-8, comma-delimited, header row

---

## What this file is

For every operator in the set, which responsible-gambling tools the operator **publishes**: deposit, loss, wager and time limits; cool-off and timeout; in-product self-exclusion; whether a written self-exclusion request is accepted; the account-closure path; and the documented navigation to reach any of it.

Every substantive claim has a source column next to it holding one or more operator-published URLs, `|`-separated.

## The central design decision: "not published" is data

Most cells that look empty are not missing — they say **`not published`**, and that is the finding. An operator that documents a cool-off mechanic but never states the durations offered has published an incomplete control, and this file records exactly that rather than guessing a plausible value or leaving a blank that a reader will mistake for "no tool."

Three distinct states, kept apart:

| Value | Meaning |
|---|---|
| `Y` / `N` | The tool is published as existing / is not published as existing. |
| `not published` | The operator documents the mechanic but not this parameter. |
| *(empty)* | Not applicable to this row — e.g. `written_self_exclusion_address` for an operator that does not accept written requests. |

Several cells carry a qualified `Y` with prose, e.g. `Y (both). Loss limit: ... Wager limit: ...`. Parse the leading token, read the prose.

## Column groups

The 28 columns run in claim/source pairs. The pattern is: the claim column, any parameter columns, then a `*_source` column carrying the URLs.

### Identity (1–3)

| # | Column | Notes |
|---|---|---|
| 1 | `operator` | Consumer-facing brand. Unique; the primary key. |
| 2 | `parent_company` | Corporate parent as publicly stated. |
| 3 | `product_type` | Which products the brand operates (sportsbook, casino, DFS, racing, poker, predictions). |

### Deposit limits (4–7)

| # | Column | Notes |
|---|---|---|
| 4 | `deposit_limit` | `Y` / `N` / qualified string. |
| 5 | `deposit_limit_periods` | Periods offered (daily / weekly / monthly) and the scope the limit applies across. |
| 6 | `deposit_increase_delay` | **The friction column.** What happens when a user *raises* a limit: cooling-off mechanic, waiting period, confirmation step. Frequently `not published` — no operator in this set publishes its per-state waiting-period values. |
| 7 | `deposit_limit_source` | Operator URLs, `|`-separated. |

### Loss and wager limits (8–9)

| # | Column | Notes |
|---|---|---|
| 8 | `loss_or_wager_limit` | Whether a loss limit, a wager (spend) limit, or both. The distinction matters: a loss limit blocks on net losses, a wager limit blocks on amount staked. |
| 9 | `loss_or_wager_limit_source` | Operator URLs. |

### Time limits and reality checks (10–11)

| # | Column | Notes |
|---|---|---|
| 10 | `time_session_limit_or_reality_check` | Time limit, session limit, or reality-check pop-up, and what it does. A **time limit** blocks; a **reality check** only interrupts. Read the prose — they are not the same control. |
| 11 | `time_session_source` | Operator URLs. |

### Cool-off / timeout (12–14)

| # | Column | Notes |
|---|---|---|
| 12 | `cooloff_timeout` | A short-term break, distinct from self-exclusion. |
| 13 | `cooloff_durations` | The duration menu. Often `not published`. |
| 14 | `cooloff_source` | Operator URLs. |

### Self-exclusion, in-product (15–18)

| # | Column | Notes |
|---|---|---|
| 15 | `self_exclusion_in_app` | Whether self-exclusion can be started inside the operator's own product. |
| 16 | `self_exclusion_durations` | Duration menu as published. Frequently `not published` or a vague ceiling such as "up to 5 years". |
| 17 | `self_exclusion_reversible` | Whether the operator states the exclusion can be lifted before the term ends, and which products it covers. |
| 18 | `self_exclusion_source` | Operator URLs. |

### Written self-exclusion (19–21)

| # | Column | Notes |
|---|---|---|
| 19 | `accepts_written_self_exclusion_email` | `Y` / `N`. |
| 20 | `written_self_exclusion_address` | The email address requests are accepted at. Empty where `N`. |
| 21 | `written_self_exclusion_source` | **Provenance differs from the rest of the file:** these two columns come from the Betttr self-exclusion directory, not from an operator help page, because operators do not generally publish this. Treated as a lower evidence tier and labelled as such in every row. |

### Account closure (22–23)

| # | Column | Notes |
|---|---|---|
| 22 | `account_closure_path` | How a user closes an account **as distinct from self-excluding**, and whether that path is self-serve. Several operators route "Close Account" into the self-exclusion flow; where that is the case, the cell says so. |
| 23 | `account_closure_source` | Operator URLs. |

### Discoverability (24–27)

| # | Column | Notes |
|---|---|---|
| 24 | `rg_tools_nav_path` | The documented tap path to the controls inside the product. `not published` is common and is itself the finding. |
| 25 | `rg_nav_source` | Operator URLs. |
| 26 | `rg_page_url` | The operator's public responsible-gambling hub. `|`-separated where more than one exists. Note that a public marketing RG site is **not** the in-product control; where the two differ, `notes` says so. |
| 27 | `rg_page_date_visible` | Whether the RG page carries a last-modified or version date. Usually `not published` — which is why this file is dated and versioned instead. |

### Notes (28)

| # | Column | Notes |
|---|---|---|
| 28 | `notes` | What stands out about this operator relative to the rest of the set, and what could not be verified. |

## Known gaps

1. **14 operators, not a census.** The set is the largest U.S. operators by visibility, not every licensed operator. Sweepstakes and social-casino operators are under-covered in this first edition.
2. **Everything here is *published* behaviour, not *observed* behaviour.** No row asserts what a control actually does in a live account. Tap-depth, which was the original ambition, is only recorded where the operator documents it — nobody in this set documents the path to deposit/loss/time limits from the app's main nav.
3. **No dated screenshots in this release.** The quarterly design calls for a dated screenshot per control so that changes are visible over time ("operator moved self-exclusion two taps deeper in Q3"). That requires accounts on each book. The first edition is documentation-only; screenshots are the planned Q4 addition, with a verification layer — never unverified crowdsourcing.
4. **Per-state variation is largely invisible.** Limits, durations and available tools vary by state licence, and operators generally do not publish the per-state values. Where an operator says a parameter "depends on where you live," the cell records that phrase rather than a number.
5. **Source pages are undated.** Almost no operator RG or help page carries a last-modified date (`rg_page_date_visible`), so a claim can go stale without any visible signal at the source. This is the reason the file is versioned quarterly and every edition is kept.
6. **Columns 19–21 are a different evidence tier** — see above.
7. **`Y` is not a quality judgement.** A published tool may be hard to find, easy to raise, or narrow in scope. That is what columns 6, 16, 17 and 24 are for. Do not aggregate the `Y` counts into a score; this file deliberately ships no score.

## Provenance

Operator-published help centres, responsible-gambling hubs and support articles, retrieved 2026-Q3. Every claim column has a matching `*_source` column. Nothing is sourced to a news article, a review site, or an affiliate.

## Corrections

**support@betttr.net.** Operators who believe a row misstates their product are the most valuable senders; we correct on their word plus a published URL. Corrections are appended and dated, never silently substituted, and the prior edition stays live at its own URL.
