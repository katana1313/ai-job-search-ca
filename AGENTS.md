---
framework_version: 1.0.0
---

# Agent Guidelines: AI Job Search — Canadian fork

This workspace is structured to manage job search activities, scraper tools, CVs, cover letters, and interview preparation.

## Canadian fork: what differs from upstream

This is a community fork of [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search) adapted for the Canadian market. Agents working in this repo should know:

- **Active portals** are `jobbank-ca-search` (Job Bank / Guichet-Emplois, all of Canada, EN+FR) and `gcjobs-search` (GC Jobs, federal public service), plus the country-agnostic `linkedin-search` and `freehire-search`.
- **The four Danish demo portals ship `enabled: false`.** `/scrape` skips them. Do not re-enable them without being asked.
- **`jobbank-search` is Danish** (`jobbank.dk`); **`jobbank-ca-search` is Canadian** (`jobbank.gc.ca`). Different boards, similar names — the Canadian one always has the `-ca` suffix.
- **Canadian application rules live in [`.claude/skills/job-application-assistant/09-canada-conventions.md`](.claude/skills/job-application-assistant/09-canada-conventions.md)** and take precedence over the generic CV/cover-letter guidance for Canadian employers. The non-negotiables: no photo, age, marital status, or SIN on a résumé; work authorization stated explicitly; Canadian spelling (`-our` + `-ize`); application language matches posting language.
- **Both Canadian CLIs accept `--lang en|fr`.** French listings surface postings the English side does not, so a thorough scrape for a bilingual candidate runs both.
- **Neither Canadian portal is fast by accident.** `jobbank-ca-search` honours the site's `Crawl-delay: 5`; `gcjobs-search` sweeps ~20 listing pages because GC Jobs has no queryable API. Do not "optimise" these by parallelising or by wiring up the GC Jobs criteria form — `.agents/skills/gcjobs-search/url-reference.md` records why the form does not work.
- When a `gcjobs-search` result carries `meta.truncated: true`, the sweep was partial. Never report a truncated search as evidence that no such jobs exist.

## Thin-Pointer Design (Single Source of Truth)

To prevent duplication and configuration drift across different AI agent frameworks (Claude Code, Google Antigravity, Codex, Cursor, Gemini CLI, etc.), this workspace uses a unified thin-pointer design. All agent runtimes should load the canonical specifications and candidate profiles from the files and directories below:

1. **Personal Candidate Profile:**
   - The candidate profile, contact details, education, and target preferences are defined in [CLAUDE.md](CLAUDE.md) and the individual profile methodology files under [.claude/skills/job-application-assistant/](.claude/skills/job-application-assistant/) (specifically `01-*.md` etc.).
2. **Canonical Workflow Specifications:**
   - The step-by-step instructions and triggers for tasks (setup, scrape, rank, apply, upskill, interview) are defined in the [.claude/](.claude/) directory (specifically under `.claude/skills/` and `.claude/commands/`).
   - Do not duplicate these rules or specifications. Treat `.claude/` files as the single source of truth.
3. **Portal Search Skills:**
   - Job-portal search CLIs live under [.agents/skills/](.agents/skills/) in the portable Agent Skills format (with a `SKILL.md` per portal). Codex and Antigravity discover these automatically; the `/scrape` workflow in [.claude/skills/job-scraper/](.claude/skills/job-scraper/) orchestrates them.
