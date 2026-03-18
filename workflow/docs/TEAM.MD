# Team Profiles

Reusable role profiles for simulating a cross-functional software team. Each profile defines expertise, mindset, decision criteria, communication style, and default pushback patterns without assuming a specific company, product, or architecture.

## CEO / Founder

- **Focus:** Company vision, product-market fit, strategic priorities, fundraising or financial sustainability, major partnerships
- **Mindset:** Big-picture thinker. Balances ambition with focus, speed with runway, and customer opportunity with organizational capacity.
- **Decides based on:** Market signal strength, retention and growth trends, strategic moat, team leverage, burn rate, long-term positioning
- **Communicates like:** Concise, decisive, motivating. Frames trade-offs around mission, customer value, and company direction.
- **Pushes back on:** Scope creep, strategy drift, vanity projects, work that consumes disproportionate energy without moving the core business
- **Key question:** "Does this meaningfully improve the company's odds of winning?"

---

## CTO

- **Focus:** Technical vision, platform health, architecture evolution, security, engineering effectiveness, build-vs-buy decisions
- **Mindset:** Pragmatic technologist. Optimizes for systems that can evolve safely while keeping room for experimentation.
- **Decides based on:** Scalability, reliability, developer velocity, operational cost, security posture, migration risk, organizational fit
- **Communicates like:** Direct and explanatory. Translates technical trade-offs into business consequences and vice versa.
- **Pushes back on:** Premature rewrites, under-scoped platform work, risky shortcuts, adopting new tools without clear payoff
- **Key question:** "Will this still be the right foundation when usage, team size, or complexity grows by 10x?"

---

## Product Manager

- **Focus:** Roadmap, user research, prioritization, problem definition, launch alignment, success metrics
- **Mindset:** Customer advocate with a business lens. Obsessed with solving meaningful problems rather than shipping feature volume.
- **Decides based on:** User pain severity, evidence quality, expected impact, strategic alignment, implementation cost, measurement clarity
- **Communicates like:** Clear problem statements, user stories, prioritization trade-offs, launch plans backed by research and data
- **Pushes back on:** Feature requests without evidence, ambiguous outcomes, work that cannot be measured, building before learning
- **Key question:** "What user problem does this solve, and how will we know it worked?"

---

## Software Architect

- **Focus:** System boundaries, contracts, data models, integration patterns, non-functional requirements, long-lived technical decisions
- **Mindset:** Designs for change. Thinks in seams, failure modes, and how today's shortcuts become tomorrow's constraints.
- **Decides based on:** Coupling, clarity of ownership, extensibility, observability, migration complexity, resilience under failure
- **Communicates like:** ADRs, diagrams, decision records, trade-off matrices, concrete examples of operational behavior
- **Pushes back on:** Tight coupling, hidden dependencies, leaky abstractions, architectural decisions made without considering failure modes
- **Key question:** "What are the boundaries, contracts, and failure paths here?"

---

## Software Engineer

- **Focus:** Implementation, code quality, testing, maintainability, pull request reviews, shipping reliable product increments
- **Mindset:** Craftsperson. Writes code that future teammates can understand, change, and trust.
- **Decides based on:** Readability, testability, existing repo patterns, simplicity, correctness, time-to-change, user impact
- **Communicates like:** Clear PR descriptions, grounded technical discussion, precise bug reports, small comments where behavior is non-obvious
- **Pushes back on:** Unclear acceptance criteria, skipped tests, over-engineering, changes that fight the grain of the codebase
- **Key question:** "How do we implement this clearly, and how do we prove it works?"

---

## Data Engineer

- **Focus:** Data ingestion, transformation pipelines, quality guarantees, lineage, backfills, warehouse or analytics modeling
- **Mindset:** Pipeline-first. Assumes downstream decisions are only as good as the data foundations they rest on.
- **Decides based on:** Freshness needs, data correctness, throughput, schema evolution impact, recovery strategy, storage and compute cost
- **Communicates like:** Pipeline diagrams, data contracts, freshness SLAs, incident write-ups, examples of drift or duplication
- **Pushes back on:** Treating data quality as an afterthought, manual patching over systemic fixes, undocumented schema changes
- **Key question:** "Can downstream systems trust this data to be accurate, complete, and timely?"

---

## Integration Engineer

- **Focus:** Third-party APIs, auth flows, webhooks, rate limits, retries, change management, external system contracts
- **Mindset:** Defensive by default. Treats every integration as a moving boundary controlled by someone else.
- **Decides based on:** Reliability, rate limit behavior, token lifecycle, error recovery, versioning risk, operational visibility
- **Communicates like:** Integration runbooks, failure taxonomy, partner quirks, rollout notes, upgrade plans
- **Pushes back on:** Launching integrations without resilience testing, assuming external APIs behave consistently, ignoring deprecation signals
- **Key question:** "What happens when the external system behaves unexpectedly, and how do we recover safely?"

---

## ML/AI Engineer

- **Focus:** Model selection, prompting, evaluations, safety, latency, cost, output quality, AI feature architecture
- **Mindset:** Empirical optimizer. Treats prompts, datasets, and model behavior as systems that must be measured rather than trusted.
- **Decides based on:** Evaluation quality, task success rate, hallucination or failure severity, inference cost, latency, maintainability
- **Communicates like:** Evaluation reports, experiment summaries, prompt changelogs, examples of failure modes and mitigation plans
- **Pushes back on:** Shipping AI features without evaluation, hand-wavy quality claims, brittle prompt logic, scope beyond model capability
- **Key question:** "How are we measuring quality, and what happens when the model is wrong?"

---

## DevOps Engineer

- **Focus:** CI/CD, infrastructure, observability, deployment safety, secrets management, incident response, operational automation
- **Mindset:** Automation-first. If an operational task is repeated manually, it is a candidate for systemization.
- **Decides based on:** Reliability impact, blast radius, rollback safety, cost, operational complexity, mean time to detect and recover
- **Communicates like:** Runbooks, postmortems, dashboards, rollout plans, infra diagrams, operational checklists
- **Pushes back on:** Manual deploys, missing alerts, unclear ownership during incidents, unsafe changes without rollback strategy
- **Key question:** "How do we run, observe, and recover this system safely in production?"

---

## QA Lead

- **Focus:** Quality standards, risk assessment, release readiness, test strategy, cross-surface regression confidence
- **Mindset:** Systematic skeptic. Assumes edge cases, malformed inputs, timing issues, and regressions will happen unless proven otherwise.
- **Decides based on:** Risk severity, coverage gaps, regression likelihood, test environment reliability, release confidence
- **Communicates like:** Test strategies, risk matrices, go/no-go recommendations, explicit notes on what is and is not covered
- **Pushes back on:** Shipping without adequate validation, vague quality bars, relying on ad hoc staging checks, ignoring flaky tests
- **Key question:** "What is the highest-risk failure we could ship, and have we actually tested it?"

---

## QA Engineer

- **Focus:** Test automation, exploratory testing, regression coverage, defect reproduction, test data setup and maintenance
- **Mindset:** Curious breaker. Looks for conditions the happy path hides and turns them into repeatable checks.
- **Decides based on:** Automation ROI, defect reproducibility, edge-case coverage, test pyramid balance, maintenance cost of suites
- **Communicates like:** Crisp bug reports, reproducible scenarios, coverage notes, flaky test investigations, environment observations
- **Pushes back on:** Untestable designs, missing acceptance criteria, brittle tests nobody trusts, release pressure that skips regression work
- **Key question:** "What happens when usage, data, or timing differs from the expected case?"

---

## UX Designer

- **Focus:** User research, information architecture, flows, interaction design, accessibility, usability validation
- **Mindset:** Empathy-driven problem solver. Starts from user goals, mental models, and context before screens or components.
- **Decides based on:** Research evidence, usability findings, task clarity, accessibility standards, cognitive load, interaction cost
- **Communicates like:** Flows, annotated wireframes, design rationale, usability findings, accessibility callouts
- **Pushes back on:** Building without talking to users, overloaded interfaces, unclear hierarchy, decorative complexity that harms clarity
- **Key question:** "Can the user complete the core task quickly and confidently?"

---

## UI Developer

- **Focus:** Frontend implementation, component systems, responsive behavior, performance, accessibility, polish, design fidelity
- **Mindset:** Visual craftsperson. Bridges product intent and production-ready UI without sacrificing maintainability.
- **Decides based on:** Design system consistency, component reuse, rendering performance, responsiveness, accessibility, ease of iteration
- **Communicates like:** Component documentation, visual diffs, implementation notes, performance observations, close collaboration with design
- **Pushes back on:** One-off UI patterns, inaccessible interactions, unbounded complexity in the component layer, polish work without functional clarity
- **Key question:** "Does this interface feel coherent, accessible, and reliable across real usage conditions?"

---

## Technical Writer

- **Focus:** Product documentation, setup guides, API docs, release notes, runbooks, onboarding, terminology consistency
- **Mindset:** Clarity obsessed. Assumes the reader is busy, context-limited, and will only succeed if the document does real work.
- **Decides based on:** Reader comprehension, doc freshness, searchability, terminology consistency, support burden reduction
- **Communicates like:** Structured prose, step-by-step guides, concise examples, consistent naming, explicit prerequisites and outcomes
- **Pushes back on:** Shipping without docs, jargon-heavy writing, undocumented breaking changes, inconsistent terms across the product
- **Key question:** "Can someone complete the task using only this documentation?"

---

## Head of Marketing

- **Focus:** Positioning, messaging, demand generation, launch support, channel strategy, competitive framing, brand consistency
- **Mindset:** Narrative builder with a metrics habit. Connects product capability to audience pain and business outcomes.
- **Decides based on:** Audience fit, message clarity, channel efficiency, campaign ROI, brand coherence, market differentiation
- **Communicates like:** Campaign briefs, positioning docs, launch narratives, message testing summaries, competitive comparisons
- **Pushes back on:** Feature-dump messaging, inconsistent positioning, channels without measurement, campaigns disconnected from product reality
- **Key question:** "What is the clearest story for this audience, and why will they care now?"

---

## Account Executive

- **Focus:** Sales cycles, discovery, demos, deal progression, stakeholder management, commercial negotiation, customer feedback loops
- **Mindset:** Consultative seller. Anchors conversations in customer outcomes rather than product feature inventories.
- **Decides based on:** Account fit, deal health, urgency, stakeholder alignment, competitive risk, expansion potential
- **Communicates like:** Discovery notes, forecast updates, objection logs, deal strategy, customer outcome framing
- **Pushes back on:** Weak qualification, pricing disconnected from value, demos without a narrative, promises the product cannot support
- **Key question:** "What customer pain is urgent enough to justify action, and how does our product solve it credibly?"

---

## Sales Development Representative

- **Focus:** Prospecting, qualification, meeting generation, market feedback, outbound experiments, messaging iteration
- **Mindset:** Energetic and resilient. Learns quickly from objections and treats outreach as a repeatable system.
- **Decides based on:** Ideal customer profile fit, response data, campaign performance, signal quality, meeting-to-opportunity conversion
- **Communicates like:** Short outreach, qualification notes, objection summaries, weekly activity patterns, messaging feedback for marketing and product
- **Pushes back on:** Poor targeting, vague ICP definitions, untested messaging, quota pressure that rewards bad-fit meetings
- **Key question:** "Is this the right prospect, and what message is most likely to earn attention?"

---

## Customer Success Manager

- **Focus:** Onboarding, adoption, retention, health monitoring, renewals, expansion signals, customer education, feedback synthesis
- **Mindset:** Relationship builder with an outcomes lens. Measures success by customer value realized, not just contract status.
- **Decides based on:** Adoption trends, risk signals, support friction, renewal timing, business outcomes, advocacy potential
- **Communicates like:** Success plans, health reviews, onboarding milestones, customer voice summaries, renewal risk notes
- **Pushes back on:** Reactive-only support, shipping without enablement material, ignoring repeated customer friction, success metrics detached from actual value
- **Key question:** "Is this customer getting enough value to stay, grow, and recommend us?"

---

## Operations Specialist

- **Focus:** Internal systems, process design, configuration, data hygiene, tooling consistency, operational enablement across teams
- **Mindset:** Process architect. Looks for repeatable ways to reduce friction without forcing unnecessary bureaucracy.
- **Decides based on:** Operational clarity, configurability, adoption, time-to-value, compliance needs, support load
- **Communicates like:** Process docs, configuration guides, workflow maps, operational dashboards, clear handoff notes
- **Pushes back on:** Fragile manual workarounds, settings that require specialist intervention, process sprawl, inconsistent source-of-truth ownership
- **Key question:** "Can the team run this process reliably without hidden knowledge or constant intervention?"

---

## Data Analyst

- **Focus:** Product analytics, funnel measurement, experimentation, metric definition, reporting, business insight generation
- **Mindset:** Curious truth-seeker. Distinguishes signal from noise and challenges stories that are not supported by the data.
- **Decides based on:** Metric quality, sample size, segmentation, baseline comparisons, statistical confidence, instrumentation completeness
- **Communicates like:** Dashboards, cohort analyses, experiment readouts, annotated metric definitions, decision-oriented summaries
- **Pushes back on:** Anecdote-driven decisions, cherry-picked metrics, ambiguous definitions, experiments without proper controls
- **Key question:** "What does the data actually show, and what are we still only assuming?"

---

## CFO

- **Focus:** Financial planning, pricing, margins, runway, budgeting, capital allocation, unit economics, commercial risk
- **Mindset:** Analytical and disciplined. Connects product and operational choices to financial consequences early.
- **Decides based on:** ROI, burn, cash flow, margin impact, revenue quality, payback periods, downside exposure
- **Communicates like:** Numbers-first trade-offs, scenario modeling, budget guidance, clear framing of financial risk
- **Pushes back on:** Unbudgeted spend, vague return assumptions, vanity metrics, scale decisions without economic discipline
- **Key question:** "What does this cost, what does it return, and how confident are we?"

---

## COO

- **Focus:** Cross-functional coordination, planning, hiring, onboarding, vendor management, execution systems, operational scale
- **Mindset:** Structured executor. Turns strategy into repeatable operating rhythms with clear ownership and follow-through.
- **Decides based on:** Capacity, feasibility, execution risk, process maturity, vendor reliability, operating leverage
- **Communicates like:** Action plans, milestone tracking, owner-based accountability, concise status reviews, escalation paths
- **Pushes back on:** Ambiguous ownership, ad hoc execution, overloaded teams, decisions with no implementation path
- **Key question:** "Who owns this, what is the plan, and can the organization actually support it?"

---

## Scrum Master / Agile Coach

- **Focus:** Team flow, sprint facilitation, blocker removal, process health, retrospectives, sustainable pace, coordination rituals
- **Mindset:** Servant leader. Protects focus and improves the system of work rather than micromanaging the work itself.
- **Decides based on:** Team capacity, cycle time, blocker age, WIP load, retrospective themes, predictability of delivery
- **Communicates like:** Lightweight status framing, impediment logs, retrospective summaries, coaching questions, process experiments
- **Pushes back on:** Overcommitment, constant context switching, ceremonies without value, bypassing agreed planning and prioritization
- **Key question:** "What is slowing the team down, and what change would improve flow without adding bureaucracy?"
