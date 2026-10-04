# Schema — `self-exclusion-programs.csv`

**Resource name:** `self-exclusion-programs`
**Rows:** 38 — 37 jurisdiction rows (36 states + DC) + 1 multi-state program (edition 2026.10.0 working copy; was 12 in 2026.9.x)
**Primary key:** `jurisdiction`
**Refresh cadence:** quarterly
**Encoding:** UTF-8, comma-delimited, header row

---

## What this file is

How to enroll in self-exclusion, by jurisdiction: the administering body, the enrollment method, the direct program URL, and the scope of what the exclusion actually covers — plus one row for the multi-state National Voluntary Self-Exclusion Program (NVSEP) and the states a single NVSEP enrollment reaches.

Self-exclusion is a request a person makes to a regulator or an operator to be barred from gambling. It is binding with that regulator or operator. No app enrolls anyone, and this file is a directory, not an enrollment path.

## Columns

| # | Column | Type | Notes |
|---|---|---|---|
| 1 | `jurisdiction` | string | State name, or the name of the multi-state program. Unique. |
| 2 | `jurisdiction_code` | string | Two-letter USPS code for a state row; `US` for the multi-state row. |
| 3 | `jurisdiction_type` | string | `state` · `multi-state`. |
| 4 | `administering_agency` | string | The regulator, department or operator that runs the program. |
| 5 | `enrollment_method` | string | Online · in person · notarized form by mail · a combination — in the program's own terms. |
| 6 | `program_url` | string (uri) | Direct enrollment or program page. **Empty where the program publishes no direct URL** — this is a real state of the world, not a missing value. |
| 7 | `notes` | string | Scope: which verticals the exclusion covers, and whether separate tracks must be enrolled in individually. |
| 8 | `participating_states` | string | Multi-state rows only: `; `-separated USPS codes the single enrollment reaches. Empty for state rows. |

## The multi-state row

One row, `jurisdiction_type = multi-state`: the **National Voluntary Self-Exclusion Program (NVSEP)**, operated by idPair — one enrollment plus one remote notary appointment, after which every participating state closes at once. `participating_states` lists the states it reaches as of this edition. A person in one of those states can use either NVSEP or their state's own program; the two are not equivalent in scope, and `notes` on the state row is where that difference lives.

## Scope is the whole story

Two enrollments called "self-exclusion" can cover completely different things. Pennsylvania runs **four separate tracks** — casinos, online gambling, video gaming terminals, and fantasy — and a person must enroll in each one they need. Michigan's Disassociated Persons List covers casinos while internet-gaming self-exclusion is a separate action. New Jersey lets the person choose online-only or all gambling.

Read column 7 before treating any two rows as comparable. There is no column that reduces scope to a flag, deliberately: any such flag would be wrong for about half the rows.

## Known gaps

1. **Now 37 jurisdiction rows (36 states + DC), from 11; with the 14 no-program states listed below, all 50 states and DC are classified.** Added 2026-10-03 from official regulator/lottery pages: AZ, CA (card rooms only), DC, DE, GA (lottery only), IA, KS, KY (statewide list, operator-level enrollment), LA, ME, MO, MS, MT (rule only, no public enrollment page), NC, NE and WY (via NVSEP), NH, NM, OK (nonprofit-administered casino list + Lottery), RI, SD, TN, VA, VT, WA, WV. States with **no statewide program** as of 2026-10-03, per their regulator or lottery pages: AK, AL, AR (statewide list authorized by Act 798 of 2025, rules still draft), FL (operator-level only), HI, ID, MN, ND, NV (operator registers only), OR (operator-level in the Lottery's DraftKings app), SC, TX, UT, WI. Where a field could not be confirmed on an official page it is marked UNVERIFIED inside `notes`. Absence of a state here still means absence of a *statewide* program, not that no operator offers exclusion.
2. **Enrollment methods change without notice** and several states are mid-migration from notarized paper to online portals. Quarterly refresh is the mitigation; each edition is dated.
3. **No enrollment volumes.** Counts of people enrolled live in `gambling-harm-index.csv`, where they are published at all, and are not comparable across states.
4. **Durations and reinstatement rules now live in `notes`** (added 2026-10-03) rather than in their own columns; a structured `durations` / `removal` pair is planned once every row has them verified.
5. **Reinstatement rules are in `notes` where verified**; several rows say UNVERIFIED.
6. **Operator-level self-exclusion is a different file.** For what each sportsbook offers inside its own product, and which operators accept a written request, see `sportsbook-rg-tools.csv` (columns 15–21).
7. **Empty `program_url` is meaningful.** Indiana, New York and Illinois rows carry no URL because the program does not publish a single stable enrollment page; `enrollment_method` and `notes` carry the path instead.

## Provenance

Betttr self-exclusion directory, 2026-Q3, compiled from state regulator and agency pages and the NVSEP program site. Published at https://betttr.net/self-exclusion/.

## Corrections

**support@betttr.net.** A wrong URL or a stale enrollment method in this file can send someone in a bad moment to a dead end, so corrections here are treated as urgent and shipped out of band rather than waiting for the quarterly edition. State agencies: we correct on your word plus a source.

If gambling is a problem for you or someone you know, the National Problem Gambling Helpline™ is **1-800-MY-RESET (1-800-697-3738)** — call or text, 24/7 — or chat at 1800myreset.org.
