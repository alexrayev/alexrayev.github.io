---
name: portfolio-site-abr
description: "Build, extend and publish Alexander Rayev's public employment portfolio website (static HTML on GitHub Pages at https://alexrayev.github.io/): add or update a sanitized case-study page, update the home page, skills, patents or README, add charts and diagrams, and publish the public resume PDF. Use when asked to add a project to the portfolio site, update links or text on the site, or publish the resume to GitHub. For tailoring or validating a resume use resume-tailoring-abr."
---

# Public portfolio site (GitHub Pages)

Repo: `https://github.com/alexrayev/alexrayev.github.io` (branch `main`), a local clone of it. Plain static HTML + one CSS file, no build step. Live site: `https://alexrayev.github.io/`.

## Hard rules (public = sanitized)
- Everything is public. Never publish: internal screenshots, hostnames, account IDs, ARNs, tokens, customer names, private repo URLs, or unpublished patent text. Filed (unpublished) patents are listed by title only, and only because the user chose so.
- Generalise details; draw simplified diagrams yourself. Real GUIs, AWS inventories and findings stay in the private decks (`portfolio-deck-abr`).
- Never invent numbers. Use measured results from the source; label projections as projections. Illustrative "embodiment" numbers from patent documents are not results.
- Do not mention internal document IDs or quote patent text. Ask once for employer/IP approval when adding Infineon-internal material, then follow the answer.
- Publish only when the user says "publish/push". Commit trailer: `Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>`.

## Structure
```
index.html            hero, stats, project cards, skills, experience, patents (granted + filed), education, contact
projects/<slug>.html  one case study per project
assets/style.css      theme (teal #0a8276, lime #9bba43, dark-mode aware)
assets/icons|keisan|lpwwd/...  images used by pages
docs/Alexander-Rayev-Resume.pdf   the downloadable public resume
README.md             project table + site link
```

## Add a case study
1. Collect facts from the source (repo, deck, PDF, resume). Verify every number.
2. Copy an existing page as the skeleton. Sections in order: crumbs, `h1` + `.tag`, `.meta` (Period, My role, Employer), The challenge, What I built (bullets), Architecture (`figure.diagram` with `.flow`/`.box a|b|c|d|g`/`.arr`), optional bar charts (`.bars` > `.brow` > `.bar|.bar.old|.bar.warn|.bar.proj`), screenshots (`figure.diagram > .shot > img`, always with `alt`, `width`/`height`), Outcomes, Technologies (`.chips`), previous/next links (`.pn`), footer disclaimer.
3. Add: a card in `index.html` (`.cards`, `.chips`, "Read the case study"), a README table row, and wire the previous/next links of the two neighbouring pages.
4. Charts/images: crop out header strips that show paths or hostnames; resize to ~1600 px wide; optimise PNG.
5. Link public product pages only when they are public (a product site or the `Infineon/amk` folder); add a "Visit the live product" button.
6. Verify (below), then commit and push only on request.

## Verify before publishing
- Link/asset check: every local `href`/`src` exists (script over `**/*.html`). Check external links respond 200 and are not "page not found" (Infineon returns 200 for missing pages; check the `<h1>`).
- Render with Playwright Edge (`headless=False`) at 1200 px and 390 px; confirm `scrollWidth` equals the viewport on mobile, and view the screenshot.
- After `git push`, poll the live URL (and the file hash for PDFs) until it matches; Pages takes about 30-90 s.

## Resume handling
- Resume work (tailoring, validation, PDF export, recruiter vs public edition) is in the `resume-tailoring-abr` skill. Rules that matter for this site:
- The file at `docs/Alexander-Rayev-Resume.pdf` is the **public edition**: no street address, ZIP or phone; keep "Hopedale, MA", email and the portfolio link; no metrics from private repos (for example PESQ/STOI). Tailored variants are never published here.
- Publish by copying the validated 2-page PDF over `docs/Alexander-Rayev-Resume.pdf`, committing, pushing, then confirming that the live file hash matches the local one and that the downloaded PDF has no phone, street or private metrics.

## Accounts and URLs
- GitHub account is `alexrayev`; Pages source is `main` / root. Use `alexrayev.github.io` in resumes.
- `gh` CLI is not installed; use git over HTTPS with local credentials and the GitHub MCP read tools. Private repos need local git credentials (`GIT_TERMINAL_PROMPT=0`).
