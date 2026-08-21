---
name: Highlights of the Day
description: Adds one unused GitHub Agentic Workflows FAQ highlight to the daily website update.
engine: copilot
on:
  schedule:
    - cron: "0 */6 * * *" # every six hours, UTC
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# Highlights of the Day

Add one unused GitHub Agentic Workflows FAQ highlight to the website's `Daily Updates` section.

## Task

1. Determine the workflow run date with `date -u +%Y-%m-%d`. Use that UTC date for every decision and for the update.
2. Read `index.html` and inspect all existing `Daily Updates` navigation controls and dialogs before editing.
3. Fetch the GitHub Agentic Workflows FAQ from https://github.github.com/gh-aw/reference/faq/ using `web-fetch`.
4. Select exactly one FAQ question that is not already represented in `index.html`. Treat a question as represented if the same FAQ question or its clear subject is already present in any existing update. If every FAQ is already represented, make no change and call the `noop` safe output.
5. Check whether the UTC date already has a daily update dialog. If that dialog already contains an FAQ, make no change and call `noop`. If it is a placeholder dialog, reuse it. Otherwise, add one matching navigation control and dialog.
6. Add the selected FAQ question and a concise, accurate answer to the date's dialog. Preserve every existing update and do not duplicate any date, navigation control, dialog, or FAQ.
7. Match the existing HTML structure, ID conventions, date wording, and styling. Use date wording such as `21st of August`, a lowercase date-based dialog ID such as `august-21-dialog`, and matching `aria-controls`, `aria-labelledby`, and `aria-describedby` references. Keep the dialog accessible.
8. Verify that exactly one dialog contains the selected FAQ, that the run date occurs only once in the navigation and dialog structure, that no existing update was altered, and that only `index.html` changed.
9. If a change was made, request one pull request with the `create-pull-request` safe output. If no change was needed, call `noop` instead.