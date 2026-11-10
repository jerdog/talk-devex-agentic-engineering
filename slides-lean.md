---
theme: wwt
title: Developer Experience in the Age of Agentic Development
subtitle: The friction didn't disappear. It moved.
info: |
  ## Developer Experience in the Age of Agentic Development

  With everything changing in tech at a frenetic pace, the emphasis on developer
  productivity has overshadowed the true essence of developer experience (DevEx).
  Frameworks like SPACE, getDX, and DORA provide valuable insights, but agentic
  coding tools have broken their core assumption: that a human is the one typing.

  This talk explores how the fundamentals of DevEx hold up in an agentic world,
  why the friction has moved from writing code to reviewing, trusting, and
  governing it, and what a practitioner-centric measurement approach looks like
  when your teammate might be an agent.
layout: cover
presenterName: Jeremy Meiss
presenterRole: Tech Solution Architect, World Wide Technology
hideBadge: true
duration: 25min
exportFilename: slides_devex-in-the-age-of-agentic-development_lean
transition: slide-left
drawings:
  persist: false
---

<!--
RESET THE TIMER. 25 minutes, mixed audience: engineering leaders and practitioners.

Thesis in one line: agentic tools didn't remove developer friction, they relocated it. A meaningful share of the code hitting your repo may not have been typed by a human at all, so DevEx has to account for the reviewing, trusting and governing that now surrounds it.
-->

---
layout: boxes
title: DevEx disasters... now with agents
boxes:
  - title: The 4,000-line PR
    detail: AI-generated changes, one-line description.
  - title: The helpful refactor
    detail: The codebase got "cleaned up" overnight. Nobody asked.
  - title: The green test suite
    detail: It passes because the agent quietly deleted the failing assertions.
---

<!--
We've all used a tool that was a disaster. Now add an agent to the mix. The disasters didn't go away. They just got faster and less legible. Let the room laugh, then move on.
-->

---
layout: speaker
speakers:
  - name: Jeremy Meiss
    role: Tech Solution Architect
    company: World Wide Technology
    photo: /images/jeremy-meiss.png
    orgs:
      - name: DevOpsDays KC organizer
      - name: CommunityDays KC organizer
      - name: CDF Ambassador 2025-26
---

<!--
I work in AI-native solution architecture, which means I live at the intersection of "does this agent actually help my developers" and "how do I prove that to leadership without a vanity metric." Keep this to 30 seconds.
-->

---
layout: stats
title: AI is an amplifier
stats:
  - value: "+59%"
    label: throughput, YoY
    caption: CI, 28M workflows, CircleCI 2026
  - value: "~2x"
    label: top 5% of teams
    caption: Nearly doubled their output
  - value: "+4%"
    label: median team
  - value: "0%"
    label: bottom quartile
    caption: Same tools. Same models.
---

<!--
DORA, the research group that has studied engineering performance for over a decade, surveyed nearly 5,000 technology professionals and landed on one sentence: AI is an amplifier. It doesn't fix a struggling organization. It takes whatever is already true about a team and produces more of it.

[click] CircleCI shows what that looks like in pipeline data, not a survey: 28 million workflows, throughput up 59% year over year. [click] Almost all of that sits with the top 5% of teams, who nearly doubled their output. [click] The median team improved 4%. [click] The bottom quarter didn't move at all.

Same tools. Same models. Radically different outcomes. That is the bridge into this talk: what the amplifier amplifies is your developer experience.

Candor note: DORA's 2026 return-on-AI report has been criticized for leaning on narrative over new research. CircleCI's pipeline data and Atlassian's workforce research reach the same conclusion independently, so nothing in this deck rests on DORA alone.
-->

---
layout: comparison
title: Two definitions, one cause and effect
left:
  title: Developer Experience
  points:
    - "“…the journey of developers as they learn and deploy technology, which if successful, focuses on eliminating obstacles that hinder a developer or practitioner from achieving success in their endeavors.”"
    - "Jessica West, Chronosphere/Palo Alto Networks"
right:
  title: Developer Productivity
  points:
    - "“…the effectiveness and efficiency with which software developers produce high-quality code and complete projects.”"
    - "LinearB"
---

Experience is the cause. Productivity is the effect.

<style>
/* Widen the boxes on this slide only: the layout's 5rem side padding drops to
   2rem, which lines the boxes up with the footer's edges. The root element
   carries this slide's scoped hash, so no :deep() is needed here. */
.wwt-comparison {
  padding-left: 2rem !important;
  padding-right: 2rem !important;
  /* Column flex so the boxes + closing line can be centered vertically in the
     space under the title (auto margins on the grid and the footer line). */
  display: flex !important;
  flex-direction: column;
}
:deep(.wwt-comparison__grid) {
  margin-top: auto !important;
}
/* Equal-height boxes: the grid already stretches both columns to the same
   height, so let each card fill its column. */
:deep(.wwt-comparison__card) {
  flex: 1;
}

/* Quote styling for the definitions: no bullets, quote first, attribution last.
   :deep() because the layout renders the list, and !important to beat its own
   scoped padding rule. Sizes are kept tight so the cause/effect line below the
   boxes clears the footer. */
:deep(.wwt-comparison__card ul) {
  list-style: none !important;
  padding: var(--wwt-space-4) var(--wwt-space-6) var(--wwt-space-3) !important;
}
:deep(.wwt-comparison__card li:first-child) {
  font-style: italic;
  font-size: 1em;
  line-height: 1.4;
  border-left: 4px solid var(--wwt-primary-base);
  padding-left: var(--wwt-space-4);
}
:deep(.wwt-comparison__card li:last-child) {
  margin-top: var(--wwt-space-3);
  padding-left: calc(var(--wwt-space-4) + 4px);
  font-size: 0.8em;
  color: var(--wwt-ink-muted);
}
:deep(.wwt-comparison__footer) {
  margin-top: var(--wwt-space-4) !important;
  margin-bottom: auto !important;
  text-align: center !important;
}
:deep(.wwt-comparison__footer *) {
  text-align: center !important;
}
</style>

<!--
These definitions haven't changed. What changed is the actor: "developer" now sometimes means a human, sometimes an agent acting on a human's behalf, and increasingly a human orchestrating several agents at once. The roots (tools, process, cognitive load, flow, and now trust in agent output) still determine the fruit.

DevEx as a concept dates to a 2012 paper presented at an IEEE conference in Zurich Fagerholm and Münch, "Developer experience: Concept and definition"), with roots in a 1985 research on programmer performance. Agentic tooling is the newest way of working those authors couldn't have anticipated, but the lens still applies.
-->

---
layout: code-focus
title: The old gold standard
---

```bash
git push heroku main
```

<!-- code-focus has no footer of its own, so add the theme's Footer here to get
     the bottom-left WWT logo, page number and dark-mode toggle. -->
<Footer />

<style>
/* The footer's muted grey is meant for light slides. On this dark layout the
   page number and toggle disappear, so lighten them here. */
:deep(.wwt-footer) {
  color: var(--wwt-ink-white) !important;
  opacity: 0.8;
}
</style>

<!--
Heroku set the DevEx bar for a decade: a git push and you're live. In this era the bar moved. It's no longer "can I ship my own code effortlessly," it's "can I direct, review and trust an agent's code effortlessly." The tools changed. The underlying want, remove friction between idea and running software, did not.
-->

---
layout: stats
title: Throughput is a vanity metric
stats:
  - value: "+15%"
    label: feature-branch throughput, median team
    caption: Code written
  - value: "−7%"
    label: main-branch throughput, same team
    caption: Code that reaches customers
  - value: "70.8%"
    label: main-branch success rate
    caption: Lowest in five years (now 76.7%). Benchmark 90%.
---

<style>
/* Size every stat value from its column's width so all three match and none
   wraps. Each .wwt-stat becomes a size container, and the value is set in
   container-width units (cqi), so the three identical columns get one shared
   font size. 24cqi is tuned so an 8-character word like "Seconds" fills about
   85% of a column; a longer value would need a smaller number here.
   !important beats the theme's fixed 72px for three-up grids; nowrap and
   overflow-wrap: normal stop the theme's break-anywhere rule splitting words. */
:deep(.wwt-stat) {
  container-type: inline-size;
}
:deep(.wwt-stat__value) {
  font-size: 24cqi !important;
  white-space: nowrap;
  overflow-wrap: normal;
}
</style>

<!--
Lines of code were always gameable. Now a defensible-looking diff is free, so volume measures nothing. CircleCI split the same pipeline data by branch type. [click] Feature-branch throughput rose for nearly every team, a 15% gain for the median team. [click] Main-branch throughput, the code that actually reaches customers, fell 7% for that same median team. [click] And the main-branch success rate hit 70.8%, the lowest in five years, against a 90% benchmark. CircleCI's July 2026 follow-up shows it recovering to 76.7%, still short of the mid-80s teams hit in 2023 and 2024.

Developers are producing more code than ever. Very little of the increase is reaching production. If velocity is the only thing you measure, the measurement is hiding the problem.
-->

---
layout: comparison
title: Where the friction lives
left:
  title: Used to live in
  points:
    - Writing boilerplate
    - Remembering syntax
    - Hunting for examples
    - Slow builds and manual test scaffolding
right:
  title: Now lives in
  points:
    - Reviewing unfamiliar diffs
    - Verifying code you didn't derive yourself
    - Calibrating trust
    - Governing what agents may touch
---

Source: Atlassian workforce research, the "AI efficiency paradox."

<!--
Atlassian's workforce research, a separate study with no connection to DORA, describes an "AI efficiency paradox": individual speed gains back up at review and approval before they reach the organization. AI didn't remove the pain, it moved it. Typing got faster. Trusting, reviewing and governing got slower. If your DevEx program measures only the first half of that trade, you're measuring half the story.
-->

---
layout: stats
title: What developers feel vs. what's measured
stats:
  - value: "96%"
    label: don't fully trust AI code
    caption: Sonar 2026, 1,149 developers
  - value: "48%"
    label: always verify code
    caption: Before committing
  - value: "+20%"
    label: felt faster with AI
    caption: METR randomized trial, 16 developers, 246 tasks
  - value: "−19%"
    label: "measured: slower"
    caption: Same trial, real tasks
---

<!--
Why does verification cost so much? [click] Sonar asked 1,149 developers and found 96% don't fully trust that AI-generated code is functionally correct. [click] Only 48% always check it before committing. That gap is roughly where your production incidents live. Sixty-one percent named the failure mode: code that looks correct but isn't reliable. AI mistakes are quiet: it compiles, the tests pass, and three weeks later it does the wrong thing under load.

[click] Then the METR randomized controlled trial: sixteen experienced developers, 246 real tasks. Before starting they predicted AI would make them 24% faster. Afterward they believed they had been about 20% faster. [click] The measured result: 19% slower. [pause]

Predicted faster. Felt faster. Measured slower. That is a developer-experience finding: the feeling and the data disagree, so a DevEx program needs both surveys and system data. Don't trust the sensation of speed.
-->

---
layout: boxes
title: Four pillars of world-class DevEx
reveal: true
boxes:
  - title: Fast, high-quality feedback loops
    detail: Agent output validation is part of the loop, not an afterthought.
  - title: Low cognitive load
    detail: From "recall syntax" to "verify a stranger's reasoning". That's a heavier tax.
  - title: Enabled flow state
    detail: Interrupted by context-switching into reviewer mode, several times an hour.
  - title: Calibrated trust and governance (new)
    detail: Know what an agent may touch and how far to trust what it hands back.
---

<!--
The three original pillars from the ACM Queue framing (feedback loops, cognitive load, flow state) all survive contact with agentic tooling. They just get harder. The fourth is emerging in 2026 conversations: calibrated trust and governance. Teams that treat "which agent can touch which part of the codebase, under what review policy" as a deliberate design decision see fewer disasters than teams that just let the agent open PRs. Click through one at a time.
-->

---
layout: boxes
title: "DORA 2025: what makes AI pay off"
boxes:
  - title: Clear AI stance
    detail: A stated, communicated position on AI use.
  - title: Healthy data ecosystems
    detail: Data that's well-governed at the source.
  - title: AI-accessible data
    detail: Internal data AI tooling can actually reach.
  - title: Small batches
    detail: Working in small, reviewable increments.
  - title: User-centric focus
    detail: Genuinely centered on the user, not the roadmap.
  - title: Quality internal platforms
    detail: Platforms worth building on.
---

<!--
Source: DORA's AI Capabilities Model, 2025. None of these are new ideas. DORA has recommended most of them for a decade. What is new is the finding that these practices are what determine whether AI adoption pays off, which means the answer to "how do we get a return on AI" and the answer to "how do we run a strong engineering organization" are the same answer. That answer is developer experience.

Check before delivery: the blog post says seven practices and names six, and the Don't Panic deck lists six. Confirm the seventh against the DORA report, or say "practices like these".
-->

---
layout: process
title: The new pillar, governance, in five moves
steps:
  - title: Set permission tiers
    detail: What an agent can touch unsupervised, and what always needs a human.
  - title: Track AI change failure rate
    detail: Separately from your overall DORA number.
  - title: Keep an audit trail
    detail: What the agent changed and why, not just that it did.
  - title: Rotate oversight duty
    detail: Like on-call, so it isn't one person's invisible tax.
  - title: Revisit the tiers
    detail: Trust is earned by track record, not granted once.
---

<style>
/* Five sentence-length steps are too wide for the layout's five-across columns
   (unequal widths, text running past the footer). Lay them out as five rows:
   number | step name | detail. The markup is unchanged, so the click-through
   reveal still works. :deep() because the layout renders the list. */
:deep(.wwt-process__steps) {
  grid-auto-flow: row !important;
  grid-auto-columns: auto !important;
  gap: var(--wwt-space-2) !important;
  margin-top: var(--wwt-space-4) !important;
}
:deep(.wwt-process__step) {
  display: grid !important;
  grid-template-columns: 4.5rem minmax(0, 1fr) minmax(0, 1.5fr);
  align-items: center;
  column-gap: var(--wwt-space-6);
  padding: var(--wwt-space-2) var(--wwt-space-4) !important;
  border-top: 3px solid var(--wwt-primary-base) !important;
}
:deep(.wwt-process__number) {
  font-size: 36px !important;
}
:deep(.wwt-process__title) {
  font-size: 1.25rem !important;
}
</style>

<!--
This pillar didn't exist in the original version of this talk because it didn't need to. Governance is being described across 2026 DevEx research as the central lever separating teams that get real value from agentic coding from teams that get real incidents. Five steps is the layout's limit, so this is the whole list.
-->

---
layout: quote
dark: true
attribution: Goodhart's Law
---

"When a measure becomes a target, it ceases to be a good measure."

<!--
Goodhart's Law was already a risk. Agents make it worse, because it's now trivially easy to hit almost any output target. Commits, story points closed and PRs opened can all be inflated by an agent in minutes without a shred of added value. If your incentives reward volume, you will get volume, and very little else.
-->

---
layout: boxes
title: How your metrics change with agents
reveal: true
boxes:
  - title: Cycle time
    detail: Include the time to understand what shipped.
  - title: PR review time
    detail: Often the real bottleneck. Generation got fast, review didn't.
  - title: Rework rate
    detail: Split human-authored from AI-authored.
  - title: Meeting load
    detail: Add "agent sync" time to the ledger.
  - title: Time to first commit
    detail: Add "time to first trusted agent task."
  - title: Perceived focus time
    detail: Count agent check-ins as interruptions.
  - title: AI change failure rate (new)
    detail: Incidents from agent changes, beside your DORA number.
  - title: Review-to-merge ratio (new)
    detail: How much scrutiny agent PRs get before shipping.
---

<style>
/* Seven boxes: the layout's three-across grid would leave one orphaned on its
   own row, so use four across (4 + 3). Tighter card type keeps two rows above
   the footer. :deep() because the layout and BoxCard render these elements. */
:deep(.wwt-boxes__grid) {
  grid-template-columns: repeat(4, minmax(0, 1fr)) !important;
  gap: var(--wwt-space-4) !important;
}
:deep(.wwt-box-card__header) {
  font-size: 1.1rem;
  padding: var(--wwt-space-2) var(--wwt-space-4);
}
:deep(.wwt-box-card__body) {
  font-size: 1rem;
  padding: var(--wwt-space-3) var(--wwt-space-4);
}
</style>

<!--
Original metrics still matter, but several change meaning. Cycle time can look great right up until an unreviewed agent change causes an incident. PR review time frequently becomes the real constraint. Two new numbers worth tracking explicitly: AI change failure rate, and review-to-merge ratio on agent-authored PRs.

Detail that no longer fits on the cards: for cycle time, watch for rubber-stamped merges, because a fast merge on unreviewed code isn't a win. For rework rate, a rising AI rework rate means tighten specs and scope, not abandon the tooling. For time to first commit, the new-hire version is "time to first trusted agent task." For focus time, count agent check-ins and approvals as their own interruption category.

Meeting load: add explicit "agent sync" time to the ledger, because coordinating what three agents are doing overnight is real work and it's invisible if you don't name it. Watch for status-theater meetings where a human narrates what an agent already logged. Onboarding now has a second track too: onboarding the developer to your team's agentic workflows, permission tiers and review conventions.
-->

---
layout: boxes
title: A practitioner-centric scorecard
boxes:
  - title: Main-branch success rate
    detail: Benchmark 90%. Down to 70.8% last year, 76.7% now.
  - title: Recovery time
    detail: Benchmark 60 minutes. The median was 72.
  - title: Merge Efficiency Ratio
    detail: Validation cycles per change. Median 3.9, top 5% 2.6, elite 1.3.
  - title: AI change failure rate
    detail: Incidents from agent changes, tracked against overall DORA CFR.
---

Sources: CircleCI 2026 State of Software Delivery and its July 2026 follow-up.

<!--
These are sourced benchmarks, not mandates. Establish your own baseline, iterate, and revisit as your team's agent fluency grows. Pair them with the practitioner view from the last slide: cycle time, PR review time, rework, and reviewer load in whatever form you can track it. Measure main-branch throughput, not activity.

Build a healthy measurement culture: no framework is a silver bullet, agentic tooling included. Aim for continuous improvement, never judgment and never a way to justify headcount cuts. Explain the why behind every new agent metric. Involve the team in setting permission tiers instead of handing down policy. Watch trends, not absolutes. Combine the numbers with the qualitative: do people actually trust this?

If AI change failure rate runs meaningfully above your human baseline, that isn't an argument against the tooling. It's a signal to tighten governance and review before scaling usage.
-->

---
layout: quote
attribution: Jeremy Meiss
---

DevEx is ruthlessly eliminating the barriers and blockers that keep your practitioners from being successful, whether the one typing the next line is a person or an agent they're accountable for.

<!--
Investing in developer experience is still a direct investment in your organization's capacity to innovate. Agentic tooling didn't change that. It raised the stakes: the friction you fail to remove now compounds at agent speed, not human speed. Pause after the last line, then advance.
-->

---
layout: thank-you
heading: Thank you
speakers:
  - name: Jeremy Meiss
    socials:
      bluesky: jerdog.dev
      linkedin: /in/jeremy-meiss
      github: jerdog
      website: jmeiss.me
slidesUrl: https://speaking.jmeiss.me
---

<!--
Slides at speaking.jmeiss.me. Questions: be ready for "how do we start measuring AI change failure rate" (tag agent-authored PRs, then join to incident data) and "what permission tier should we start with" (read-only plus PR drafts, widen on track record).
-->
