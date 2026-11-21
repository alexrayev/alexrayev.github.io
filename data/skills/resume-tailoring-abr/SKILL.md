---
name: resume-tailoring-abr
description: "Tailor, validate and export Alexander Rayev's 2-page resume (.docx and .pdf) for a specific job posting or role, using the master resume as the source of truth. Use when asked to adapt, shorten, retarget or check a resume against a job description or requirements document, to add or remove sections, to produce a recruiter or public edition, or to validate page count, layout, links and spelling of a resume."
---

# Resume tailoring and validation

Master: `ARayev.docx` (+ `.pdf`), exactly 2 pages. Variants are new files (`ARayev-<role>.docx/.pdf`) and are never published; only the general public edition goes on the site (see `portfolio-site-abr`).

## 1. Read the target
- Job posting: fetch the page; if it returns 403 or is JS-rendered, open it with Playwright in Edge (`headless=False`) and read the body text. A requirements document (.docx/.pdf) is read directly.
- Extract: must-have skills, preferred skills, seniority, domain, location/work arrangement, and unusual asks (a named tool such as Claude Code, regulated-industry experience, incident management).

## 2. Map evidence, do not invent
- For each requirement, find real evidence in the master resume, the portfolio case studies or the project repos. Use the strongest 3-5 matches as lead bullets.
- Mirror the posting's wording only where the facts support it. Never add skills, titles, employers, dates, years of experience or metrics that are not already true and documented. If the resume lacks something the posting asks for, say so in your reply instead of papering over it.
- Respect user directives about wording (for example: say "AI" not "edge AI" for a role, no "N years" in the header, add or keep a specific sentence verbatim).
- Titles and dates stay as on the master unless the user explicitly changes them; flag any difference (a recruiter or background check will see it).

## 3. Edit the .docx (python-docx)
- Work on a copy. The layout is one table: left column = section label, right column = content. Rows: Summary, Software (skills), Experience (one row per company or paragraph group), Education, Personal.
- Replace text on the first run and remove the other runs so formatting is kept. Clone an existing bullet paragraph (`copy.deepcopy`) to add bullets. Remove blank spacer paragraphs and fixed row heights when space is tight. Add `snapToGrid=0` and consistent 11 pt paragraph marks if gaps look uneven.
- Keep each bullet to the result: what was built, the stack, the measured outcome. Merge bullets that describe the same system.
- Header lines: name, optional location line, email (hyperlink), portfolio link (`https://alexrayev.github.io/`, hyperlink, visible text `alexrayev.github.io`). Recruiter editions may include phone and street address; the public edition removes phone, street and ZIP and keeps city and state.

## 4. Validate and export (Word COM, never skip)
- `ComputeStatistics(2)` = 2 pages; `Range.Information(3)` for the page of "DELL-EMC" = 2 and for the last Infineon bullet = 1. Fix by trimming wording in the longest Infineon bullets; set `keep_with_next` on the Dell header, title and first paragraph so the header never strands at the bottom of page 1.
- Spelling/grammar: only product names (for example Crossplane, RxJS, Dask) may be flagged. No tracked changes or comments.
- `ExportAsFixedFormat(pdf, 17)`; then read the PDF with PyMuPDF: page count, hyperlink URIs (`mailto:` and the portfolio URL), forbidden strings absent for the chosen edition, and a word-level diff against the docx text (only caps and line-break hyphens may differ).
- Render PNGs of both pages and look at them.

## Locked files
Word may hold the file (`~$` file, "Read-Only" window title). Save to a new versioned name rather than fail; stop only your own hidden `WINWORD` process, by PID.

## 5. Report
Say which file is final, what changed and why (mapped to posting requirements), what the posting asks for that the resume cannot support, and which claims the user must confirm (wording of AI-tool usage, titles, employer approval of metrics). Upload to GitHub only on request.
