---
framework_version: 1.2.2
---

# Job Evaluation Criteria — Raymond Chu

## Fit Analysis Process (mandatory on every new JD, once)
Before drafting anything for a new JD:
1. Strongest matching story and why (pull from 07-interview-prep.md /
   Story Bank).
2. Gaps or reframing needed.
3. Honest callback likelihood.
Then ask clarifying questions before drafting. Do not repeat the Fit
Analysis again later in the same session unless a new JD is introduced.

## Target Roles
Senior Product Manager through Director of Product (Senior PM, Group PM,
Principal PM, Director of Product all in scope) — CRM/CX platforms, IoT/
health tech, GenAI/AI product, payments/compliance-adjacent, or B2B SaaS
domains.

## Locations
Vancouver, BC / Metro Vancouver only. Not open to relocation at this time.

## Work Authorization
Canadian citizen — no sponsorship required for any Canadian role.

## Deal-Breakers
- Base salary below $130K CAD.
- Relocation outside Metro Vancouver (not open to relocation at this time).

## Strong Preferences (not deal-breakers, but weighted in ranking)
- On-call and travel requirements are flexible if compensation reflects
  the added demand, not a filter on their own.
- No industry exclusions — open to any sector.
- Genuine GenAI/AI product scope, technical PM work with API/platform
  ownership, and B2B SaaS or CRM/CX domains are strong natural fits per
  the Domain Keyword Map below, but are not hard requirements.

## Domain Keyword Map (for JD matching — condensed from candidate profile)
| Domain | Real Experience | Notes |
|---|---|---|
| CRM | D365, OSC, Salesforce | Direct |
| IoT | TELUS Health Aging in Place | Direct |
| AI/GenAI | LLM pilot, Murf.ai IVR, Copilot pilot, Custom Copilot | Direct |
| Chatbots | Quiq (owned), NARVAR integration | Direct |
| Payments/PCI | PCI Pal audits, DTMF integration | Direct |
| B2B SaaS | Flowfinity (builder), lululemon (buyer/operator) | Be precise on builder vs. buyer distinction |
| Ecommerce | NARVAR-Quiq shipment tracking | Best direct ecommerce-ownership story |

Full domain map and reframing notes live in 01-candidate-profile.md — refer
there for anything not covered above, and ask Raymond before assuming a
gap.

## Eligibility Gate — run before scoring

Raymond is a Canadian citizen applying to Canadian roles, so this gate
passes automatically for the target market. Keep it active for the rare
case of a posting requiring a clearance level tied to additional
citizenship history, or a non-Canadian posting slipping through.

If the candidate is not a citizen or permanent resident of the country they are applying in, run this first. It is a hard filter, not a scoring dimension, and it is separate from work-permit *timing*: timing asks "can they work the required hours yet?", eligibility asks "are they permitted to hold this job at all?". A candidate can pass timing and still be categorically excluded.

Read the posting's eligibility / work rights / "who can apply" section **verbatim** and classify:

| Posting wording | Verdict |
|-----------------|---------|
| Names a **citizenship or permanent-residency requirement** ("must be a citizen of X", "permanent resident", "PR required", "full working rights" where the employer means citizen/PR) | **FAIL — hard stop.** Do not score, do not draft. Quote the exact wording back to the user. |
| Requires a **security clearance** at any level | **FAIL** in most countries, since clearance is normally gated on citizenship. Verify the specific scheme rather than assuming. |
| **Explicitly names** the candidate's permit class, or says "international applicants welcome", "visa holders considered", "we sponsor" | **PASS** — verified acceptance. Worth noting as a positive in the application. |
| **Silent** on citizenship or residency | **PROCEED, but mark unverified.** Check the employer's own careers or international-applicant page before drafting. |

**Two rules that are easy to get wrong:**

1. **Silence is not permission.** Large graduate programs frequently gate eligibility on their own website rather than in the job ad. Highest-risk categories: professional-services firms, government and defence, banking, telecommunications, and anything touching critical infrastructure.
2. **A company-wide "we accept international applicants" statement is not role-level permission.** The common pattern is a general welcome followed by a *named list* of the specific programs or service lines it covers. Confirm the **specific posting or stream** appears on that list before drafting.

**Report an eligibility failure to the user with the quoted source** rather than silently dropping the role. They may know something about their own status that the profile does not record.

If the candidate's permit also constrains *hours* or *start date* (a student visa with a term-time cap, a permit that begins on graduation), record that as a second gate under this section during `/setup`, with the specific dates. Do not merge it with the eligibility question above — they fail for different reasons and need different answers.

A role that fails this gate is not scored and not drafted. Everything below applies only to roles that pass it.

## Language Gate — run before scoring

No dimension or gate anywhere in this framework currently checks a posting's language requirements against what the candidate actually speaks - it is not one of the five Scoring Dimensions below, not a field `/scrape` or `/rank` track, and not something `/apply`'s language detection (Step 1, which already extracts a posting's required language generically) has anywhere to report to. This gate adds that check, structured the same way as the Eligibility Gate above: read the posting, classify against profile data, and treat a hard mismatch as FAIL before scoring.

Read the posting's language requirements as stated for **the role itself** — not the language the ad happens to be written in. A posting written in a language you don't work in, for a role that only needs languages you do work in on the job, passes fine; only an explicit job-condition requirement ("fluent X required," "must communicate with the Y team in Z") triggers this check. For each language the posting requires as a job condition, compare it against your Languages table in CLAUDE.md / `01-candidate-profile.md`:

| Posting requirement vs. your Languages table | Verdict |
|---|---|
| Requires a language **not on your table at all** (e.g. "fluent Polish required," "must communicate with the Warsaw team in Russian," and you list no Polish/Russian row) | **FAIL — hard stop.** Do not score, do not draft. Quote the exact requirement line. |
| Requires a language you **do** list, but the posting's stated bar (as written — "fluent," "native," "C1+," "business-level") reads as plausibly **higher** than your declared level | **FLAG, then proceed.** Not a fail. Score and draft normally, but surface the gap explicitly in your report to the user (quote both the posting's requirement and your declared level) so they can judge it themselves — bars like "fluent" vary a lot by company and geography, and a recruiter may be flexible. Never silently drop the posting and never silently treat it as a clean pass. |
| Requires a language you list, at or below your declared level (or the posting doesn't specify a level at all — just names the language) | **PASS.** No note needed. |

Judge the level comparison the same way you judge everything else in this framework: read both sides as written and reason about it, don't force either into a rigid scale — CEFR letters, LinkedIn-style buckets ("professional working proficiency"), and plain-English words ("conversational," "fluent," "native") all appear in the wild and don't map onto each other precisely. When genuinely unsure whether a stated bar exceeds the candidate's level, prefer FLAG over a silent PASS — the human is meant to be the tiebreaker, not the gate.

**Worked example (Raymond's profile):** Languages table lists English (Native/professional), Cantonese (Native), and French/Mandarin/Japanese (Conversational/travel-level). A posting requiring "Bilingual - imperative" (French/English, federal postings) → **FAIL**, French is declared only at conversational/travel level, well below a federal "imperative" bar — do not treat it as meeting the requirement. A posting requiring "fluent English" → **PASS**, native/professional clears it cleanly. A posting requiring "conversational French an asset" → **PASS** with a note, since it's a nice-to-have, not a job condition.

## Scoring Dimensions

Evaluate each job posting against these five dimensions:

### 1. Technical Skills Match (0-100)
How well do the required/preferred skills align with the candidate's capabilities?

| Score | Meaning |
|-------|---------|
| 80-100 | Core requirements are primary skills |
| 60-79 | Most requirements match, 1-2 gaps that are learnable |
| 40-59 | Partial match, significant upskilling needed |
| 0-39 | Fundamental mismatch |

**Strong match areas:** CRM/CX platform ownership (Oracle Service Cloud, D365, Salesforce Service Cloud), payments/PCI compliance (PCI Pal, DTMF), GenAI/AI product pilots
**Moderate match areas:** Chatbot/conversational platforms (Quiq, NARVAR), voice AI/IVR (Murf.ai, Five9), B2B SaaS platform ownership (Flowfinity)
**Weak match areas:** Deep hands-on engineering/coding, formal people-management of a PM team

### 2. Experience Match (0-100)
Does work history align with what they're looking for?

| Score | Meaning |
|-------|---------|
| 80-100 | Direct experience in the same domain and role type |
| 60-79 | Related experience, transferable skills clear |
| 40-59 | Adjacent experience, would need to make the case |
| 0-39 | Unrelated experience |

**Strong:** CRM/CX platforms, IoT/health tech, contact center operations at scale, global hardware/vendor sourcing
**Moderate:** GenAI/AI product (pilot-scale, not ground-up platform build), B2B SaaS (mixed builder/buyer history)
**Entry-level:** Formal people-management of a PM organization

### 3. Behavioral/Culture Fit (0-100)
Does the role and company culture match the behavioral profile?

| Score | Meaning |
|-------|---------|
| 80-100 | Culture strongly matches behavioral preferences |
| 60-79 | Mixed signals but mostly compatible |
| 40-59 | Some friction areas |
| 0-39 | Significant culture mismatch |

**Red flags to research:** Department disorganization, work dominated by maintenance over development, poor chemistry with leadership, culture mismatches. Check reviews, media coverage, LinkedIn connections, and network contacts for insider perspective.

### 4. Location & Logistics (Pass/Fail + Notes)
- Within commute range: PASS
- Remote with occasional office: PASS
- Requires relocation: FAIL (deal-breaker)
- Frequent international travel: FLAG (discuss with user)

### 5. Career Alignment & Motivation (0-100)
Does this role advance career goals and contain tasks that energize?

| Score | Meaning |
|-------|---------|
| 80-100 | Strongly aligned with career direction, clear growth path |
| 60-79 | Good role but only partially aligned with long-term goals |
| 40-59 | Decent job but doesn't build toward career goals |
| 0-39 | Dead end or backwards step |

**Career goals:**
- Grow into Group PM / Director of Product scope on a CRM/CX, GenAI/AI, or platform-ownership mandate.
- Keep building genuine GenAI/AI product depth rather than one-off pilots.
- Stay in Metro Vancouver, at $130K+ CAD base.

**Motivation filter:** Evaluate not just whether you *can* do the tasks, but whether the tasks will *energize* you. Consider:
- Tasks that energize: Untangling broken/ungoverned systems nobody owns, 0-to-1 builds in ambiguous problem spaces, translating messy vendor/technical complexity into shippable decisions.
- Tasks that drain: Purely maintenance-mode roadmaps with no ownership ambiguity to resolve.
- Non-task factors: leadership style, department culture, company values, degree of autonomy.

**Life situation alignment:** Consider personal constraints:
- **Security**: Actively seeking since May 2026; base salary below $130K CAD is a hard deal-breaker.
- **Flexibility**: Metro Vancouver only, not open to relocation.
- **Professional development**: Prioritize roles with genuine AI/GenAI product scope or deeper platform ownership over lateral moves.

### 6. Salary Benchmark (Optional)

If the salary lookup tool is configured (`salary_data.json` exists), look up the company:
```
python salary_lookup.py "<Company Name>" --json
```

If a city is known from the posting, add `--city "<City>"` to narrow results.

Present findings as:
```
### Salary Benchmark
| Metric | Value |
|--------|-------|
| [Category] index | XX.X (+/-X.X% vs baseline) |
| Overall index | XX.X (+/-X.X% vs baseline) |
```

Interpret results relative to the baseline defined in the data file's metadata. For index-based data, higher typically means above-market compensation.

If the salary tool is not configured, skip this section.

## Output Format

Present the evaluation as:

```
## Job Fit Evaluation: [Role] at [Company]

| Dimension | Score | Notes |
|-----------|-------|-------|
| Technical Skills | XX/100 | [brief note] |
| Experience Match | XX/100 | [brief note] |
| Behavioral Fit | XX/100 | [brief note] |
| Location | PASS/FAIL | [brief note] |
| Career Alignment | XX/100 | [brief note] |

**Overall Score: XX/100** (weighted average of scored dimensions)

### Verdict: [Strong Fit / Good Fit / Moderate Fit / Weak Fit / Poor Fit]

### Key Strengths for This Role
- [bullet points]

### Gaps to Address
- [bullet points]

### Recommendation
[1-2 sentences: apply/skip/apply with caveats]

### Company Research Checklist
- [ ] Checked company website (mission, values, recent news)
- [ ] Checked review sites (Glassdoor, Jobindex, etc.)
- [ ] Checked LinkedIn for team size, recent hires, connections
- [ ] Checked media for restructuring, growth, or workplace issues
- [ ] Identified network contacts who may know the team/manager
```

## Weighting
- Technical Skills: 30%
- Experience Match: 25%
- Behavioral Fit: 15%
- Career Alignment: 30%

(Location is pass/fail, not weighted)

## Thresholds
- **Strong Fit** (75+): Definitely apply, tailor everything
- **Good Fit** (60-74): Apply, address gaps in cover letter
- **Moderate Fit** (45-59): Consider carefully, discuss with user
- **Weak Fit** (30-44): Probably skip unless strategic reasons
- **Poor Fit** (<30): Skip

## Pre-Application: Call the Employer (Best Practice)

Before writing the application, consider whether the candidate should call the contact person listed in the posting. **Only call if there are substantive questions** - never call just to "be remembered."

### When to Suggest Calling
- The posting has unclear or ambiguous requirements
- It's unclear which competencies are essential vs. nice-to-have
- The role description is vague about day-to-day tasks
- There's a named contact person who invites questions

### Good Questions to Ask
- "What are the primary challenges in this role?"
- "How is time typically divided across the listed responsibilities?"
- "Which competencies are most critical for success in this position?"
- "What does success look like in the first 6-12 months?"

### Rules for the Call
- Prepare a 30-second "elevator pitch" about your background in case they ask
- The call's purpose is **gathering information**, not delivering a pitch
- Take notes - use what you learn to tailor the application
- Reference the conversation naturally in the cover letter ("After speaking with [name], I was especially drawn to...")
