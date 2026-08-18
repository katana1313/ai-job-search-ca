---
framework_version: 1.4.0
---

# CV Templates and Tailoring Guide

<!-- SETUP: Profile statements and section ordering are personalized by running /setup -->

## Template: LaTeX moderncv (Banking Style)

All CVs use the moderncv LaTeX package with the "banking" style and "blue" color scheme.

**Output file:** `cv/main_<company>_<role>.tex`
**Compile with:** **lualatex** on MiKTeX/TeX Live. pdflatex often fails on modern MiKTeX installs with `fontawesome5` font-expansion errors; lualatex handles the same sources cleanly.
**Master reference:** `cv/main_example.tex` (comprehensive CV with all competencies, experience, and achievements - use as source when building targeted CVs). Deliberately not page-budgeted or bullet-capped: it holds more raw material per role than any single targeted CV needs, so `/apply` has real options to select from when relevance-weighted cutting (below) trims it down per JD.

### Compile command

```bash
cd cv && lualatex -interaction=nonstopmode main_<company>_<role>.tex
```

Expected output: `Output written on main_<company>_<role>.pdf (2 pages, ...)`. Any page count other than 2 is a failure that must be fixed before presenting to the user.

## Document Structure

```latex
\documentclass[11pt,a4paper,sans]{moderncv}
\moderncvstyle{banking}
\moderncvcolor{blue}

% Force both first and last name AND section headings to render in moderncv
% blue (color1). Default banking on lualatex+MiKTeX leaves these black, which
% looks inconsistent with the rest of the blue accent scheme.
\renewcommand*{\firstnamestyle}[1]{{\fontsize{34}{36}\bfseries\upshape\color{color1}#1}}
\renewcommand*{\lastnamestyle}[1]{{\fontsize{34}{36}\bfseries\upshape\color{color1}#1}}
\renewcommand*{\sectionstyle}[1]{{\sectionfont\color{color1}#1}}

\usepackage[utf8]{inputenc}
\usepackage{needspace}
% moderncv's banking style already loads fontawesome5 internally (mapped to
% FontAwesome 6 icon names on MiKTeX). Do NOT add a second
% \usepackage{fontawesome5} - it causes "already defined" compile errors.
% Use the low-level \faIcon{icon-name} form, not shortcut macros like
% \faMapMarkerAlt or bare \faLightbulb - those are not reliably defined
% under moderncv's internal load. Confirmed-working names on this install:
% \faIcon{location-dot}, \faIcon{lightbulb}.
\usepackage{hyperref}
\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    filecolor=magenta,
    urlcolor=blue,
    pdftitle={[YOUR_NAME] - CV},
    pdfpagemode=FullScreen,
}
\usepackage[scale=0.77]{geometry}
\usepackage{import}

% One-line "so what" synthesis under a role's bullets. Use sparingly -
% most relevant/senior roles only, it costs vertical space.
\newcommand{\insight}[1]{\vspace{2pt}\par{\small\itshape\color{color1}\faIcon{lightbulb}\ #1}}

% Personal data - single-line compact contact header: name, then one line
% of location | email | phone | LinkedIn. Do NOT use moderncv's separate
% \address/\phone/\email/\extrainfo lines (that renders as 2-3 stacked
% lines) - put everything in \extrainfo instead, on one line, and leave
% \address/\phone/\email uncalled.
\name{[FIRST_NAME]}{[LAST_NAME]}
\extrainfo{\small \faIcon{location-dot}\ [CITY, PROVINCE] \enspace$\vert$\enspace \href{mailto:[YOUR_EMAIL]}{[YOUR_EMAIL]} \enspace$\vert$\enspace [YOUR_PHONE] \enspace$\vert$\enspace \href{[YOUR_LINKEDIN_URL]}{LinkedIn}}

\begin{document}
\makecvtitle

% 1. Profile statement (1-3 sentences, tailored per role)
% 2. Skills section
% 3. Education section
% 4. Professional Experience section
% 5. Selected Publications (if applicable)
% 6. Honors and Awards (if applicable)
% 7. References

\end{document}
```

### Color overrides

The three `\renewcommand*` lines in the preamble are required on lualatex+MiKTeX. Without them the firstname, lastname, and section headings render in black even though `\moderncvcolor{blue}` is set, which looks inconsistent with the rest of the blue accent scheme (links, bullet markers, contact icons). The override forces all three to use `color1` (moderncv's accent colour, which becomes blue under `\moderncvcolor{blue}`). Both names render bold; if you prefer the firstname in regular weight, change the firstnamestyle override from `\bfseries` to `\mdseries`. Don't drop the override - on most modern installs the defaults render visibly wrong.

Name size is set to **22pt** (`\fontsize{22}{24}`), not moderncv's 34pt default - Raymond prefers a compact header (34pt reads as oversized next to a single-line contact row). Keep the two in proportion: a single-line contact header pairs with the smaller name; if a future variant goes back to moderncv's default stacked address/phone/email layout, the larger 34pt name reads better with it.

### Single-line contact header (Raymond's preferred style)

Put location, email, phone, and LinkedIn all on **one line** via `\extrainfo{...}`, separated by `\enspace$\vert$\enspace`, with a `\faIcon{location-dot}` marker before the location. Do not call `\address`, `\phone`, or `\email` - moderncv stacks those onto separate lines, which is the older/bulkier look Raymond moved away from. City + province only (no country, no street address - see `09-canada-conventions.md`).

**Watch the line width.** A full LinkedIn URL (`linkedin.com/in/...`) plus a full address line often overflows the page margin at this compact size - check for `Overfull \hbox` warnings referencing the header line after every compile, and visually confirm the header isn't clipped at the right margin (compare against the PDF, not just the log: a clipped line doesn't always throw a large warning). If it overflows: drop to a bare `LinkedIn` hyperlink label instead of the full URL, drop trailing country name, or tighten `\enspace` to `\ `.

### Insight line (optional "so what" callout)

A one-line italic synthesis after a role's bullets, using the `\insight{...}` macro defined in the preamble - e.g. `\insight{Drives an AI-first product pivot end to end, from market research through executive buy-in.}` placed right after `\end{itemize}` and before the closing `}}` of the `\cventry`. This is a deliberate borrow from an external Word-template style Raymond liked: it gives a skimming recruiter a 1-second "so what" without reading every bullet.

Use it selectively - it costs a full line of vertical space per role, so on a page-budgeted (2-page) tailored CV, prioritize it for the most senior/relevant 2-3 roles and drop it first if a role gets cut down to conserve space, before cutting a substantive bullet.

The icon is yellow (`\definecolor{lightbulbyellow}{HTML}{FFD400}` in the preamble), not blue - Raymond wanted a true bright yellow, not the muted amber/gold that was tried first. The icon itself uses `\color{lightbulbyellow}`, then resets to `\color{color1}` before the text so the synthesis text stays blue like the rest of the document's accent color.

### No top-level bullet glyph

moderncv's banking style default (`\labelitemi`) is a large blue `\textbullet`, and Raymond found it redundant everywhere it showed up - before each job/education entry (where the bold title/company already anchors the line) and before each Core Competency line (where the bold category label already does). Fixed at the source with a single preamble override:
```latex
\renewcommand*{\labelitemi}{}
```
This empties the glyph everywhere `\labelitemi` is used (first-level `itemize`: Core Competencies, the Professional Experience/Earlier Career entry wrappers, Education & Certifications, Languages, References) while leaving indentation/spacing untouched, since it's the same moderncv list engine, just an empty label.

**Do not use `\usepackage{enumitem}` with `\begin{itemize}[label={}]` for this** - tried first, and it silently resets itemize spacing (topsep/itemsep/parsep) document-wide once loaded, including in itemize environments that never used the optional argument. That widened the gaps between the nested "-" job bullets too (untouched second-level `\labelitemii`, which should look exactly the same as before) and pushed the tailored CV from 2 pages to 3. The `\renewcommand*{\labelitemi}{}` approach doesn't touch enumitem or spacing internals at all - verify with a page-count check either way, this class of regression won't show up as a compile error, only as an unexpected page-count change.

**Emptying the glyph alone still leaves the list indented.** `itemize` reserves its normal left-margin/label-width geometry (`\leftmargini`, `\labelwidth`, `\labelsep`, `\itemindent`) even when `\labelitemi` renders nothing - the text sits indented into blank space that used to hold the marker. This is visible on close inspection (Core Competencies/Education/Languages/References text not starting flush with the section heading rule) and it costs word-wrap: a narrower text column wraps sooner than necessary. Fix with a second local-group macro, same non-enumitem approach as `\dashitemize`:
```latex
\newcommand{\flushitemize}{\setlength{\leftmargini}{0pt}\setlength{\labelsep}{0pt}\setlength{\labelwidth}{0pt}\setlength{\itemindent}{0pt}\setlength{\listparindent}{0pt}}
```
Wrap every markerless `itemize` (Core Competencies, Education & Certifications, Languages, References) in `{\flushitemize \begin{itemize}...\end{itemize}}`. Do not apply this to the job-accomplishment bullet lists wrapped in `\dashitemize` - those keep their normal indent, since a visible dash marker reads correctly with standard indentation; only the markerless lists need flushing.

### Single-line job entry header (replaces moderncv's 2-line `\cventry` default)

moderncv's default `\cventry` layout renders company+location on one line and title+dates on the next. Raymond prefers everything on one line - `Title | Company -- Location`, dates flush right - to save vertical space, matching a Word template style he likes. Don't fight moderncv's internal `\cventry`/`\cvitem` engine to get this; define a standalone replacement and stop using `\cventry` for entries built this way:
```latex
\newcommand{\cvoneline}[4]{%
  \noindent\textbf{#1} \normalfont | #2 -- #3%
  \ifthenelse{\equal{#4}{}}{}{\hfill\textit{#4}}%
  \par\vspace{1pt}%
}
```
(`\usepackage{ifthen}` required.) Usage: `\cvoneline{Senior Product Manager, Aging in Place}{TELUS Health}{Vancouver, BC}{Dec 2025--May 2026}` - pass an empty 4th argument for undated Earlier Career entries (the date block is omitted entirely, not left as blank space). Follow immediately with the italicized overview line and the bullet list, exactly as under a `\cventry` - `\cvoneline` is a drop-in replacement for the header only.

**Side effect to watch for:** moderncv's default pattern wraps each entry in an outer `\begin{itemize}\item{\cventry{...}}\end{itemize}` (originally just for spacing). Once entries switch to `\cvoneline`, drop that outer wrapper entirely - don't keep it out of habit. If it's dropped, the job-accomplishment bullet list *inside* the entry is no longer nested inside another list, so it becomes a level-1 list instead of level-2, and silently inherits the empty `\labelitemi` from the markerless-list fix above instead of the dash marker (`\labelitemii`). This is exactly why `\dashitemize` exists - wrap every job-accomplishment bullet list in `{\dashitemize \begin{itemize}...\end{itemize}}` to restore the dash. Verify after converting any entry: check that its bullets still show dashes, not blank markers.

**Gap between entries within Professional Experience: a full line, not a tight 3pt.** `\vspace{\baselineskip}` between entries (after each entry's closing `\insight{...}` or last bullet, before the next `\cvoneline`) reads as properly separated roles rather than a dense block; `\vspace{3pt}` (moderncv's tighter default, still used for the gap between the section heading and the first entry) is too tight once entries are stacked without an outer wrapper. Before applying this to a page-budgeted tailored CV, compile and check the page count doesn't change, and visually confirm the entry that used to sit right at a page boundary (usually the 2nd role) still fits fully - `\baselineskip` per gap adds up across 3-4 entries and can tip a tight layout onto a 3rd page.

**Check for overflow before trusting it fits.** The longest title/company combinations (e.g. `Senior Product Manager, Initiatives & Global Tools | lululemon -- Vancouver, BC`) are close to the line limit at 10-11pt in a ~7.3in column - compile and check for `Overfull \hbox` warnings referencing that line, and visually confirm no clipping at the right margin, the same discipline as the contact header line.

### Spacing inside itemize lists (important)

**Do not place `\vspace{...}` between `\item` entries in an `itemize` list.** Even though the source looks symmetric, this pattern occasionally produces a noticeably oversized gap before a single item: the inter-item `\vspace` creates a paragraph break that interacts unpredictably with the list's internal `\itemsep`, so LaTeX renders one of the gaps wider than the rest. Remove the inter-item `\vspace` and let `itemize` use its native uniform spacing.

```latex
% WRONG - intermittently produces an oversized gap before one bullet
\begin{itemize}
\item \textbf{Foo}: ...
\vspace{1pt}
\item \textbf{Bar}: ...
\vspace{1pt}
\item \textbf{Baz}: ...
\end{itemize}

% RIGHT - uniform spacing using the list's native itemsep
\begin{itemize}
\item \textbf{Foo}: ...
\item \textbf{Bar}: ...
\item \textbf{Baz}: ...
\end{itemize}
```

Two related patterns are fine and should be kept:
- `\vspace{1pt}` immediately after `\section{...}` (between section heading and first item) - this is between the heading and the list, not between list items.
- `\vspace{3pt}` between top-level `\cventry` blocks in Professional Experience or Education - this gives breathing room between roles and renders consistently.

### Section headings must match the CV's language (important)

Section headings such as `\section{Core Competencies}`, `Professional Experience`, `Education`, `Languages`, `Publications`, `Honors and Awards`, `References` (and any others your template defines), plus the `Available upon request.` line under References, are all **literal English text baked into the template** - they do not translate themselves. Whenever the CV language (see `CV language` in the candidate profile) is not English, translate every one of these too, whatever they are, not just the body prose - a CV with a fully localized profile statement and bullets sitting under untouched English section headers reads as sloppy and inconsistent, and it's an easy thing to forget precisely because the prose translation is the obvious, visible part of the job. Worked example for Spanish: `Competencias Clave`, `Experiencia Profesional`, `Educaci\'on`, `Idiomas`, `Publicaciones`, `Distinciones y Premios`, `Referencias`, `Disponibles a solicitud.` The same rule applies for any other target language - check this explicitly during the verification pass.

## Section-by-Section Tailoring

### Profile Statement / Elevator Pitch (Best Practice)
This is the most important section to customize. It appears right after `\makecvtitle`.

Write 5-7 lines that function as an "elevator pitch": a concise, compelling introduction explaining why you're qualified for *this specific role*. Focus on what the employer gains from hiring you.

When the role sits outside your home domain, **lead with the domain-transfer argument** - the one or two sentences connecting your background to their problem (e.g. wave physics to radar signal processing) belong in the profile statement's opening, not buried in the cover letter. It is the strongest card a domain-changer holds; play it first.

**Create 2-3 profile statement templates for your main role types:**

<!-- SETUP: These are populated based on your background -->
**For [YOUR_PRIMARY_ROLE_TYPE] roles:**
> [YOUR_PROFILE_STATEMENT_TEMPLATE_1]

**For [YOUR_SECONDARY_ROLE_TYPE] roles:**
> [YOUR_PROFILE_STATEMENT_TEMPLATE_2]

Statements labeled *[Used for: <company>_<role>]* were extracted from archived application drafts by `/setup` Path A. They are **phrasing references, never fact sources**: when drafting from one, every factual claim still comes from `01-candidate-profile.md` - a past tailored draft does not vouch for its own accuracy.

**Target 3-4 rendered lines, and never let the last line be a 1-2 word widow.** Both 3 and 4 lines are standard for a resume summary; 3 is the safer target since it structurally can't widow, but 4 is fine if the last line is substantially full. Compile and look at the actual wrap - a widowed last line (e.g. "...align Engineering, Design, Data Science, and Revenue stakeholders." wrapping to just "Revenue stakeholders." alone) reads as unbalanced and wastes vertical space. Fix by trimming a few words to pull the wrap back a line, not by shortening randomly - trim from the least load-bearing clause first.

**Watch for run-ons disguised by punctuation.** A colon or semicolon can make 2-3 chained ideas look like one clean sentence even though it violates the same run-on rule in `03-writing-style.md` ("chaining 2-3 ideas together with commas and 'and'/'then' is a run-on even if grammatically legal"). `"...spaces: pivoting X at Company A, and running Y at Company B."` is a run-on wearing a colon as a disguise, not an exception to the rule. Target 2-3 short sentences, each carrying exactly one idea (identity, one proof point, one skill claim), roughly 40-55 words / 3-4 lines total - not one long sentence stretched across a colon and an "and".

### Core Competencies / Skills Section (Best Practice)
Reorder and emphasize based on the role. Use bold category labels.

List **5-7 key competencies** in bullet format, tailored to the specific job. For each competency, briefly explain how it adds value to the position.

Use the posting's own core term in the matching bullet's bold label when it truthfully applies - ATS and skim-reading hiring managers match literally, and "MLOps" in a heading outperforms a paraphrase like "ML Deployment".

**Capitalize the first word of every comma/semicolon-separated item within a competency line**, regardless of whether it's a proper noun. Normal-English capitalization (proper nouns only) produces an uneven-looking list here - e.g. `HubSpot, marketing campaign analytics partnership, CRM/chatbot platforms...` caps `HubSpot`/`CRM` because they're proper nouns but leaves `marketing` lowercase, which a skimming eye reads as randomly inconsistent even though it's grammatically correct. This section functions as a keyword list, not narrative prose, so treat every item the same way: `HubSpot, Marketing campaign analytics partnership, CRM/chatbot platforms...`.

### Education & Certifications (merged section)

Raymond's degree (Associate of Arts) is a weaker credential than his certifications (BrainStation Product Management, CSM, UBC Sauder Agile Leadership, MCSA) - bolding it as its own `\cventry`-style section header gave it more visual weight than it's earned. Merge Education into the Certifications list instead: one `\section{Education \& Certifications}`, each item a plain `\item Credential -- Institution` line (no bold, no separate `\cventry`), **certifications first, degree last** - matching the order in Raymond's external Word master template. Do not give the degree its own subsection or bold treatment above the certifications.

- Always include the highest degree
- Include thesis topics when relevant to the target role (rare for Raymond's profile - Associate of Arts has none)

#### In-progress qualifications must say so explicitly

**A bare year range is not enough.** An entry reading `2025–2026`, seen partway through 2026, looks like a *finished* degree, because a reader skimming a CV treats a closed range as closed. A profile statement that says "currently completing…" does not fix it: the education entry is where a reader checks the credential, so it has to stand on its own.

State completion inside the entry itself:

```latex
\item{\cventry{2025--2026}{[Degree], [Field]}{[Institution]}{[Location]}{}{\vspace{1pt}
In progress, expected [Month Year]. [Relevant topics]
}}
```

Any consistent form works: `In progress, expected <Month Year>.` / `Expected completion <Month Year>.` / a date field of `2025–present`.

Claiming a credential not yet held is a factual misstatement, and it is the kind discovered at transcript or reference check rather than at interview. It costs nothing to prevent. The same applies to in-progress certifications and courses.

**Check for agreement:** for a current student, the profile statement, the education entry, and any availability or work-permit note must all give the same completion date. Contradiction between them is worse than any single version.

### Professional Experience
- Rewrite bullet points to emphasize aspects most relevant to the target role
- Use 4-6 bullets for most recent role, 3-4 for previous, 2-3 for older
- **Emphasize measurable results** where possible: "Reduced processing time by X%", "Model adopted by the team"

**Italicize the role-overview line** (the intro sentence(s) before the bullet list in each `\cventry`'s description). Plain-text overview text sitting directly above plain-text bullets reads as one undifferentiated block. Italics separates it typographically at zero page-cost - prefer this over adding `\vspace` before the bullet list, which costs vertical space on an already page-budgeted (2-page) document. Wrap the whole overview sentence(s) in `\textit{...}`.

**Dates: include months, not just years, for any role.** Year-only dates (`2025--2026`) can make a short stint look much longer than it was - Raymond's TELUS Health role is Dec 2025-May 2026 (~5 months), and year-only formatting made it readable as up to two years. Always use `Mon YYYY--Mon YYYY` in the `\cventry` years field (e.g. `Dec 2025--May 2026`). This applies uniformly across all dated roles, not just short ones - consistency matters more than the marginal clutter of a few extra characters on a 5-year role.

**Bold the job title, not the company.** moderncv's banking style defaults to bold company / italic title, which is right for finance-pedigree resumes but backwards for a PM-titled resume: a recruiter scans for the title first, and italics is a lower-emphasis style than bold, so the default visually subordinates the exact word being scanned for. Override per entry rather than fighting moderncv's internal style engine:
```latex
\cventry{Dec 2025--May 2026}{\textbf{\upshape Senior Product Manager, Aging in Place}}{\mdseries TELUS Health}{Vancouver, BC}{}{...}
```
`\upshape` cancels the style's default italic on the title argument; `\mdseries` cancels its default bold on the company argument. Apply this to every `\cventry` in the document (Professional Experience, Earlier Career, and Education) for a consistent single visual anchor per line - don't bold company in some entries and title in others. Regular weight for the company, not semi-bold: the default font (Latin Modern Sans under moderncv/lualatex) has no semi-bold cut, so a true semi-bold would require loading a whole extra font family for one weight - not worth it when a single clean bold anchor (the title) already does the job.

#### Check tenure against visible output

Before finalizing, look at each role the way a stranger will: **date span versus how much work is shown.** A two-year role represented by a single project reads as low output, whether or not that is fair. The reader cannot know what filled the time, so they guess, and the guess is unflattering.

This bites hardest on **career changers** (part of the tenure went into learning the new field), on **long-cycle work** (industrial deployment, clinical or regulatory projects, research — one delivery genuinely takes quarters), and on anyone whose employer kept them on a single account or product.

Three honest fixes, in order of preference:

1. **Surface more real work.** Ask what else the period contained. There are often real secondary projects, internal tooling, or support work that never reached the CV because it felt minor. Best fix when the material exists.
2. **Make the phases within the role explicit.** If the span genuinely had stages, say so — an initial period learning the domain or supporting the team, then ownership of the named work through to delivery. A phased arc reads as a growth curve; an undifferentiated multi-year block reads as stagnation.
3. **Name what made the cycle long.** Data collection from a live environment, validation with domain experts, deployment and iteration against real output. Reviewers who know the domain accept this immediately.

**Never** pad with invented projects, and **never** quietly shorten the employment dates so the ratio looks better. Both are discoverable, and both are worse than the perception problem being solved.

**Prepare the interview answer too.** If a long span against little visible output survives these fixes, the question is coming. The candidate needs a ready two-part answer — what actually filled the time, and what the outcome was — recorded in their interview prep rather than improvised in the room.

### Languages

Keep this to one line. Group every conversational-level language behind a single `Conversational:` label rather than repeating `(conversational)` after each one - e.g. `English (native/professional), Cantonese (native). Conversational: French, Mandarin, Japanese.` List native-level languages individually with their own label (they're the load-bearing claim); only the conversational tier benefits from grouping.

### Earlier Career - date consistency (important)

Every entry in the undated "Earlier Career" block must be treated the same way - **either all entries show years, or none do.** A mix (e.g. one role showing `2002--2011` while others show no years at all) defeats the purpose of the undated convention: a reader can still anchor a rough career-start estimate off the one dated entry, and the inconsistency itself reads as an odd, unintentional slip rather than a deliberate choice. Default to omitting years from every Earlier Career entry, per `09-canada-conventions.md`; if a specific application calls for showing full tenure instead (some employers/recruiters expect it and omission can read as evasive), show it on every entry, not just one.

**Earlier Career section note wording:** keep the italic note under the `\section{Earlier Career}` heading to the plain `Details available on request.` only. Do not include the fuller "Undated per Canadian age-discrimination convention..." explanation on an actual tailored CV - that's the internal rationale (documented in `09-canada-conventions.md`), not something a recruiter needs to read on the page itself. This wording previously leaked from the master reference into a tailored CV verbatim; the master (`main_example.tex`) now uses the same plain wording specifically to prevent that recurring.

### Handling Employment Gaps (Best Practice)
If there is a gap in your employment history:
- The gap should be explained matter-of-factly if needed
- Describe how professional development continued during the gap
- Frame as deliberate skill-building and career repositioning

### Publications
- Include Google Scholar link if applicable
- Select 3-4 most relevant publications (not always all of them)
- For non-academic roles, keep brief

### Evidence Links
Wherever the CV names a verifiable artifact - a public project, a hackathon entry, a publication - carry its link (`\href`) so a reader can verify the claim in one click. A CV whose strongest claims are checkable reads as more credible everywhere else too.

### Honors and Awards
- Keep format brief, one line each

### References
- List 2-4 references with name, title, company, and contact
- End with: "More references are available upon request."
- **Do not attach reference letters** - employers typically contact references directly

## Compile-and-Inspect Loop (MANDATORY)

After writing the CV and before presenting to the user, always compile and visually inspect the PDF. Iterate until the layout is clean. Workflow:

1. Run `lualatex -interaction=nonstopmode main_<company>_<role>.tex`
2. Check the output page count: must be exactly 2
3. Read the PDF via the Read tool and visually inspect both pages
4. Check for **orphaned entries**: a `\cventry` title line must never sit alone at the bottom of page 1 with its bullets on page 2

**Checking page count and running an ATS keyword grep is NOT sufficient to confirm no line wraps.** After every compile, read every bullet, overview line, and insight line individually against its rendered width - a sample check, a page-count check, or a "looks fine" skim is not an acceptable substitute. This has caused repeated user-facing errors when only a subset of lines was checked after a content edit.

### Fixing common page-break problems

**Problem: entry title on page 1, bullets orphaned to page 2**
Add `\needspace{5\baselineskip}` immediately before the problematic `\cventry`:
```latex
\needspace{5\baselineskip}
\item{\cventry{YEAR--YEAR}{Role Title}{Organization}{Location}{}{...}}
```
Include `\usepackage{needspace}` in the preamble.

**Caveat - use `\needspace` before entries, never before `\section` headings.** A section-level `\needspace` pushes the entire section (heading plus content) to the next page whenever the request does not fit, stranding empty space above and typically *adding* a page instead of saving one. Apply it only to the individual `\cventry` that actually orphans, and only after a compile shows the orphan.

**Problem: one trailing section spills to page 3 (e.g., References alone on page 3)**
Add `\enlargethispage{2-3\baselineskip}` before a late section (e.g., before `\section{Honors and Awards}`) to stretch page 2 by a few lines. This is the standard LaTeX rescue for near-miss overflows.

**Problem: 3 pages with significant content on page 3**
Cut content — do not compress geometry or `\vspace`. See "Relevance-weighted cutting" below for the rule.

**Problem: content finishes early on page 2 (feels thin)**
Restore the highest-relevance item that was previously cut — a CV that ends mid-page 2 looks incomplete.

## ATS Parseability

Most employers run CVs through an ATS before a human sees them, and the ATS reads the PDF's embedded **text layer**, not the rendered page. A CV can pass visual inspection and still extract as garbage. After the layout passes the compile-and-inspect loop, verify the text layer:

```bash
cd cv && pdftotext -layout main_<company>_<role>.pdf main_<company>_<role>.txt
```

`pdftotext` comes from [poppler](https://poppler.freedesktop.org/), not the TeX distribution - it is an **optional** dependency, but install it (`winget install oschwartz10612.Poppler` on Windows) rather than skipping the check when it's missing. The visual PDF read is not a substitute: it caught neither the `LOCATION-DOT` icon-glyph garbling nor the `chat-bot` hyphenation break documented above - both were only visible in the actual extracted text layer. If truly unavailable, skip with an explicit warning and note the check wasn't performed, don't silently substitute the visual read as equivalent.

What to check in the extraction:

- **Contact details as literal text.** The stock template's fontawesome contact icons extract as glyph names (`MOBILE-ALT`, `Envelope`) - harmless noise, because the actual address and number are printed beside them. The failure mode is a contact detail carried *only* by an icon or a hyperlink (like the `LinkedIn` link text, whose URL is not in the text layer): invisible to an ATS. The email address must always appear as printed text.
- **No garbled output.** `(cid:NNN)` markers or `�` characters mean a font is embedded without a Unicode mapping - an ATS sees the same garbage. This shows up with unusual fonts in custom templates, not with the stock moderncv setup under lualatex.
- **Reading order.** The stock banking style is single-column, so extraction order matches visual order. Custom templates (via `/add-template`) with sidebars or multi-column layouts can interleave unrelated lines; if extraction order is scrambled, the user is trading ATS compatibility for looks and should be told.
- **Keyword coverage.** Match the posting's required/preferred terms against the extracted text, in the posting's language. Prefer the posting's exact term over a synonym when it is truthfully applicable - ATS matching is often literal. Never add a keyword the profile does not support.
- **Decorative icons that extract as broken glyph names.** Not every `\faIcon{...}` extracts cleanly - `\faIcon{lightbulb}` in the insight-line convention extracts as a real Unicode emoji (harmless), but `\faIcon{location-dot}` in an earlier header version extracted as the literal text `LOCATION-DOT` sitting directly in front of "Vancouver, BC" - a real risk on parsing-fragile platforms like Workday, which sometimes auto-extracts a location field straight from resume text. The fix isn't a better icon, it's asking whether the icon carries real information at all: a location pin doesn't (the text "Vancouver, BC" already says it), so it was simply removed rather than swapped for another icon. Check every icon this way - if `pdftotext` extraction shows something other than the intended emoji or is silent (a blank glyph), and the icon is purely decorative, drop it rather than hunt for a cleaner icon name.
- **Automatic hyphenation can break a keyword across a line-wrap.** LaTeX's hyphenation algorithm inserted a genuine hyphen in "chatbot" - "chat-bot" - purely because it fell at a line-wrap point, not because of anything in the source text. This is invisible in a visual PDF read and only shows up in the actual extracted text layer. A literal ATS keyword search for "chatbot" (candidate-pool search in Greenhouse/Ashby, for instance) could miss that specific instance. Fix with `\hyphenation{chatbot}` in the preamble (add other JD-critical compound keywords there too if a compile-and-extract check catches them mid-hyphenated) - cheaper and more reliable than trying to reword around every possible line-break point.

### Date fields must be ASCII ranges (confirmed ATS import failure)

This one is worth knowing about because it fails **silently**. A CV that passes every other check in this section - clean extraction, no `(cid:)` markers, contact details intact, correct reading order - can still have its dates dropped on import. In a real Workday resume import, a CV built from this template lost the end date of a short contract role and failed to import **any** education entry at all, forcing manual re-entry. Nothing about the PDF or its text layer looked wrong.

Two independent causes, both easy to avoid:

1. **`--` in a `\cventry` date renders as an en-dash (U+2013), not a hyphen.** LaTeX ligatures `--` (two ASCII hyphens, U+002D) into a single en-dash glyph, so `2016--2024` reaches the PDF text layer as `2016<U+2013>2024`. Many parsers split date ranges only on an ASCII hyphen and see no range at all. Write the date argument with a **single hyphen**:

   ```latex
   \item{\cventry{2016-2024}{Role Title}{Organization}{Location}{}{...}}   % parses
   \item{\cventry{2016--2024}{Role Title}{Organization}{Location}{}{...}}  % en-dash, may not
   ```

   This applies to the **date argument only**. Keep `--` everywhere it is typographically correct in prose, for example a numeric range like `EUR 600k--1M`.

2. **A bare single year gives the parser no end date.** A short contract, mandate or internship written as `\cventry{2016}` imports as a start date with nothing to close it. Use an explicit range, with months where the role ran under a year:

   ```latex
   \item{\cventry{Mar 2016 - Jul 2016}{Contract Role}{Client}{Location}{}{...}}
   ```

   Where a genuine range exists, use it even when a single year would be factually accurate - a degree written `1995` is true but imports worse than `1992-1995`. Do not invent a start date you do not have; a lone graduation year is fine, just expect it to be typed in by hand.

**Add this to the step 5d checks**: after extracting the text layer, confirm every experience entry shows a start *and* an end separated by an ASCII hyphen. Because the failure is silent and invisible in the PDF, the candidate otherwise discovers it only while filling in the application form.

## Page Budget - Hard 2-Page Limit

The CV **must** fit on exactly 2 pages when compiled. The per-section numbers below are
default starting guides for reaching that fit, not hard per-section caps. The actual
bullet count per role should follow the relevance-weighted cutting logic and the "Default
retention priority by employer" section further down, which can override these numbers
when a specific JD's fit calls for it — e.g. Impark getting more than 2 bullets if it is
genuinely the strongest match for a given posting, or the most recent role getting fewer
than 4 if most of its bullets score low on relevance. The 2-page total is the hard
constraint; the row-by-row split is a starting point to iterate from.

| Section | Starting guide |
|---------|-----------|
| Profile statement | 3-4 lines |
| Skills | 5 items, each 1-2 lines |
| Most recent role | 4-5 bullets |
| Previous role | 2-3 bullets |
| Older roles | 2 bullets (1 line each) |
| Education | 2-3 entries |
| Publications | 2-3 entries |
| Awards | 3 entries, single line each |
| References | "Available upon request." (single line) |

**If in doubt, cut rather than squeeze.** Reducing `\vspace` or geometry scale to force-fit content makes the CV look cramped.

## Relevance-weighted cutting (the right way to shrink a CV)

**Cut by signal, not by section.** Static priority lists ("remove oldest education first, then shorten the earliest role...") are wrong when a relevant "lower-priority" item is competing with an irrelevant "higher-priority" item. An older-role bullet that speaks directly to the posting is worth more than a recent-role bullet that does not.

For every candidate line, score three things:

1. **Relevance to THIS posting** — does the line hit a named tool, keyword, or stated responsibility in the job ad?
2. **Uniqueness** — is it the only place this claim appears, or is it duplicated elsewhere in the CV?
3. **Narrative load** — does the cover letter depend on it? If cutting the line would force you to rewrite a cover-letter paragraph, it is load-bearing.

Cut the lowest-total-score line first, regardless of which section it sits in.

### Practical order of cuts (easiest → last resort)

1. **Redundancy.** If an achievement appears in both Core Competencies AND a role bullet, the Core Competencies version is usually the cleaner cut (the experience bullet is more concrete evidence).
2. **Profile-statement fluff.** A sentence that just restates what Publications or Skills will show. ("Peer-reviewed publications on X..." is already a Publications entry — profile can claim it once and stop.)
3. **Low-relevance experience bullets.** A bullet about work that does not touch posting keywords, wherever it sits. This cuts across sections before touching the structural list.
4. **Low-relevance supporting content.** An older-role bullet that does not speak to the target role. A certification that does not touch the posting's stack. A language entry that can be condensed to one line.
5. **Low-relevance publications.** Keep 1-2 publications that best match the posting. Cut the rest before touching experience bullets.
6. **Last-resort structural cuts.** Oldest education entry, tightening an older role to 2 bullets, collapsing Certifications into a single line. These only happen if the relevance-weighted cuts above have already been exhausted.

### Pitfalls to avoid

- Do not mechanically cut from the bottom of a static section list without checking relevance. "Cut the oldest role first" is wrong if that role is literally about the skill the posting asks for.
- Do not cut the one concrete example the cover letter leans on. Relevance is measured against the cover letter you wrote, not just the job posting — interviewers will have read both.
- Do not cut to fit if the fit is borderline (2.02 pages). Prefer `\enlargethispage{2-3\baselineskip}` on a late section for near-misses; reserve content cuts for genuine overflow (content on page 3 that is more than a single trailing section).

### Cross-section redundancy cap (distinct from page-budget cutting)

Even a true, relevant claim should not appear in 3+ places across the document. During the 2026-08-06 Microsoft tailoring session, the same claim (a Copilot pilot involving "Microsoft engineers," and "influence without formal authority") each showed up in the profile statement, Core Competencies, and a role bullet — sometimes a fourth time in the insight line. Cap any single specific claim at **2 places**: a Core Competencies keyword line or an insight-line synthesis, **plus** the bullet that proves it with real detail. If a claim already lives in Core Competencies and a bullet, the profile statement should not restate it — give the profile statement's sentence different content instead (a different proof point, or a skill claim the bullet doesn't already carry).

After drafting, do one explicit pass scanning the profile statement, Core Competencies, every insight line, and every bullet against each other for near-verbatim repeated phrases — not just Core-Competencies-vs-bullet, which is the only pair the "Relevance-weighted cutting" section above already checks.

### Verify tenure/duration claims by arithmetic, not by reusing a headline number

When a bullet, competency line, or profile statement states "N+ years" tied to a *specific* title, platform, or skill (as opposed to total career tenure), compute it from the actual date ranges of the roles that involved that specific thing — don't carry forward `01-candidate-profile.md`'s overall "9+ years" figure onto a narrower claim it doesn't support. Example from 2026-08-06: "9+ years owning real-time communications platforms" was wrong — Five9/Talkative ownership was lululemon-only (~4.5–5 years), not the full 9+ year career span. Also check the *title* attached to a duration claim: "Senior Product Manager" was only held for ~5.1 years (lululemon + TELUS Health), not the full ~8-9 years across all PM-titled roles (which also includes Flowfinity's plain "Product Manager" title).

**The target JD's own qualifying language can legitimately broaden the count.** If a JD's required/preferred experience is phrased broadly (e.g. "product/service/program management," not "product management" alone), it's legitimate to include adjacent roles — Imperial Parking's ops/service-management tenure, for instance — toward the total, *if* the CV states the claim in the JD's own broader terms ("years in product, program, and service delivery") rather than as a narrower title-specific claim those years don't all support.

### Claims naming or implying the target company's own staff

When the candidate's documented experience involved working with staff/engineers from the **same company the CV is being submitted to** (e.g., a past vendor pilot with Microsoft, applying to Microsoft), avoid specific-sounding language like "worked directly with Microsoft's engineers" unless the candidate can name the team or individuals if asked in an interview — a claim about the target company's own people is uniquely easy and tempting for them to quietly verify internally. Default to defensible framing that describes the *activity*, not an implied named relationship: "worked with Microsoft's technical team on feature testing," not "worked directly with Microsoft engineers." Apply the same caution anywhere else a claim could be checked against the specific employer being applied to, not just this Microsoft example.

### Overview-line length (the italicized intro under each `\cvoneline`)

Target **1 line** for each role's overview/intro sentence(s), the same "prefer shorter" instinct as the profile statement. Most overview lines can hit this once bullets underneath already carry the supporting detail — if a fact in the overview is already stated in a bullet, cut it from the overview rather than the reverse. Reserve 2-line wrapping for overview lines that are inherently enumerative and would lose real information if compressed: naming several distinct job titles for a career-progression role (e.g. Bell Canada's 5-title progression), or — only if not already covered by the bullets underneath — naming several distinct platforms/systems. Don't force a 2-line-worthy enumeration down to 1 line by deleting a named title or platform; don't leave a compressible prose overview at 2-3 lines when the detail is already redundant with a bullet.

### Run-on scan applies even to text copied from `main_example.tex`

The master reference is not guaranteed run-on-free. Re-check every sentence pulled from it against `03-writing-style.md`'s one-idea-per-sentence rule during tailoring — don't assume inherited text already complies just because it's in the master.

### Default retention priority by employer (Raymond Chu)

Before applying the JD-specific relevance scoring above, start from this default priority
order when trimming `main_example.tex` down for a targeted CV: **lululemon first, TELUS
Health and Flowfinity second, Impark and earlier career last.** lululemon is the longest
tenure, most senior, and most product-relevant role, so it should generally retain the
most bullets. TELUS and Flowfinity are secondary. Impark and earlier career (Preston
Mobility, VANOC, Bell Canada) are the oldest and least product-specific, so they should
generally retain the fewest.

This is a starting prior, not an override of relevance scoring. If a specific JD's
keywords genuinely pull more weight toward an otherwise-lower-priority role (e.g. a
contact-center-operations posting where the Impark QA/SLA story is the single strongest
match on the CV), let that JD-specific relevance win rather than mechanically enforcing
the employer ranking above it.

## Recommended Section Order

The section order varies by role type:

**For technical / data science / ML roles:**
1. Profile statement / elevator pitch
2. Core competencies / Skills
3. Professional Experience (reverse chronological)
4. Education (reverse chronological)
5. Languages
6. Publications & Awards
7. References

**For domain-specific / specialist roles:**
1. Profile statement / elevator pitch
2. Core competencies / Skills
3. Education (reverse chronological) - credentials are a key qualifier
4. Professional Experience (reverse chronological)
5. Publications & Awards
6. References
