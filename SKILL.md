---
name: linkedin-lead-pipeline
description: "Run a two-stage lead pipeline: extract visible Sales Navigator results, then find and verify public LinkedIn URLs through Google without opening profiles. Use for lead spreadsheets, not outreach."
---

# LinkedIn Lead Pipeline

Use this as the parent workflow for lead-list collection and public-URL discovery. The two primary micro-skills remain independent submodules under `skills/`; load only the one needed for the user’s requested phase.

## Choose The Phase

1. **Extract Sales Navigator leads**: the user has an open, signed-in Sales Navigator people search and wants a sheet with `Name`, `Position`, `Company`, and `LinkedIn URL`. Read [Sales Navigator extraction](skills/linkedin-sales-nav-leads/SKILL.md). The URL is discovered through Google without opening profiles.
2. **Find or verify public URLs through Google**: a lead sheet already has names, positions, and companies, and the user wants public LinkedIn URLs found or checked without touching LinkedIn. Read [Google-only URL discovery](skills/finding-linkedin-id/SKILL.md).
3. **Full pipeline**: extract the result cards first, then run Google-only URL discovery. Do not begin URL discovery until the extraction checkpoint or workbook is saved and verified.

The existing [LinkedIn lead verification](skills/linkedin-lead-verification/SKILL.md) is retained only for an explicitly requested, read-only audit of links that already exist. It is not part of the default two-stage workflow.

## Shared Rules

- Preserve the lead list as the source of truth. Keep the original name, company, role, source row, and existing URL for each lead.
- Maintain separate checkpoints for extraction and Google URL discovery. A confident Google result is not evidence that an extraction page was complete, and vice versa.
- Use public person-profile `/in/` URLs only for deliverables. Never substitute Sales Navigator, company, post, people-directory, or search URLs.
- Do not guess a profile slug. A blank or unresolved URL is safer than a plausible wrong person.
- LinkedIn browsing is read-only unless the user explicitly authorizes a spreadsheet edit. Never connect, message, follow, react, save leads, change account settings, or solve a CAPTCHA.
- During default URL discovery, do not open individual LinkedIn pages. Use only Google results and stop if Google presents sign-in, CAPTCHA, unusual-traffic, or verification pages.
- Before modifying a workbook, obtain explicit authorization. Then change only the requested cells and preserve all unrelated sheets, formulas, formatting, hyperlinks, and row order.
- For a requested original-file replacement, first validate a staged enriched copy, then archive the original with a timestamp and verify the final placed workbook against that archive.

## Full-Pipeline Handoff

For a completed run, provide:

- total extracted lead rows and deduplicated rows;
- URL counts for `Found`, `Needs review`, and `Not checked`;
- any confidently discovered public URLs and the matching Google-result evidence;
- the saved workbook and audit-report paths;
- any interrupted page, row, or audit order required for resumption.

Do not claim the workflow is complete if an extraction repair queue or unresolved URL queue remains.
