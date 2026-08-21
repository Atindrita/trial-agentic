---
name: Weekly Report Status
description: Generate a concise weekly activity report for the previous seven days and publish it as an issue.
engine: copilot
strict: true
on:
  schedule:
    - cron: "0 9 * * 1"
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

Produce a concise GitHub activity report covering the previous seven days ending at workflow start time.

Read repository activity for:

- commits pushed in the last seven days
- issues created, updated, or closed in the last seven days
- pull requests opened, updated, merged, or closed in the last seven days

Create exactly one new issue containing:

### Overview

A short summary of overall activity for the window.

### Activity

- commits: concise count and notable highlights
- issues: concise count and notable highlights
- pull requests: concise count and notable highlights

### No Activity

If there was no activity in any category, say so clearly. If only some categories had no activity, state that explicitly for those categories.

Keep the report brief, factual, and easy to scan. Do not mention work outside the previous seven days.
