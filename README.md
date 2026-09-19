# race-sheets

Race start-list spreadsheets for ICF canoe slalom World Cups (WC) and World Championships (WCH), compiled from public ICF data by Race Desk and downloaded by the PaddleTagger photo-tagging app. Anyone may download; nothing here needs a login.

## Layout

```
index.json                              # every event: key, dates, grade, paths, updated_at
events/{Venue}_{Year}_{Kind}/
  {Venue}_{Year}_{Kind}_start.xlsx      # absent when the grade is FAIL
  manifest.json                         # grade, reason_code, dates, format, hashes, updated_at
```

- `Kind` is `WC` or `WCH`.
- **Each `manifest.json` is authoritative; `index.json` is a cache**, regenerated on every publish. Where they disagree, the manifest wins.
- A sheet is **updated in place**: the results pass stamps `Rank` on the Final and Teams rows of the same file, and `updated_at` changes. No versioned copies under new names.
- A failed compilation still publishes its `manifest.json`, with `grade: "FAIL"` and a `reason_code`, and no spreadsheet — so a bad sheet can never be used for tagging.
