# Interview Prep — STAR Story Bank (Raymond Chu)

Usage: pull stories in full STAR format (never abbreviate the Action step —
that's where the behavioral signal lives). Map to the likely question using
the "Use For" tags. Only cite metrics labeled [CONFIRMED], [EST], or
[CALCULATED]. Never state a [MISSING] metric as if it were confirmed — say
it's not available and ask Raymond before inventing a placeholder. If a
likely question has no strong story, say so plainly rather than stretching
a weak-fit story to cover it.

Baseline metrics (floor, not ceiling): CX adoption +40% | Efficiency
+25–30% | GenAI pilot 60% manual effort reduction | Churn reduction 60% |
License growth 25% | Admin work -30% | SLA improvement 30% | Hardware:
1,200+ units, 900+ staff NA

---

## Story Index by Competency

| Competency | Best Story | Backup |
|---|---|---|
| Technical Leadership / API | Educator Booking API | PCI Pal DTMF API |
| AI / Innovation | AI IVR Rollout | GenAI Pilot |
| AI Governance / Go-No-Go | Copilot Pilot | GenAI Pilot |
| 0-to-1 Execution | TELUS AiP Expansion | Product-in-a-Product |
| GTM / Adoption | Product-in-a-Product | Quarterly Planning Leadership |
| Technical PM / Compliance | PCI Pal DTMF API | D365 Stabilization |
| Security / PCI | PCI Pal DTMF API | D365 Stabilization |
| Scale / Infrastructure | Work-at-Home Hardware | Quarterly Planning |
| Proactive Initiative / No Brief | Medallia & Web Forms | AI IVR Rollout |
| Contact Center QA | Impark QA Ownership | — |
| Expectation-Setting / Pushback | Metro Mobile License Growth | Membership Enrollment |
| OKR / Cross-Org Planning | Quarterly Planning Leadership | TELUS AiP Expansion |
| Ecommerce Ownership | NARVAR–Quiq Integration | Educator Booking API |
| Agency / SOW Delivery | Flowfinity Consultant Billing | — |
| Managing/Mentoring PMs | PM Mentorship | Quarterly Planning Leadership |
| Onboarding-Stage Client Rescue | Second Harvest Rescue | Metro Mobile License Growth |
| Billing / Financial Data Pipelines | Return Fraud & Tax Reconciliation | PCI Pal DTMF API |
| Platform Rebuild / Re-Architecture | Educator Booking API (Acuity rebuild) | OSB-to-Kafka Backend |
| Early-Career / "How Did You Start" | Bell National Billing Rollout | — |

**Known gaps — ask Raymond before claiming these:** conflict resolution
(no true interpersonal-conflict story yet), data-analytics deep dive (a
time data changed direction or killed a feature), full onboarding-funnel
instrumentation built from scratch (membership enrollment story is a
partial fit only).

---

## Story: Educator Booking Automation (API Workflow)
**Company:** lululemon | **Competencies:** Technical leadership, platform
rebuild/re-architecture, API strategy, workflow automation, WFM efficiency

**Situation:** Before any automation work began, the existing Acuity setup
had been configured by a small business account team and an unsupervised
lululemon employee, with no product oversight. Separately, 70+ digital
educators each spent ~1 hour per booking manually emailing clients,
scheduling in Acuity, and setting up a Talkative video session. WFM then
manually matched an educator by shift — consuming 60+ hours/week.

**Task:** Bring Acuity under real product ownership, then eliminate the
manual coordination across educators, WFM, and clients.

**Action:** Rebuilt the Acuity setup properly — both booking configuration
and the integration/API layer — before any automation began. Reframed the
problem from a tool issue to a workflow automation opportunity. Partnered
with Engineering to build an API chain: client books → email sent
automatically → Talkative session created → on-shift educator assigned by
availability. Separately led a redesign of the booking page layout,
shipped alongside the API work.

**Result:** Educator time per booking dropped from 60 to 15 minutes (75%
reduction) across 70+ educators. WFM reclaimed 60+ hours/week. Combined
estimated labor savings ~$200K+ CAD/year. Booking conversion rose from
under 3% to over 10% within 30 days of the redesign and API shipping
together (attribution between the two changes is a hypothesis, not a
measured split). Contributed to $10M+ in Guest Services sales the
following year (directional, not isolated). The Acuity/Talkative API was
later reused by the WFM team for shift scheduling, integrated into
Verint.

**Metrics:** 75% time reduction [CONFIRMED] | 60+ hrs/week WFM savings
[CONFIRMED] | 70+ educators [CONFIRMED] | ~$200K+/yr [CALCULATED] |
conversion 3%→10%+ in 30 days [CONFIRMED] | $10M+ sales contribution
[CONFIRMED — directional attribution]

**Soundbite:** "What looked like a scheduling tool problem was a $200K+
annual labor drain. I rebuilt an ungoverned Acuity setup, then led an API
automation across booking, video, and shift management that cut educator
prep time by 75% and freed WFM entirely from manual scheduling, across 70+
digital educators."

**Use for:** technical leadership, API strategy, inheriting/re-architecting
an ungoverned system, reusable platform components.

---

## Story: AI IVR Rollout (Murf.ai + Five9 — Global)
**Company:** lululemon | **Competencies:** AI implementation, proactive
opportunity identification, legal/compliance navigation, global rollout
sequencing, vendor negotiation, call deflection

**Situation:** The internal EHC tech support line commissioned a fix for
its volunteer-dependent IVR recording process (multi-day, 4-6 hrs per
update). No one had connected it to the identical guest-facing IVR
problem.

**Task:** Deliver the EHC fix; independently identify and build the case
for expanding it guest-facing.

**Action:** Delivered the EHC fix using Murf.ai integrated into Five9,
cutting the update cycle from multi-day to under an hour. Proactively took
the guest-facing application through legal and branding approval without
being asked, pre-negotiated vendor pricing, and designed a phased global
rollout: EHC → AU/NZ → APeC → EMEA (NA scoped next at time of departure).
Established a reusable regional implementation pattern at each stage.

**Result:** Turned a single internal fix into a four-region enterprise AI
voice program. Enabled same-day emergency IVR updates for guest-facing
incidents, turning IVR into a proactive call-deflection tool.

**Metrics:** ~85% cycle time reduction [CALCULATED EST] | multi-day → under
1 hour [CONFIRMED] | 4 regions sequenced [CONFIRMED] | legal/branding
approval secured proactively [CONFIRMED]

**Soundbite:** "I was asked to fix one internal phone line. I recognized
the broader opportunity, took it through legal and branding myself,
negotiated vendor pricing, and turned it into a four-region global AI
voice rollout, without anyone asking me to."

**Use for:** proactive initiative, AI implementation, global rollout
sequencing, vendor negotiation.

---

## Story: Product-in-a-Product (Customer Health Tracking App)
**Company:** Flowfinity | **Competencies:** 0-to-1 execution, GTM, customer
success, data-driven prioritization, churn management

**Situation:** Flowfinity was in high-growth with no centralized way to
track customer health or product usage. Sales had zero visibility.

**Task:** Build a solution enabling proactive churn management and
data-driven prioritization.

**Action:** Built a customer health-tracking app on Flowfinity's own
platform within 60 days. Trained the sales team on adoption and
data-entry discipline. Used the app to weight feature requests by ARR
impact.

**Result:** Reduced account churn by 60%. Enabled ARR-weighted roadmap
prioritization.

**Metrics:** Churn reduction 60% [CONFIRMED] | built in 60 days [CONFIRMED]

**Soundbite:** "I built a customer success app early on, trained sales to
use it, and it evolved into a key system for tracking feature requests and
prioritizing based on real customer impact."

**Use for:** 0-to-1 execution, GTM, customer success, building on your own
platform.

---

## Story: D365 Stabilization, Sunset & PCI Compliance
**Company:** lululemon | **Competencies:** Technical PM, CRM stabilization,
compliance, security, stakeholder consensus

**Correction — do not use old framing:** Raymond did NOT manage or own the
OSC → D365 → Salesforce migration. He stabilized D365 after migration and
owned its sunset/deprecation in the final year, while a separate team
built Salesforce Service Cloud.

**Situation:** D365 was added to Raymond's portfolio in his final year
specifically for stabilization and deprecation, while global CRM data
pipelines and PCI compliance needs continued across jurisdictions. Design,
Tech, and Legal needed consensus on the broader CRM operating model.

**Task:** Stabilize D365, run its sunset program, and ensure security
compliance and zero-downtime service while a separate team built the
replacement.

**Action:** Stabilized D365 for North America and managed its deprecation
timeline. Managed PCI Pal security audits across jurisdictions. Built
consensus across Design, Tech, and Legal on stabilization and sunset
priorities.

**Result:** 100% security compliance maintained. CX platform adoption
increased 40% globally. Zero downtime for global support teams throughout.

**Metrics:** Security compliance 100% [CONFIRMED] | Platform adoption +40%
[CONFIRMED]

**Soundbite:** "In my final year, D365 landed on my plate for stabilization
and sunset, not to build its replacement. I stabilized it for North
America, ran the deprecation timeline, and kept us at 100% PCI compliance
throughout, while a separate team built Salesforce Service Cloud."

**Use for:** technical PM, compliance, CRM stabilization, cross-functional
consensus-building.

---

## Story: Generative AI Pilot (Internal Knowledge Retrieval)
**Company:** lululemon | **Competencies:** GenAI/AI innovation, operational
efficiency, automation

**Situation:** Guest support teams were overwhelmed with manual data
discovery and repetitive queries, slowing response times.

**Task:** Find scalable automation for internal knowledge surfacing
without significant engineering lift.

**Action:** Led a pilot for GenAI/LLM tools to automate internal data
discovery and knowledge base surfacing. Managed vendor evaluation, pilot
design, and rollout.

**Result:** 60% reduction in manual workflow effort for internal agents.
Improved guest discovery speed.

**Metrics:** Manual effort reduction 60% [CONFIRMED]

**Soundbite:** "I leveraged LLMs to automate internal knowledge retrieval,
turning a manual research process into an automated workflow that saved
60% of agent effort."

**Use for:** GenAI/AI innovation, operational efficiency, vendor
evaluation.

---

## Story: PCI Pal DTMF & Refund API
**Company:** lululemon | **Competencies:** Security compliance, API
integration, PCI, systems thinking, risk mitigation

**Situation:** Educators were taking guest credit card info verbally over
phone/chat to process refunds, a direct PCI violation. Refunds also
required manually swivel-chairing between PCI Pal and the CRM.

**Task:** Eliminate the PCI risk, automate the refund workflow, keep the
experience seamless for guest and educator.

**Action:** Partnered with Engineering to build a PCI Pal–CRM API
integration with DTMF keypad entry. Guests enter card digits on their
phone keypad, masked from the educator entirely. The API then triggers the
refund automatically in the CRM.

**Result:** Full PCI compliance achieved. Automated refund generation
removed the manual multi-system workflow. Per-transaction time dropped
from ~10 min to ~3 min (70%). Scaled to hundreds of transactions/week
globally. PCI Pal maintained 100% uptime throughout Raymond's tenure and
served a second live use case: CS-assisted guest order payment
processing.

**Metrics:** ~70% time reduction [CONFIRMED] | hundreds of
transactions/week [CONFIRMED] | 100% uptime [CONFIRMED] | second use case
confirmed [CONFIRMED]

**Use for:** security/PCI compliance, technical PM, API integration,
payments infrastructure reliability.

---

## Story: TELUS — C-Suite Approval for AiP Program Expansion
**Company:** TELUS Health | **Competencies:** 0-to-1 strategy, market
research, executive influence, pilot design, IoT, vendor sourcing

**Situation:** TELUS Health's Aging in Place program relied on a
pendant-based fall-detection solution, limited in scope and underperforming
in market penetration. Canada's aging population represented a
significant untapped opportunity.

**Task:** Identify the right technology pivot, validate the market
opportunity, and build a case for program expansion with C-suite.

**Action:** Conducted market research on Canada's aging population and the
pendant model's limitations. Identified ambient sensing as the technology
that could solve for nighttime falls and broader willingness-to-pay.
Defined pilot requirements. Designed and ran an Innovation Day event to
source vendor partners. Built and presented the business case for C-suite
approval.

**Result:** Received C-suite approval to expand the AiP program. Pilot
launched to validate ambient sensing use cases.

**Metrics:** C-suite approval secured [CONFIRMED] | Pilot launched
[CONFIRMED] | Hard outcome metrics [MISSING — pilot in progress, role
ended before results]

**Soundbite:** "I identified that TELUS Health's pendant solution was too
narrow for Canada's aging population opportunity. I researched the
market, reframed the product around ambient sensing, ran an Innovation Day
to source pilot vendors, and secured C-suite approval to expand the
program."

**Use for:** 0-to-1 strategy, market research, executive influence, IoT.

---

## Story: Medallia Survey Recovery & Returns Web Form Restoration
**Company:** lululemon | **Competencies:** Proactive problem
identification, initiative without a brief, technical remediation, Peak
season delivery

**Situation:** When D365 was added to Raymond's portfolio for deprecation,
he discovered two critical systems broken since the original D365
implementation, Medallia post-interaction survey triggers and guest-facing
returns web forms, both dormant over a year. Nobody had flagged them. The
broken web forms forced all guest returns submissions through the GEC
manually.

**Task:** Not formally assigned — identified both issues independently and
took ownership.

**Action:** Rebuilt Medallia post-interaction survey triggers using D365,
Five9, and Medallia configuration. Migrated guest-facing returns web forms
from Oracle-hosted to Microsoft-hosted infrastructure. Managed both
workstreams simultaneously, launched before Peak season.

**Result:** Both systems restored and functioning before Peak, without
being asked.

**Metrics:** Dormant >1 year prior [CONFIRMED] | delivered before Peak
[CONFIRMED]

**Use for:** proactive initiative with no brief, technical remediation,
ownership without formal assignment.

---

## Story: Second Harvest Onboarding Rescue
**Company:** Flowfinity | **Competencies:** Client relationship
management, onboarding-stage rescue, SOW structuring

**Situation:** A new client (~2 months into onboarding) was at risk of
churning. They had no working prototype, felt over their head configuring
and building their own apps, and hadn't expected that level of hands-on
self-build involvement when they signed on.

**Task:** Prevent early-stage churn and get the client to a working
rollout before the relationship soured further.

**Action:** Took over day-to-day management of the client relationship.
Diagnosed that the client needed more hands-on help than the standard
engagement included, and structured a SOW for supplemental billable
consulting and dev hours. Brought in pilot users from the client's own
team for faster, more relevant feedback. Drew on his own prior
client-side experience to better translate their needs into the solution.

**Result:** The account did not churn. Second Harvest remained a Flowfinity
client long-term.

**Metrics:** Client tenure at intervention ~2 months [CONFIRMED] |
long-term retention [CONFIRMED]

**Soundbite:** "Second Harvest was two months in and already frustrated.
They didn't expect to be building their own apps, and they didn't have
anything working yet. I took over the relationship, realized they needed
more hands-on help than the standard engagement gave them, and set up a
SOW for extra consulting hours. They stayed with us long-term after
that."

**Use for:** onboarding-stage client rescue, relationship management, SOW
structuring.

---

## Story: lululemon Return Fraud Prevention & Regional Tax Reconciliation
**Company:** lululemon | **Competencies:** Billing administration,
financial data pipelines, fraud/risk controls, policy-to-system
translation

**Situation:** lululemon's returns process auto-refunded guests as soon as
a return shipping label was scanned, with no check that the returned item
matched the purchase, a known, exploited vulnerability (guests could send
back rocks or unrelated items and still get a full refund). Separately,
refund amounts weren't correctly broken out by regional tax (EMEA/APeC),
forcing Accounting to reconcile manually.

**Task:** Close the fraud gap and fix the refund calculation logic so
Accounting could reconcile without manual work, across multiple
currencies and tax regions.

**Action:** [See KB for full action detail if this becomes a focus story —
confirm specifics with Raymond before using in a live interview.]

**Result:** Fraud vulnerability closed. New fields and calculation logic
added to correctly break out EMEA/APeC regional tax on refunds, enabling
full accounting reconciliation and reducing manual work.

**Metrics:** [CONFIRMED — fraud gap closed and reconciliation logic
shipped; ask Raymond for any quantified fraud-loss-prevented or
manual-hours-saved figure before citing a number]

**Use for:** billing/financial data pipelines, fraud prevention,
policy-to-system translation.

---

## Story: Bell Canada — National Billing System Rollout & Training
**Company:** Bell Canada | **Competencies:** Early-career technical
aptitude, train-the-trainer, national rollout support

**Situation:** Raymond was part of the inaugural training class at Bell's
newly opened Vancouver call centre, early in his career as a Customer
Service Representative. Bell was rolling out a new national billing system
and needed frontline input from regional call centres during testing.

**Task:** Represent the Vancouver call centre in national billing system
testing at Bell's Toronto HQ, then bring the system back and get the local
team ready.

**Action:** Traveled to Toronto for national testing alongside reps from
other regions. Upon returning to Vancouver, trained 200+ agents on the
new system ahead of local rollout.

**Result:** Vancouver's rollout succeeded on the strength of this training
work. This early recognition marked the start of a path through 4
additional roles at Bell, ultimately reaching Store Manager.

**Metrics:** 200+ agents trained [CONFIRMED] | selected as sole Vancouver
rep [CONFIRMED]

**Soundbite:** "Early in my career, I was picked to represent our
Vancouver call centre at Bell's Toronto HQ for national billing system
testing. I came back and trained over 200 agents on the new system before
rollout. That was the first time I understood what it meant to be the
bridge between a big system change and the people who had to use it every
day."

**Use for:** early-career opener, "how did you get your start," career
progression narrative. Not a substitute for a primary competency story on
a senior PM application — use to open, then pivot to a PM-era story.

---

## Story: Membership Enrollment — Discovery to Iteration
**Company:** lululemon | **Competencies:** Discovery, expectation
calibration, cross-functional negotiation (Ops), iteration based on data,
change management with frontline staff, UX partnership

**Situation:** While shadowing educators in his first year, Raymond
identified that Guest Services had no path into the membership program at
all, despite constant guest touchpoints across phone, chat, email, and
video. Discovery with the membership team and manual analysis of the
prior 30 days of guest interactions showed approximately 40% of guests
engaging with Guest Services were not already enrolled in membership.

**Task:** Design and scope a CRM-based enrollment capture workflow, and
set a credible capture target for that 40% non-enrolled population.

**Action:** Initially targeted capturing 70-80% of the 40% gap. After
further discovery with Operations, learned educators were concerned the
added consent step would hurt performance metrics like Average Handle
Time, and flagged training gaps on how to position membership.
Recalibrated the target down to ~50% of the 40% gap based on that input.
Ops pushed back on making consent fields mandatory, so the workflow
launched optional first. After one month live, the team confirmed optional
fields weren't providing enough granularity into why guests were
declining. In the first sprint of month two, shifted to mandatory fields
with a required decline reason. Separately, UX partnership identified
friction in the consent step, producing a small AHT improvement (~2-3%),
directly addressing the original educator concern about handle time.
Built short demo videos showing exactly where the consent ask sat in the
workflow (10-15 seconds) and ran roleplay training with educators.

**Result:** After iteration (mandatory fields, UX-driven workflow
tightening, educator training), enrollment capture reached approximately
80% of the original 40% non-enrolled gap, contributing to 30,000+ total
enrollments in 6 months.

**Metrics:** Initial gap ~40% [CONFIRMED] | initial target 70-80%
[CONFIRMED] | recalibrated target ~50% of the gap [CONFIRMED] |
optional-to-mandatory shift ~1 month after launch [CONFIRMED] | AHT
improvement ~2-3% [CONFIRMED] | final result ~80% capture of the 40% gap
[CONFIRMED] | total enrollments 30,000+ in 6 months [CONFIRMED]

**Soundbite:** "I was optimistic early, thought we could capture 70-80% of
the gap. Once I dug into Ops concerns about handle time and training gaps,
I recalibrated to a more realistic number and launched with optional
fields first. After a month, the data confirmed what I'd flagged early on,
optional fields didn't tell us why guests were declining. We moved to
mandatory fields in the first sprint of month two, partnered with UX to
tighten the workflow, which actually improved handle time slightly rather
than hurting it, and used short demo training to show educators it only
took 10-15 seconds. We ended up capturing about 80% of the original gap."

**Use for:** iteration based on data, expectation calibration, negotiating
with a skeptical stakeholder team, UX partnership. This is the deep-dive
version — use for STAR-format questions specifically; the shorter summary
lives in 01-candidate-profile.md for elevator-pitch framing.

---

## Story: Impark QA Ownership
**Company:** Imperial Parking (now Reef Technology) | **Competencies:** Contact center
QA, scorecard design, calibration facilitation, coaching frameworks,
people leadership

**Situation:** Post-acquisition, Impark's contact center needed a
functioning quality program alongside CRM and billing integration work.
Raymond was one of two managers responsible for the entire contact center
operation.

**Task:** Own the QA program, including scorecards, calibrations, and
coaching workflows, across 7 supervisors and 100+ agents.

**Action:** Designed and maintained call quality scorecards and evaluation
frameworks. Led calibration sessions with 7 supervisors to align scoring
standards and coaching approaches. Built on earlier Bell Mobility
experience as a frontline agent with direct call quality responsibilities.

**Result:** Improved SLA performance by 30%. Improved new-hire retention
by 60%. Established consistent quality standards across a post-M&A
contact center spanning 400+ cities.

**Metrics:** SLA improvement 30% [CONFIRMED] | retention improvement 60%
[CONFIRMED] | 7 supervisors led through calibrations [CONFIRMED] | 100
core + 20 specialized staff under direct responsibility [CONFIRMED]

**Use for:** contact center QA, people leadership at scale, SLA
management, onboarding/retention process design.

---

## Story: Copilot for D365 Pilot (AI Governance / Go-No-Go)
**Company:** lululemon | **Competencies:** AI pilot governance, Microsoft
partnership, executive communication, protecting business over optics

**Situation:** Raymond was handed a Copilot for D365 pilot (email/chat
summarization for GEC educators) roughly one month before Peak season,
with no extra runway.

**Task:** Design and run a full pilot evaluation in a compressed timeline
and deliver an honest recommendation, not just a rubber-stamped rollout.

**Action:** Designed and ran the full pilot evaluation framework in weeks.
Worked directly with Microsoft engineers and product teams to communicate
test results and fix requests. Partnered with Tech, Legal, and Operations
on compliance and performance risk.

**Result:** Delivered a clear go/no-go recommendation, deprioritized ahead
of Peak when the pilot did not meet the minimum performance bar and
Microsoft could not commit to a fix timeline. Protected the business over
the optics of shipping something unready.

**Metrics:** Full pilot designed and evaluated in weeks [CONFIRMED] |
go/no-go delivered to senior stakeholders [CONFIRMED] | deprioritized on
performance grounds [CONFIRMED]

**Soundbite:** "I was handed a Copilot pilot a month before Peak with no
runway. I designed the full evaluation framework, worked directly with
Microsoft engineers, and when it didn't meet the bar and they couldn't
commit to timelines, I recommended we don't ship it. Protecting Peak was
the right call."

**Use for:** AI governance/go-no-go, Microsoft platform experience,
protecting business over optics. Not a strong fit for "tell me about a
personal mistake" questions, the decision itself was correct, not a
failure — use Metro Mobile License Growth or Membership Enrollment for
those instead.

---

## Story: Global Work-at-Home Hardware Ecosystem
**Company:** lululemon (2020-2021) | **Competencies:** 0-to-1 execution,
hardware/vendor management, executive buy-in, MDM, budget ownership

**Situation:** COVID-19 forced an immediate shift to remote work at
lululemon in 2020. Global hardware supply chains were frozen. No remote
work infrastructure existed when Raymond joined the effort.

**Task:** Standardize remote hardware across USA/Canada for 900+ staff
from scratch, under supply constraints, requiring executive budget
approval.

**Action:** Sourced vendors across a constrained market. Selected Lenovo
Mini-PCs, monitors, and peripherals as the standard kit. Partnered with IT
Infrastructure on standardized imaging and remote MDM deployment via
Microsoft Intune. Built the $2.2M business case and secured OpsCo/SteerCo
approval.

**Result:** Deployed across North America before Peak 2021. Scaled to
1,200+ users by 2024. Became the permanent standard for all remote staff.

**Metrics:** Launch deployment 900+ staff [CONFIRMED] | scaled to 1,200+
[CONFIRMED] | $2.2M budget secured [CONFIRMED] | deployed before Peak 2021
[CONFIRMED] | became company permanent standard [CONFIRMED]

**Soundbite:** "In the middle of a global hardware shortage, I built
lululemon's remote work infrastructure from scratch, sourced vendors,
standardized Lenovo kits with MDM imaging, secured $2.2M OpsCo/SteerCo
approval, and deployed 900+ staff before Peak 2021. It scaled to 1,200+
and became the company standard."

**Use for:** scale/infrastructure, 0-to-1 execution under constraint,
executive budget approval, vendor management.

---

## Story: Metro Mobile License Growth (Pushback / Mistake / Learning)
**Company:** Flowfinity | **Competencies:** Expectation-setting, client
discovery, pricing model innovation, pushing back on a stakeholder

**Resume rule:** never frame as a resume bullet, it surfaces pushback on a
colleague that reads poorly without context. Use only the licensing model
outcome and account growth metric on a resume if needed; keep the pushback
narrative interview-only.

**Situation:** A sales manager tasked Raymond with growing Metro Mobile's
license count from 150 to 100% of their 300-person team within 2 months.
When asked what the target was based on, the sales manager had no data
behind the number, it was an arbitrary ask.

**Task:** Push back on an unfounded target while still finding a credible,
evidence-based path to real growth, rather than simply refusing outright.

**Action:** Told the sales manager directly the 2-month/100% target wasn't
realistic as stated. Proposed meeting the client first to build rapport
and pull real usage data before committing to any revised number. Met with
the client's owner and operational leads, shadowed their teams, and ran
discovery sessions. Found license growth was running ~10/month
historically, with adoption and trust as the actual blockers, not
capacity. Proposed a revised, evidence-based target of ~15/month for an
initial window, with reassessment after. Built training plans for
operational leads to drive organic usage rather than positioning the
product purely as a management reporting tool.

**Result:** Became a multi-year engagement, not the original 2-month
sprint. Reached ~240 licenses by ~1.5 years and ~280-300 by ~2 years. The
trust built through this process led to a new seasonal/usage-based
licensing model, later adopted for other large seasonal clients.

**Metrics:** Original target 150→300 in 2 months [CONFIRMED, unfounded] |
real historical growth ~10/month [CONFIRMED] | revised target ~15/month
[CONFIRMED] | ~240 licenses at 1.5 years, ~280-300 at 2 years [CONFIRMED]

**Soundbite:** "A sales manager wanted Metro Mobile doubled in two months
with no data behind the number. I pushed back, then went and did the
discovery myself, real usage was growing about 10 licenses a month, and
trust was the actual blocker, not capacity. I proposed a realistic target
and built training to drive organic adoption. It took about a year and a
half of sustained work to hit 240, and close to two years to get to 280,
driven by trust, not a deadline. That same trust-based engagement also led
to a new licensing model we later rolled out to other seasonal clients."

**Self-identified learning:** should have paired the pushback on the
original target with an immediate alternative proposal rather than just
stating it was unrealistic. Also over-prioritized this one client's
requests relative to the broader client book during the engagement.

**Use for:** expectation-setting, pushing back on a stakeholder,
mistake/what-I'd-do-differently, pricing/packaging design origin.

---

## Story: Quarterly Planning Leadership
**Company:** lululemon | **Competencies:** OKR/cross-org planning,
executive communication, founding a governance function

**Situation:** lululemon's Guest Services product organization spanned 8
product teams (chatbot, WFM, ecommerce, social tools, data governance,
global tools, core CRM, extended CRM) with no structured mechanism to
surface dependencies or align priorities across them.

**Task:** Build and sustain a recurring planning process that aligned all
8 teams and their engineering counterparts.

**Action:** Built and led a recurring quarterly planning process bringing
together all 8 product teams and their engineering counterparts, using a
mix of OKR-based goal setting and other prioritization frameworks
depending on the team. Surfaced dependencies ahead of time. Delivered a
cross-team presentation sharing the aligned plan with Operations and
leadership across all functions. Sustained this as the org's quarterly
alignment mechanism for 3 years.

**Result:** Reduced roadmap conflicts and rework through early dependency
visibility (qualitative outcome, no hard percentage confirmed). Separately:
Raymond was 1 of 2 original Senior PMs who established this process; the
Senior PM group itself grew from 2 to 8 Senior PMs over time, each owning
their own team of BA/PM/dev resources, and Raymond mentored newer Senior
PMs as they joined.

**Metrics:** 8 product teams + engineering coordinated [CONFIRMED] | 3
years sustained [CONFIRMED] | Sr PM group grew 2→8 [CONFIRMED] | rework/
conflict reduction [CONFIRMED — qualitative, no hard % — ask before citing
a number]

**Soundbite:** "I helped build and ran a quarterly planning process across
8 product teams and engineering for three years. I was one of two original
Senior PMs who set it up, and the Senior PM group itself grew from 2 to 8
people over that time, each owning their own team."

**Use for:** OKR/cross-org planning, executive communication, founding a
governance function (not just operating within an existing one).

---

## Story: NARVAR-Quiq Shipment Tracking Integration
**Company:** lululemon | **Competencies:** Ecommerce systems ownership,
API integration, chatbot platform ownership, self-serve deflection

**Situation:** Guest Services fielded a steady stream of post-purchase
"where is my order" inquiries through chat, even though shipment status
was already available through NARVAR, the third-party tracking vendor.
Guests had to leave the chat experience to check tracking separately.

**Task:** Reduce post-purchase support volume by surfacing shipment
tracking directly inside the guest-facing chat experience Raymond already
owned.

**Action:** As owner of the Quiq chatbot platform, drove and prioritized
an API integration pulling NARVAR shipment-tracking data directly into the
chat flow, so guests could get real-time order status without leaving the
conversation or contacting an agent.

**Result:** Reduced post-purchase support volume by roughly 35%, since
most post-purchase contacts were tracking-related. The integration was
also picked up by the Marketing team for outreach campaigns, beyond the
original guest-support use case, evidence the API was built as reusable
infrastructure rather than a one-off feature.

**Metrics:** Post-purchase support volume reduction ~35% [EST — Raymond's
conservative recollection, not a pulled report] | reused by Marketing for
outreach [CONFIRMED]

**Soundbite:** "Most of our post-purchase support volume was guests asking
where their order was, information that already existed in NARVAR. I
owned our chatbot platform, so I drove an API integration to surface that
tracking data directly inside chat. That alone cut post-purchase support
volume by roughly a third."

**Use for:** ecommerce systems ownership, reducing support volume through
self-serve, end-to-end API integration ownership.

---

## Story: Flowfinity Consultant / SOW-Based Client Delivery
**Company:** Flowfinity | **Competencies:** Agency-style delivery, SOW
scoping, concurrent engagement management, vertical/operationally complex
domain range

**Situation:** Beyond his core PM and customer success role, Flowfinity
had external clients wanting custom project work (apps and dashboards)
built on top of the core platform, scoped and billed outside the standard
product roadmap. Clients spanned several operationally complex,
field-services-heavy verticals beyond Metro Mobile, including a geological
survey firm, San Diego Zoo (wildlife tracking, near an Air Force base),
and the City of Cincinnati (municipal sewer systems).

**Task:** Deliver custom client builds as a billed consultant, working
with Sales to properly scope and structure each engagement, across a range
of operational domains.

**Action:** Partnered directly with Sales to scope custom client requests
and set up SOWs for each engagement. Delivered the actual builds himself,
billed at $200/hr. Typically ran 1-3 client engagements concurrently,
balancing this alongside core PM/CS responsibilities. Had the same
hands-on depth of involvement (client relationship ownership, discovery,
app building) with the geological survey, San Diego Zoo, and Cincinnati
engagements as with Metro Mobile.

**Result:** Delivered custom, billable client work consistently alongside
core platform responsibilities, direct, lived experience with SOW-based,
billable-hour client delivery across multiple operationally complex
verticals, not just internal roadmap ownership.

**Metrics:** $200/hr billed rate [CONFIRMED — interview context only, not
for resume use] | typically 1-3 concurrent engagements [CONFIRMED] | same
depth of involvement across all listed clients [CONFIRMED, though scope/
outcome detail beyond Metro Mobile is lighter, confirm specifics with
Raymond before a deep interview probe]

**Use for:** agency/SOW/consultancy delivery, vertical or operationally
complex domain range beyond a single client type.

**Note:** the consultant/SOW work was core scope of Raymond's one
full-time Flowfinity role, not side or contract work performed outside a
separate job. Frame naturally as part of the role's responsibilities,
never as moonlighting.

---

## Story: Project Manager Mentorship
**Company:** lululemon | **Competencies:** Managing/mentoring without
formal authority, developing talent, influencing a decision you don't own

**Situation:** Over Raymond's ~5-year tenure, 4 Project Managers cycled
through, reporting formally to Tech rather than to Raymond, but working
closely with him day-to-day on his initiatives.

**Task:** Get strong performance and growth out of PMs Raymond had no
formal authority over, and give honest, useful input to their actual
managers when performance wasn't working.

**Action:** Functionally mentored each PM through their day-to-day work.
Kept documented feedback and memos of conversations and expectations with
each one. When 2 of the 4 weren't meeting the bar, gave their formal
manager specific, documented feedback and examples rather than vague
concerns, while being clear he held no authority to make the final call
himself.

**Result:** 2 of the 4 PMs succeeded and moved on to other roles. 2 did
not work out; their managers made the performance decision, informed
directly by Raymond's documented feedback.

**Metrics:** 4 PMs mentored over ~5 years [CONFIRMED] | 2 promoted/moved
on, 2 performance-managed out [CONFIRMED] | Raymond's role: documented
feedback and memos, no formal authority [CONFIRMED]

**Soundbite:** "Four different Project Managers rotated through working
with me over five years, all reporting to Tech, not to me. I mentored each
one directly, kept real documentation of our conversations and
expectations, and when it wasn't working out for two of them, I gave
their manager specific, evidenced feedback rather than a vague
impression. Two moved on because it wasn't the right fit. I didn't have
the authority to make that call myself, but my input clearly shaped it."

**Resume caution:** do not imply formal management authority on a resume
or cover letter. Frame explicitly as mentorship with documented
performance input, the manager of record made the final call.

**Use for:** managing/mentoring other PMs, giving feedback without formal
authority, influencing a decision you don't own.

---

## Story: OSB-to-Kafka Returns Backend Re-Architecture
**Company:** lululemon | **Competencies:** Product-led technical
requirements, backend re-architecture, driving change without owning the
technical build

**Note:** this initiative is confirmed and genuinely distinct from the
Return Fraud Prevention & Tax Reconciliation story (a different problem,
addressed on a different track), but it is documented at a lighter level
of detail in the source material than the other stories in this file.
Confirm specifics with Raymond before using it as a primary story in a
live interview.

**Situation:** lululemon's returns/refund pipeline ran on Oracle Service
Bus (OSB), a system the organization wanted to move toward a modern,
event-based architecture.

**Task:** Define the requirements and business logic needed to move the
returns/refund pipeline to a Kafka-based event-streaming architecture.

**Action:** Defined the requirements and business logic for the move from
OSB to Kafka. Engineering owned the technical architecture and
implementation; Raymond's role was product-led requirements definition,
not the technical design itself.

**Result:** Returns/refund backend moved to event-based (Kafka)
architecture, shaped by Raymond's requirements and business logic.

**Metrics:** [CONFIRMED that the role was requirements/business logic, not
architecture ownership; exact timeline relative to other initiatives and
any hard outcome metric are not yet confirmed, ask Raymond before citing
either]

**Soundbite:** "Separately from the return fraud work, we also moved the
returns backend off Oracle Service Bus onto a Kafka-based event
architecture. I defined the requirements and business logic for what that
needed to support; engineering owned the technical build. It's a good
example of driving a backend re-architecture from the product side without
owning the technical implementation myself."

**Use for:** backend/platform re-architecture, defining technical
requirements for engineering, driving change without owning the technical
decision.

---

## Questions for Raymond to Ask the Interviewer
Suggest 1–2 tailored to the specific JD and interview stage — not generic
"what's the roadmap" questions unless genuinely well-targeted. Draft these
fresh per interview based on the actual JD and what's been discussed.
