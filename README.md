# LinkedIn Lead Pipeline

A Codex skill collection for a careful, checkpointed LinkedIn lead workflow:

1. Extract leads from an open, signed-in Sales Navigator people search.
2. Verify existing public LinkedIn profile URLs against the lead record.
3. Find or repair a URL only when the public evidence is strong enough.

The pipeline is designed for accuracy and recoverability. A blank URL is preferred to a plausible but unverified match.

## Workflow

| Phase | Purpose | Output |
| --- | --- | --- |
| Extract | Collect lead rows from a live Sales Navigator search, page by page | Checkpoints and a clean workbook |
| Verify | Audit existing public profile URLs against name, company, and role | Verified, unverified, broken, and review outcomes |
| Discover or repair | Research only the requested missing or broken URLs | Confident public `/in/` URLs, with unresolved rows left blank |

Each phase has its own checkpoint or audit state. Finishing one phase does not imply that another is complete.

## Included skills

- [Sales Navigator extraction](./skills/linkedin-sales-nav-leads): extracts a user-authorized, open Sales Navigator search without changing its filters.
- [LinkedIn URL verification](./skills/linkedin-lead-verification): audits existing URLs in a workbook without guessing replacements.
- [Public profile discovery](./skills/finding-linkedin-id): finds direct public profile URLs for explicitly requested rows, using an evidence gate.

## Install

Clone with submodules so all three skills are available:

```bash
git clone --recurse-submodules https://github.com/alimoizuddin/linkedin-lead-pipeline.git
```

Use the root `SKILL.md` for the full pipeline, or load only the specific skill needed for an individual phase.

## Operating rules

- The user's workbook and existing lead fields remain the source of truth.
- Sales Navigator extraction requires the user's live signed-in search and explicit authorization to collect.
- Only observed, public person-profile `/in/` URLs are accepted for final deliverables.
- The workflow never constructs profile slugs, sends messages, connects with people, saves leads, or changes LinkedIn settings.
- If LinkedIn throttles, restricts, or blocks the session, progress is saved and the run stops at the recorded resume point.
- Spreadsheet edits require authorization and are limited to the requested cells. Unrelated sheets, formulas, formatting, hyperlinks, and row order are preserved.

Use the workflow only in ways that comply with LinkedIn's terms, applicable law, and your organization's policies.

## Repository layout

```text
SKILL.md                         # Parent workflow and cross-phase rules
agents/openai.yaml               # Codex display metadata
skills/
  linkedin-sales-nav-leads/      # Sales Navigator extraction submodule
  linkedin-lead-verification/    # Existing URL verification submodule
  finding-linkedin-id/           # Public URL discovery submodule
```

The repository intentionally contains no lead lists, browser sessions, checkpoints, credentials, or private research material.

## License

Released under the [MIT License](LICENSE).
