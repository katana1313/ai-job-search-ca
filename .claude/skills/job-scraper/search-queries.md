# Search Queries for Job Scraper — Canada

<!-- Populated by /setup for Raymond Chu. Re-run `/setup --section search` to update. -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI
first. In this Canadian fork the relevant ones are:

| Skill | Covers | Notes |
|-------|--------|-------|
| `jobbank-ca-search` | Job Bank / Guichet-Emplois, all of Canada | Government-run, every province and territory, all sectors. `--lang fr` for the French listings |
| `gcjobs-search` | GC Jobs — federal public service | Jobs open to the public. Sweeps the listing and filters locally, so give it ~30 s |
| `linkedin-search` | Global, incl. Canada | Pass a Canadian place string, e.g. `-l "Vancouver, British Columbia, Canada"` |
| `freehire-search` | Country-agnostic REST API | Ships with upstream |
| `talent-com-search` | Talent.com, defaults to ca.talent.com | Every province/territory, English and French |
| `eluta-search` | Eluta.ca | Indexes employer career pages directly ("Canada's Top 100 Employers"), good for jobs never posted to boards |

The Danish demo skills (`jobindex-search`, `jobnet-search`, `jobbank-search`,
`jobdanmark-search`) are inherited from upstream and left installed for reference.
**Set `enabled: false` in their `SKILL.md` frontmatter so `/scrape` skips them** — they
will otherwise run Danish queries on every scrape.

> `jobbank-search` (upstream, Danish `jobbank.dk`) and `jobbank-ca-search` (this fork,
> Canadian `jobbank.gc.ca`) are different boards with confusingly similar names. The
> Canadian one always carries the `-ca` suffix.

The `site:` query templates below are the **WebSearch fallback** — for boards without a
CLI, company career pages, or when a CLI fails.

## Search sites

Primary (have CLIs — no `site:` line needed):
- **jobbank.gc.ca** — Job Bank, national coverage
- **emploisfp-psjobs.cfp-psc.gc.ca** — GC Jobs, federal public service
- **linkedin.com/jobs** — filter to Vancouver / Metro Vancouver
- **ca.talent.com** — Canadian aggregator
- **eluta.ca** — indexes employer career pages directly

Secondary (WebSearch fallback, no CLI in this fork):
- **indeed.ca** — largest commercial board in Canada; blocks automated access, so
  WebSearch only
- **glassdoor.ca** — postings plus salary and review context
- **jobillico.com** — strong in Quebec, bilingual (lower priority — Raymond is
  Vancouver-only and English-professional; keep for national sweeps, not a primary source)
- **workinnonprofits.ca**, **charityvillage.com** — non-profit sector
- **BC Public Service Careers** (gov.bc.ca/careers) — provincial
- **City of Vancouver careers** — municipal
- Company career pages via `site:` search

## Query categories

Combine each query with Vancouver-area location terms: `Vancouver`, `Metro Vancouver`,
`Greater Vancouver`, `Burnaby`, `Richmond`, `North Vancouver`, `West Vancouver`,
`New Westminster`, `Coquitlam`, `Surrey`, `Remote Canada`, `Hybrid Vancouver`.

### Priority 1: Senior Product Manager / Group Product Manager / Principal Product Manager / Director of Product

Core target titles, in rough order of seniority match.

```
site:linkedin.com/jobs "Senior Product Manager" Vancouver Canada
site:linkedin.com/jobs "Group Product Manager" Vancouver Canada
site:linkedin.com/jobs "Principal Product Manager" Vancouver Canada
site:linkedin.com/jobs "Director of Product" Vancouver Canada
site:indeed.ca "Senior Product Manager" OR "Director of Product" Vancouver
site:eluta.ca "Product Manager" Vancouver
"Senior Product Manager" OR "Director of Product" "Vancouver" careers -site:linkedin.com
```

Also run the NOC official title for the role, not just the colloquial one — Canadian
postings frequently use NOC wording verbatim. See `09-canada-conventions.md` §6.

### Priority 2: Domain keywords

Primary (weight heavily): **CRM**, **GenAI/AI product**, **B2B SaaS**.
Secondary (lighter weight — real experience, not the lead pitch): **PCI/payments compliance**, **IoT**.

```
site:linkedin.com/jobs "Product Manager" CRM Vancouver Canada
site:linkedin.com/jobs "Product Manager" "GenAI" OR "AI product" Vancouver Canada
site:linkedin.com/jobs "Product Manager" "B2B SaaS" Vancouver Canada
site:indeed.ca "Product Manager" CRM OR "GenAI" "British Columbia"
site:talent.com "Product Manager" "B2B SaaS" Vancouver
site:linkedin.com/jobs "Product Manager" PCI OR payments Vancouver Canada
site:linkedin.com/jobs "Product Manager" IoT Vancouver Canada
```

### Priority 3: Adjacent roles (pivot potential)

```
site:linkedin.com/jobs "Program Manager" Vancouver Canada
site:linkedin.com/jobs "Manager, Call Centre Integrations" OR "Manager, Contact Centre Technology" Vancouver
site:indeed.ca "Program Manager" "British Columbia"
site:indeed.ca "Call Centre" Technology Manager Vancouver
```

### Priority 4: Public sector

Federal is covered by the `gcjobs-search` CLI. These reach the provincial, municipal,
and broader-public-sector boards it does not:

```
site:gov.bc.ca/careers "Product Manager" OR "Program Manager"
"Senior Product Manager" city of Vancouver careers
"Product Manager" BC health authority careers
```

**Language caution:** Raymond's French is conversational/travel-level only, not
professional. Do not surface or prioritize "Bilingual - imperative" federal postings on
the assumption his French qualifies — see `CLAUDE.md` Identity section and
`09-canada-conventions.md` §8 on federal language requirements.

### Priority 5: Remote and cross-border

```
site:linkedin.com/jobs "Senior Product Manager" "remote" Canada
site:linkedin.com/jobs "Director of Product" "remote - Canada" OR "Canada remote"
```

Watch for US postings that say "remote" but are not open to Canadian residents —
check for a Canadian entity or "authorized to work in Canada" before applying.

### Target Company Watch List

Direct monitoring for companies of specific interest, run alongside the priority
categories above. Confirm each company's actual careers-page/ATS domain before relying
on a `site:` filter against it — these shift over time.

```
site:linkedin.com/jobs "Product Manager" Workday
site:linkedin.com/jobs "Product Manager" Arc'teryx
site:linkedin.com/jobs "Product Manager" Instacart
site:linkedin.com/jobs "Product Manager" Asana
site:linkedin.com/jobs "Product Manager" Wealthsimple
```

Also run `linkedin-search -k "Product Manager" -l "Vancouver, British Columbia, Canada"`
and filter results locally for these five employers, since LinkedIn's own search often
surfaces postings `site:` filters miss.

## Location filter

Raymond is not open to relocation. Vancouver/Metro Vancouver only.

- **Ideal:** Vancouver, Burnaby, Richmond, New Westminster, North Vancouver, West
  Vancouver — core Metro Vancouver, realistic daily commute
- **Acceptable:** Coquitlam, Port Moody, Port Coquitlam, Surrey, Delta — Metro
  Vancouver periphery, commutable but longer
- **Borderline:** Langley, Abbotsford, Fraser Valley — only if fully remote or rare
  in-office days
- **Too far:** anywhere outside Metro Vancouver requiring a regular in-person commute
  (Victoria, Kelowna, Calgary, Toronto, etc.), unless the role is fully remote

Canadian specifics worth encoding:
- Job Bank writes locations as `City (PR)`, e.g. `Vancouver (BC)`; GC Jobs writes
  `City (Province)`, e.g. `Vancouver (British Columbia)`.
- Postings covering several sites appear as "Various locations" — open the posting to
  see whether Vancouver is included.
- Winter commute distances are not summer commute distances; be honest about the limit.

## Date filter

Only include jobs posted within the last 14 days, or whose closing date has not passed.
Where a posting date cannot be determined, include it but flag as "date unknown".

GC Jobs publishes a **closing** date rather than a posting date — filter those on the
deadline instead, and treat anything closing within 48 hours as urgent.

## Work-authorization filter

Raymond is a Canadian citizen — no sponsorship-related screening needed. Still screen
out:
- Federal postings with a *Who can apply* restriction that excludes external candidates
  where relevant (`whoCanApply` from `gcjobs-search`)
- Security-cleared roles that require a clearance level Raymond does not hold
- "Bilingual - imperative" federal postings (see Priority 4 language caution above) —
  his French does not meet a professional bilingual bar

## Adapting queries

If the user specifies a focus area, select queries from the matching category and
generate 2-3 custom queries for that focus. For example:
- `/scrape federal` → run `gcjobs-search` with no title filter plus the public-sector
  queries (screen out bilingual-imperative postings per the language caution above)
- `/scrape remote` → the remote category plus
  `linkedin-search --remote remote -l "Canada"`
- `/scrape companies` → the Target Company Watch List section only
