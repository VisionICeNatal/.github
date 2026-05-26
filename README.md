# VisionICeNatal/.github

Org-wide GitHub configuration for the [VisionICeNatal](https://github.com/VisionICeNatal) organization. **No project code lives here** — only metadata that GitHub picks up automatically and applies across every repo in the org.

## Contents

| Path | What it does | GitHub docs |
|---|---|---|
| [`profile/README.md`](./profile/README.md) | Renders on the org's public landing page at https://github.com/VisionICeNatal | [Customizing your organization's profile](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/customizing-your-organizations-profile) |

That's everything that's here today. The sections below list other files GitHub will pick up *from this same repo* if and when we add them — none are required.

## Reserved paths

If we add the files below, GitHub applies them as **org-wide defaults**; any repo that ships its own copy of the same file overrides the default for that one repo.

| Path | Purpose |
|---|---|
| `FUNDING.yml` | Default "Sponsor" button links |
| `ISSUE_TEMPLATE/*.md` (or `*.yml`) | Default issue templates |
| `PULL_REQUEST_TEMPLATE.md` | Default PR template |
| `dependabot.yml` | Default Dependabot config |
| `CODE_OF_CONDUCT.md`, `SECURITY.md`, `SUPPORT.md`, `CONTRIBUTING.md` | Community health files used as defaults |

Reference: [Creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).

## Editing notes

- **This README** is what you're reading; it only renders when you visit `VisionICeNatal/.github` directly. The org's *public* landing page uses [`profile/README.md`](./profile/README.md).
- This repo must be **public** for GitHub to render `profile/README.md` on the org page — even though every other VisionICeNatal repo can stay private. Public visibility here does not expose any private content; this repo only holds metadata.
- Changes propagate within ~30 seconds of pushing; hard-refresh the org page if you don't see them. Per-repo overrides take precedence the moment they appear in that repo's default branch.
- File paths and filenames are **case-sensitive**. `Profile/README.md` or `README.MD` will silently fail to render. When in doubt, copy the exact path from this table.

## License

Configuration content here (templates, prose) is published under **CC0-1.0** — these files are boilerplate and should be free to copy into any project. The Python packages this org maintains are under their own licenses (currently all AGPL-3.0-only — see each repo's `LICENSE` file).
