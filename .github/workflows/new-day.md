---
name: New Day
description: Adds a dated daily update and confirmation dialog to the website.
engine: copilot
on:
  schedule:
    - cron: "0 0 * * *" # daily, midnight UTC
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit:
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

Update the website for the current UTC date.

## Task

1. Determine the workflow run date with `date -u +%Y-%m-%d`. Use that UTC date
   for every decision and for the new update.
2. Read `index.html` and inspect the existing `Daily Updates` navigation and
   daily-update dialogs before editing.
3. If the UTC date is already represented anywhere in the existing daily
   updates, make no change and finish with a `noop` safe output.
4. Otherwise, add one navigation control to the existing `Daily Updates`
   navigation and one matching dialog. Preserve every existing daily update.
5. Follow the existing HTML structure, ID conventions, date wording, and
   styling. Use the established date wording such as `1st of August`, a
   matching lowercase date-based dialog ID such as `august-1-dialog`, and the
   corresponding `aria-controls`, `aria-labelledby`, and `aria-describedby`
   references. The dialog must be accessible and confirm that the daily update
   ran for the UTC date.
6. Before finishing, verify that there is exactly one new date, navigation
   control, and dialog for this run, that no existing update was altered or
   duplicated, and that only `index.html` changed. Never modify `styles.css`.
7. If a change was made, request one pull request with the `create-pull-request`
   safe output. If no change was needed, use `noop` instead.