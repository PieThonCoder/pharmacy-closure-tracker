# Pharmacy Closure Tracker

**Live site:** https://pietoncoder.github.io/pharmacy-closure-tracker/

State pharmacy boards publish today's license roster and delete yesterday's. When a pharmacy closes,
most boards never mark it closed — the license simply stops appearing, and downstream registries
(NPPES, NCPDP-derived files) keep listing it as active. This project snapshots the public rosters of
11 states + DC (Texas daily, the rest weekly) and publishes what changed each week: new licenses,
removals (including removals while listed *Active*), status and name changes, keyed by the board's
own license number, with a live cross-check against the NPI registry.

This repository holds the generated site. It is rebuilt automatically after each capture run.

## Data

- `data/week-<from>-<to>.csv` — this window's event-level change log
- `data/since-2026-08-08.csv` — cumulative event-level change log
- `data/latest.json` — machine-readable summary (totals, per-state, removed-while-Active rows with NPPES status)
- `feed.xml` — RSS of weekly updates

Weekly change logs are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
Cite as: *Pharmacy Closure Tracker, https://pietoncoder.github.io/pharmacy-closure-tracker/, retrieved YYYY-MM-DD*.

The full daily/weekly snapshot archive, entity-resolved events across all recorded states, and the
reconstructed 2014–2026 Texas panel are available for research collaboration and licensing —
[open a data request](https://github.com/PieThonCoder/pharmacy-closure-tracker/issues/new?title=Data%20request).

## Method (short)

Removal = license number present in the previous roster, absent now. "Removed while Active" = its last
published status was Active/Current. Renewal re-listings (an appearance whose original issue date predates the
earlier snapshot by >90 days) are excluded. A removal whose street address reappears among the same window's
new licenses is flagged as a probable ownership change/relocation. Nonresident (out-of-state shipper) licenses
are flagged and excluded from the headline count. Removal is not proof of closure — confirm before relying on any single row.
