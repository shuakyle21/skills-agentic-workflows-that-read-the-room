---
name: update-github-info
description: Draft concise GitHub Info website updates from Mona's notes, the GitHub Blog, and the GitHub Changelog.
on:
  workflow_dispatch:
  schedule:
    - cron: 'daily'
permissions:
  contents: read
  pull-requests: read
tools:
  edit:
  web-fetch:
resources:
  - https://awesome-copilot.github.com/workflows/
safe-outputs:
  create-pull-request:
    title-prefix: '[mona] '
    draft: true
    fallback-as-issue: false
network:
  allowed:
    - github.com
    - github.blog
    - awesome-copilot.github.com
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` before making any changes.

Use these sources:
- `notes/mona-notes.md`
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/
- Awesome Copilot workflows: https://awesome-copilot.github.com/workflows/

Use the `web-fetch` tool to fetch https://awesome-copilot.github.com/workflows/ and add its findings to the `sources` list when looking for new workflow ideas or examples.

Update `site/content/github-info.md` with concise, practical updates for readers.
When a change comes from the GitHub Blog or GitHub Changelog, mention the source clearly in the content.

Use the configured `edit` tool to prepare the website content update, then rely on `safe-outputs: create-pull-request` so the agent proposes the change without writing directly to `main`.

Open a pull request for Mona to review, and make sure the pull request title clearly references Mona or GitHub Info.

If there is no useful update to publish, call `noop` with a short reason instead of making a change.