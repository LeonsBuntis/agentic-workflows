---
name: Weekly Report Status
description: Publishes a weekly activity report covering commits, issues, and pull requests from the previous 7 days.
engine: copilot
on:
  schedule:
    - cron: "0 9 * * 1" # weekly, Monday 09:00 UTC
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Generate a concise activity report for this repository covering the **previous 7 full days ending at run start (UTC)**.

## Task

1. Determine the reporting window: the 7 days immediately preceding this run.
2. Using `gh` commands, gather activity within that window:
   - **Commits**: commits pushed to the default branch.
   - **Issues**: issues opened and closed.
   - **Pull requests**: pull requests opened, merged, and closed.
3. Summarize the findings in a concise, well-organized report using GitHub-flavored markdown, with a section for each category (`### Commits`, `### Issues`, `### Pull Requests`).
4. For each category with no activity in the window, clearly state that no activity occurred (for example, "No commits were pushed in this period.").
5. Publish the report as a new issue via the `create-issue` safe output. Include the reporting window (start and end dates) in the issue body.
6. If there is no activity at all across commits, issues, and pull requests for the window, still create the issue and clearly state that no activity occurred during the period — do not skip publishing.

Keep the report factual and concise; avoid speculation beyond what the gathered data shows.
