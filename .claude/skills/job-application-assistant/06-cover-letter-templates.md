---
framework_version: 1.0.1
---

# Cover Letter Templates and Tailoring Guide

## Template: Custom cover.cls (XeLaTeX)

Cover letters use a custom LaTeX document class (`cover.cls`) with Lato/Raleway fonts.

**Output file:** `cover_letters/cover_<company>_<role>.tex`
**Compile with:** XeLaTeX (cover.cls requires fontspec)

**Export filename (for delivery to Raymond / actual submission):** once a cover letter is finalized, produce a renamed copy of the compiled PDF as `Raymond Chu_Cover Letter-<Role>-<Company>.pdf` alongside the working `cover_letters/cover_<company>_<role>.pdf`, mirroring the CV export-filename convention in `05-cv-templates.md`. Derive `<Role>`/`<Company>` the same way: title-case, acronyms preserved uppercase, spaces instead of underscores. The `cover_<company>_<role>` naming stays the git-tracked working-file convention.
**Font directory:** `cover_letters/OpenFonts/fonts/`

### Compile command

```bash
cd cover_letters && xelatex -interaction=nonstopmode cover_<company>_<role>.tex
```

Expected output: `Output written on cover_<company>_<role>.pdf (1 page, ...)`. Any page count other than 1 is a failure that must be fixed before presenting to the user.

## Compile-and-Inspect Loop (MANDATORY)

After writing the cover letter and before presenting to the user, always compile and visually inspect the PDF. Iterate until the layout is clean:

1. Run `xelatex -interaction=nonstopmode cover_<company>_<role>.tex`
2. Confirm page count is exactly 1 and compile succeeded
3. Read the PDF via the Read tool and visually check: signature fits at the bottom, no text cut off, bullet font matches body
4. **Check every bullet for a line-wrap widow, the same discipline as the CV.** A bullet that wraps to a second line holding only 1-3 words (e.g., "reconciliation." or "cut." alone on line two) reads as unbalanced. Read the extracted or rendered text of each bullet individually - a page-count-only check will miss this, since the letter can compile to a clean 1 page while individual bullets still wrap badly inside it. Trim the bullet to fit one line, or if a 2-line bullet is unavoidable, the wrapped second line must be substantially full (comparable to the CV's 70% rule in `05-cv-templates.md`), not a short widow.

### Known template pitfall: itemize inside `\lettercontent{}`

The `\lettercontent{}` macro appends `\\` to its argument. This breaks when the argument ends in `\end{itemize}` because `\\` has no line to break after the environment closes, producing `! LaTeX Error: There's no line here to end.` and no PDF output.

**Wrong (breaks compile):**
```latex
\lettercontent{Here is how my experience maps:
\begin{itemize}
    \item ...
\end{itemize}}
```

**Correct — close `\lettercontent{}` before the list and wrap the list in the matching Raleway-Medium font so typography stays consistent:**
```latex
\lettercontent{Here is how my experience maps:}

{\raggedright\fontspec[Path = OpenFonts/fonts/raleway/]{Raleway-Medium}\fontsize{11pt}{13pt}\selectfont
\begin{itemize}
    \item ...
\end{itemize}\par}
\vspace{6pt}

\lettercontent{[next paragraph]}
```

The font wrapper is mandatory — if you just move `\begin{itemize}` outside `\lettercontent{}` without the `\fontspec` block, bullets render in the default body font (Lato) and visually mismatch the rest of the letter.

**The `\fontspec` call above must declare `BoldFont`, or every `\textbf{Label:}` inside the bullets silently renders as regular weight.** Confirmed twice (Mercury and Coalition cover letters, both 2026-09-02) - `\fontspec[Path = ...]{Raleway-Medium}` alone loads only the medium weight, so `\textbf{}` has no bold face to switch to and LaTeX substitutes the regular weight with only a compile-time warning (`Font shape ... undefined`) as the tell. `Raleway-Bold.otf` already exists in `OpenFonts/fonts/raleway/`, so the fix is one added key: `\fontspec[Path = OpenFonts/fonts/raleway/, BoldFont = Raleway-Bold]{Raleway-Medium}`. Check the compile log for this specific warning every time a cover letter is built, not just when the bullets look wrong on inspection - the regular-weight substitution is easy to miss on a visual skim.

## Document Structure

```latex
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Cover Letter - [Company], [Role]
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

\documentclass[]{cover}
\usepackage{fancyhdr}

\pagestyle{fancy}
\fancyhf{}

\rfoot{Page \thepage \hspace{0pt}}
\thispagestyle{empty}
\renewcommand{\headrulewidth}{0pt}
\begin{document}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%     TITLE NAME
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\namesection{}{\Huge{[YOUR_NAME]}}{  \href{mailto:[YOUR_EMAIL]}{[YOUR_EMAIL]} | [YOUR_PHONE] |  \urlstyle{same}\href{[YOUR_LINKEDIN_URL]}{LinkedIn}
}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%     MAIN COVER LETTER CONTENT
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

\currentdate{\today}
\lettercontent{Dear [Name/Team],}

\lettercontent{[Opening paragraph - role, connection to background, 2-3 sentences]}

\lettercontent{[Body paragraph - most relevant experience, introducing the bullet list]}

{\raggedright\fontspec[Path = OpenFonts/fonts/raleway/]{Raleway-Medium}\fontsize{11pt}{13pt}\selectfont
\begin{itemize}
    \item [Concrete achievement/skill 1]
    \item [Concrete achievement/skill 2]
    \item [Concrete achievement/skill 3]
\end{itemize}\par}

\lettercontent{[Connection to company - why this role, why this company specifically]}

\lettercontent{[Personal fit paragraph - behavioral strengths, team contribution, 2-3 sentences]}

\lettercontent{I look forward to hearing from you.}

\begin{flushright}
% No trailing \\ inside \closing{} - cover.cls appends its own \\, and a
% doubled break triggers "! LaTeX Error: There's no line here to end."
\closing{Kind regards,}

\signature{[YOUR_NAME]}
\end{flushright}
\end{document}
```

## Key Commands Reference

| Command | Purpose |
|---------|---------|
| `\namesection{}{Name}{contact info}` | Header with name and contact |
| `\currentdate{date}` | Date field (use `\today` or explicit date) |
| `\lettercontent{text}` | Body paragraph (adds spacing after) |
| `\closing{text}` | Closing line |
| `\signature{name}` | Printed name below signature |

## Tailoring Guidelines

### Recipient block and contact line (Raymond's finalized format)

Based on the version actually submitted for the StackAdapt application, use a formal left-aligned recipient block above the salutation, and show the full LinkedIn URL as visible text rather than just a "LinkedIn" hyperlink label (better for ATS - a contact detail carried only by anchor text, not the literal URL, doesn't index cleanly on parsers that don't extract hyperlink annotations):
```latex
\namesection{}{\Huge{[YOUR_NAME]}}{  \href{mailto:[EMAIL]}{[EMAIL]} | [PHONE] |  \urlstyle{same}\href{[LINKEDIN_URL]}{linkedin.com/in/[YOUR_HANDLE]}
}

{\raggedright\currentdate{[Month DD, YYYY]}}
\companyname{Hiring Team}
\companyaddress{[Company] \\ Re: [Role Title]}

\lettercontent{Dear [Company] Hiring Team,}
```
`\currentdate` defaults to `\raggedleft` (right-aligned) in `cover.cls` - override to `\raggedright` as shown so the date sits with the rest of the left-aligned block, matching a traditional formal business-letter layout. `\companyname{}` and `\companyaddress{}` are existing `cover.cls` commands - use them for this block rather than inventing new formatting.

### Salutation
- If you know the hiring manager's name: "Dear [First Last],"
- If you know the team: "Dear [Company] hiring team,"
- Generic: "Dear [Company]," (avoid "To whom it may concern")

### Length - Hard 1-Page Limit
- Target: 1 page including signature block
- Maximum: **never exceed 1 page**
- **Word budget: 250-300 words** of body text (not counting LaTeX markup). This is the safe maximum. 350 words will overflow.
- **Always count**: opening paragraph + bullet list paragraph + closing paragraph = 3 blocks. Add a 4th only if the others are short.
- When adding company-specific content, trim other content to compensate rather than adding net length

### Word-count gate (MANDATORY — before presenting to the user)
Fitting on 1 compiled page is not the same check as staying inside the
250-300 word budget — a letter can compile to 1 page while sitting well
over budget, or one large dense paragraph can hide a total near the
350-word ceiling. Before showing a draft (first draft or a revision) to
the user, count the words in the body text and state the count. This is
the cover-letter equivalent of the CV's page-count check and is just as
mandatory.

### Don't run bullets and prose in parallel
Pick one mode: prose-only paragraphs, or short paragraphs plus a bullet
list. Do not describe the same achievement in a flowing paragraph and
then repeat it in a bullet — that's not more evidence, it's the same
evidence twice, and it's the fastest way to blow the word budget without
noticing. If bullets are used, the surrounding paragraphs should
introduce and connect them, not restate their content.

### Paragraph density
Keep each paragraph to **2-3 sentences, 3-5 lines max**, readable in about 10 seconds. A paragraph running to 4-5 sentences reads as a dense block even when the letter as a whole is within the word budget - total word count and per-paragraph density are different checks, and a letter can pass the first while failing the second. Each paragraph should center on one idea: a strong topic sentence, one or two supporting sentences, done. Leave a full blank line between paragraphs so the page reads as distinct, scannable blocks rather than one continuous wall of text.

When a paragraph runs long, the fix is to **cut content**, not to split it into more, shorter paragraphs - splitting keeps every word but dilutes the letter's structure (a 3-4 paragraph cover letter is itself a best-practice target, so fragmenting into 6-7 paragraphs to solve density trades one problem for another). Identify the least load-bearing sentence in the dense paragraph (often a summary/restatement sentence that doesn't add new information) and cut it outright.

### Closing paragraph structure
The closing paragraph needs to do more work than a single "I look forward to hearing from you" line - that alone reads as a placeholder, not a close. A proper closing is **2-4 sentences, roughly 50-75 words**, and covers:
1. A brief restatement of the value you bring (don't just repeat the opening - tie back to the specific role)
2. Genuine, specific excitement about this opportunity or company - ideally something concrete (a verified company fact, mission detail, or structural distinction), not generic enthusiasm
3. A clear, confident call to action (welcoming the chance to discuss the role, not a vague hope)
4. Thanks for the reader's time and consideration
Match the tone of the rest of the letter and keep the sign-off professional ("Kind regards," / "Sincerely," / "Best regards," are all safe).

### Line Spacing
- Add `\usepackage{setspace}` and `\setstretch{1.0}` if the letter is long and needs to fit on one page
- Use `\vspace{.5cm}` between major sections for readability (only if space permits)

### Bullet Lists
- Place `\begin{itemize}...\end{itemize}` **outside** a `\lettercontent{}` block (see "Known template pitfall" above), wrapped in the matching Raleway-Medium `\fontspec` so the bullet font matches the body
- 3-5 bullets is ideal
- Start each bullet with bold label or action verb
- Use `\textbf{Label:}` for category-style bullets
- Each bullet should be one sentence (two only if it truly can't be said in one), never exceeding two lines, and all bullets in the same list should read as parallel in length and grammatical structure - one noticeably longer or differently-shaped bullet stands out as unbalanced next to short, punchy ones.

### Don't duplicate resume content
Do not repeat resume bullets verbatim in the cover letter, and do not simply restate a resume achievement in prose form either - both waste the one page available to make a distinct case. Two legitimate options instead:
1. **Use different achievements entirely** - pull KB facts that never made it onto the tailored resume.
2. **Reuse the same achievement but add real context the resume doesn't have** - the mechanism behind a number, the specific stakeholder story, why it mattered. A resume bullet states an outcome; a cover letter can explain how it happened.
Before finalizing bullet or paragraph content, check it against the tailored CV for this same application - if a sentence could be lifted straight from one document into the other with no change, it needs either different content or genuinely new detail, not a synonym swap.

### Bullet framing at the Director/senior level
Task-execution verbs ("closed," "fixed," "built") read as individual-contributor work even when the underlying achievement is substantial. For Director-level or senior-leadership target roles specifically, prefer ownership and direction language ("owned," "led," "built the case that got...") over pure task-completion phrasing - the same outcome/translator-framing principle documented in `05-cv-templates.md`'s Pre-Drafting Checklist, applied to cover letter bullets. This matters more here than on the CV because a cover letter has only 3-5 bullets total, so each one needs to read as scope-appropriate on its own, not rely on surrounding bullets to establish seniority.

### Choosing which achievements to feature (limited slots, prioritize deliberately)
With only 3-5 bullets available, an achievement that maps to one of the JD's explicit **Required Skills/Qualifications** generally outranks one that only illustrates a "typical day" responsibility area - the required-qualifications list is the hard-screen checklist a recruiter or ATS is actually checking candidates against, while a responsibilities section describes role scope more loosely. When two candidate KB facts are otherwise comparable in strength, the one demonstrating a named requirement should usually win the limited slot.

### LaTeX Special Characters

| Character | Write | Typical trigger |
|---|---|---|
| `&` | `\&` | company names: Bang \& Olufsen, H\&M |
| `%` | `\%` | quantified achievements: "cut latency by 40\%" |
| `$` | `\$` | salary and cost figures |
| `#` | `\#` | "ranked \#1" |
| `_` | `\_` | file names, code identifiers |
| `~` | `\textasciitilde{}` | URLs, "approx." tildes |
| `^` | `\textasciicircum{}` | version strings |

Two failure modes deserve special care:
- **`%` fails silently.** An unescaped `%` starts a LaTeX comment: the compile succeeds with zero errors, and everything after the `%` on that line vanishes from the PDF. Check every `%` in every bullet before compiling.
- **`&` fails loudly** (alignment-tab errors, `Missing } inserted`) - the compile loop catches it, but escape company names up front rather than debugging the compile.

A bullet whose text begins with a literal `[` must be braced: `\item {[text]}`. Unbraced, LaTeX parses `[text]` as `\item`'s optional label and renders it off the left page edge, missing from the PDF text layer entirely.

### Non-English Cover Letters
- Same template structure, just write content in the posting's language
- Adjust date format to local convention
- Adjust closing to local convention (e.g. "Med venlig hilsen," for Danish)

## Checklist Before Finalizing
- [ ] No em-dashes (use commas or periods instead)
- [ ] No long run-on sentences (a sentence chaining 2-3 ideas together with commas and "and"/"then" is a run-on even if grammatically legal, per `03-writing-style.md`)
- [ ] No cliches or empty filler
- [ ] Every claim backed by specific example
- [ ] Forward-looking framing: focuses on tasks you'll solve, not just past duties
- [ ] Motivation section references this specific company's mission/values
- [ ] Company name and role are correct throughout
- [ ] Date is current
- [ ] Fits on one page
- [ ] Language matches the job posting language
- [ ] Salutation is appropriate (named person if possible)
- [ ] Headline is engaging and specific, not generic

## Submission Guidelines (Best Practice)
- Submit only the documents the employer requests
- Export as PDF to preserve formatting
- Name files clearly: "[Your Name] CV" and "[Your Name] Cover Letter"
- Follow all employer instructions regarding anonymity or specific materials
