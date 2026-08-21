---
name: New Day
description: Add the workflow run's UTC date to the Daily Updates navigation and matching dialog in index.html.
engine: copilot
strict: true
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
    if-no-changes: ignore
env:
  WORKFLOW_RUN_STARTED_AT_UTC: ${{ github.run_started_at }}
---

# New Day

Update `index.html` for the workflow run's UTC date only.

Use `WORKFLOW_RUN_STARTED_AT_UTC` as the source timestamp. Derive the UTC calendar date from that timestamp and use the existing page's date wording style for visible text, matching the current `1st of August` format exactly.

Follow the existing HTML structure, accessibility attributes, dialog pattern, ID conventions, and styling hooks already present in `index.html`.

Requirements:

- modify only `index.html`
- do not modify `styles.css`
- preserve every existing daily update, navigation control, and dialog
- add one new `Daily Updates` navigation button for the UTC date if it is not already present
- add one matching accessible `<dialog>` for that same date if it is not already present
- keep IDs consistent with the existing convention, matching the new date
- the new dialog must clearly confirm that the daily update ran for that UTC date
- do not duplicate an existing date, navigation control, or dialog

If the UTC date is already represented in the existing `Daily Updates` navigation or dialogs, make no file changes and finish without creating a duplicate.
