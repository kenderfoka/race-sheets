# race-sheets

Race spreadsheets for ICF canoe and kayak events — slalom and wildwater, sprint and paracanoe, marathon and ocean racing, 2009 to 2026 — compiled from public results by the race-desk Bots and downloaded by the PaddleTagger photo-tagging app, which finds an event by its photos' dates. Anyone may download; nothing here needs a login.

## Layout

```
index.json                              # every event: key, venue, kind, dates, grade, paths, updated_at
events/{Venue}_{Year}_{Suffix}/
  {Venue}_{Year}_{Suffix}_start.xlsx    # a whitewater sheet (slalom, wildwater)
  {Venue}_{Year}_{Suffix}_Results.xlsx  # a flatwater sheet (sprint and paracanoe, marathon, ocean)
  manifest.json                         # grade, reason_code, gaps, dates, discipline, start_times, hashes, updated_at
```

- **The key names the folder and the file, nothing more.** The competition is the manifest's `kind`: `WC`, `WCH`, `JWCH`, `WWC`, `OG`, `ECH`, `PG`, `TWG` and `MAR` today. A key's suffix can differ from it: `Moscow_2021_MAR` is an `ECH`, `Madeira_2024_COR` a `WCH`.
- **Each `manifest.json` is authoritative; `index.json` is a cache**, regenerated on every publish. Where they disagree, the manifest wins.
- **Grades:** `PERFECT`, `USABLE` (a sheet with declared gaps, listed in `gaps`) or `FAIL`. A failed compilation still publishes its `manifest.json`, with `grade: "FAIL"` and a `reason_code`, and no spreadsheet — so a bad sheet can never be used for tagging.
- A sheet is **updated in place**: a later pass (results, ranks, ids) rewrites the same file, and `updated_at` changes. No versioned copies under new names.

## How sheets arrive

- **Current-season events** are published to `main` by the live desks' evening runs.
- **Historic events (2008–2025)** arrive as pull requests from the Labs, are checked independently by a Claude check, and are merged only when the sheet passes. A question neither side can settle waits for the maintainer under the label `needs-ruling`.
