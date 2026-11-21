---
name: portfolio-deck-abr
description: "Build a polished PowerPoint (.pptx) portfolio deck for one of Alexander Rayev's projects (a code repo, a running GUI, an AWS-deployed system, or a process) in the teal/lime Infineon portfolio style. Use when asked to create a portfolio deck, case-study presentation or architecture deck from a repo, a live application or an AWS account, or to redraw a deployment diagram with better presentation. Covers discovery, read-only evidence capture, screenshots, python-pptx generation, PowerPoint render QA and committing to the private repo."
---

# Portfolio deck (.pptx) for a project

Produces a 15-26 slide deck in the same style as the existing portfolio decks. These decks contain real GUIs, AWS details and findings, so they are **internal**: commit them only to a private repo, never to the public portfolio site. For the public site use the `portfolio-site-abr` skill.

## 1. Discover (read-only)
- Repo: clone with local git credentials (`GIT_TERMINAL_PROMPT=0`). Read README, docs, config, tests, CI. If a clone returns 403 with a SAML message, the org needs re-authorization; do not work around it.
- Running GUI: drive your own Edge with Playwright (`channel="msedge"`, `headless=False`; headless is blocked by policy). The user signs in manually; never type credentials. Capture 1500x900 or larger. Delete profiles and temp files afterwards.
- AWS: use the `aws` CLI with a named read-only profile and the project's region. Only `describe/list/get` calls. Do not publish account IDs, ARNs, hostnames, tokens or keys; mask names in screenshots.
- Process/data decks: read the source deck, CSVs and scripts. Treat secrets in scripts (tokens, passwords, internal hosts) as sensitive; never copy them into a deck and tell the user to rotate them.

## 2. Plan the storyline
Cover: title, what it is, why/problem, architecture, key GUI screens (one per slide with 4-5 captioned bullets), engineering highlights, results/metrics, capabilities, tech stack, closing summary. Add a security/findings slide only when the evidence is real. Prefer measured numbers; label projections as projections.

## 3. Generate with python-pptx
Use constants: `TEAL 0A8276`, `TEAL_D 08665C`, `LIME 9BBA43`, `MINT DFF4F3`, `INK 1D1D1D`, `GREY 575352`, `LIGHT F7F7F7`, `LINE EEEDED`, `MAGENTA BE3283`, `ORANGE F97414`; font "Source Sans 3"; slide size 12191695 x 6858000 EMU. Layout: teal header band with a lime underline, kicker text in caps (e.g. "ENGINEERING"), rounded cards, numbered badges, screenshot on the left and bullets on the right.
- Keep text boxes autosize-safe: short bullets, explicit font sizes, no overflow.
- AWS diagrams: use the official AWS Architecture Icons package (download from the AWS icon release; keep the 48px PNGs you need) and credit "AWS Architecture Icons (c) Amazon Web Services".
- Diagram redraws: author an SVG, render with Playwright to PNG at device scale 1.5, save PNG/JPG/SVG next to the original and keep the original as `*-original.*`.
- Use `git mv` when moving decks into `Portfolio/` so history is kept.

## 4. QA (always)
- Export every slide to PNG with PowerPoint COM (`PowerPoint.Application`, `Slide.Export`) or LibreOffice and look at each one: overlaps, clipped text, wrong colours, unreadable screenshots.
- Check numbers against the source. Check that no secret, token, email or internal host appears in text, notes or images.
- Fix and re-render until clean.

## 5. Deliver
- Save in the `Portfolio/` folder of the private repository and keep a local copy.
- Commit and push only when the user says so; commit message ends with `Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>`.
- Tell the user what was left out on purpose (secrets, unmeasured claims) and what needs employer approval.

## Pitfalls
- Edit files with the edit/create tools, not PowerShell here-strings. Run Python with `PYTHONIOENCODING=utf-8` on Windows.
- Word/PowerPoint may hold a file open (`~$` lock file): write a new versioned file rather than fail.
- The integrated browser viewport is tiny; use Playwright's own Edge for full-size captures.
