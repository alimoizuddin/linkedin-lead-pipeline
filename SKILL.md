---
name: linkedin-lead-pipeline
description: Run an end-to-end LinkedIn lead workflow: extract a signed-in Sales Navigator search, verify existing profile URLs, and repair only confidently proven broken links. Use for lead spreadsheet pipelines, not LinkedIn outreach.
---

# LinkedIn Lead Pipeline

Use this as the parent workflow for lead-list collection and LinkedIn profile-quality work. The three implementation skills remain independent submodules under `skills/`; load only the one needed for the user’s requested phase.

## Choose The Phase

1. **Extract from Sales Navigator**: the user has an open, signed-in Sales Navigator people search and wants lead rows collected. Read [Sales Navigator extraction](skills/linkedin-sales-nav-leads/SKILL.md).
2. **Verify existing URLs**: a workbook already contains LinkedIn URLs and the user wants to know whether they match each lead. Read [LinkedIn lead verification](skills/linkedin-lead-verification/SKILL.md).
3. **Find or repair URLs**: links are blank, broken, or wrong and the user explicitly wants a replacement URL found. Read [Public URL discovery](skills/finding-linkedin-id/SKILL.md).
4. **Full pipeline**: use the three phases in that order. Do not begin a later phase until the earlier phase's checkpoint or workbook is saved and verified.

## Shared Rules

- Preserve the lead list as the source of truth. Keep the original name, company, role, source row, and existing URL for each lead.
- Maintain separate checkpoints for extraction, URL verification, and URL discovery. A verified profile result is not evidence that an extraction page was complete, and vice versa.
- Use public person-profile `/in/` URLs only for deliverables. Never substitute Sales Navigator, company, post, people-directory, or search URLs.
- Do not guess a profile slug. A blank or unresolved URL is safer than a plausible wrong person.
- LinkedIn browsing is read-only unless the user explicitly authorizes a spreadsheet edit. Never connect, message, follow, react, save leads, change account settings, or solve a CAPTCHA.
- If LinkedIn presents a sign-in, security, rate-limit, or restriction screen, save progress and stop. Do not work around the restriction; report the exact resume point.
- Before modifying a workbook, obtain explicit authorization. Then change only the requested cells and preserve all unrelated sheets, formulas, formatting, hyperlinks, and row order.

## Full-Pipeline Handoff

For a completed run, provide:

- total extracted lead rows and deduplicated rows;
- URL counts for `Verified`, `Unverified`, `Broken`, `Needs review`, and `Not checked`;
- any confidently discovered replacement URLs and the evidence supporting them;
- the saved workbook and audit-report paths;
- any interrupted page, row, or audit order required for resumption.

Do not claim the workflow is complete if an extraction repair queue, verification checkpoint, or unresolved URL queue remains.
