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
duration: 45min
exportFilename: slides_devex-in-the-age-of-agentic-development
transition: slide-left
drawings:
  persist: false
---

<!--
RESET THE TIMER. 45 minutes, then Q&A. Mixed audience: engineering leaders and practitioners.

Thesis in one line: agentic tools didn't remove developer friction, they relocated it. A meaningful share of the code hitting your repo may not have been typed by a human at all, so DevEx has to account for the reviewing, trusting and governing that now surrounds it.

Pacing map, 45 minutes: Opening 4. Foundations 7. Frameworks 5. The friction moved 8. Pillars and governance 9. Measure 9. Close 3. If you are running long at the halfway mark, the six metric slides in the Measure act are the pressure valve: say the headline of each in one sentence, or skip straight to the scorecard.
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
clicks: 0
stats:
  - value: "+59%"
    label: throughput, YoY
    caption: 28M CI workflows
  - value: "~2x"
    label: top 5% of teams
    caption: Nearly doubled their output
  - value: "+4%"
    label: median team
  - value: "0%"
    label: bottom quartile
    caption: Same tools. Same models.
---

<style>
/* The stats layout has no body slot, so pin the source line above the footer
   with a pseudo-element on the layout root (this slide's scoped hash is on it). */
/* Show every stat at once, with no click-through. The layout reveals stats with
   v-clicks, so keep them visible here and tell Slidev (clicks: 0) that this
   slide has no click steps. */
:deep(.slidev-vclick-hidden) {
  opacity: 1 !important;
  pointer-events: auto !important;
}
.wwt-stats::after {
  content: "Sources: CircleCI 2026 State of Software Delivery (28M CI workflows); DORA 2025.";
  position: absolute;
  left: 5rem;
  right: 5rem;
  bottom: 3.5rem;
  font-size: var(--wwt-text-caption);
  color: var(--wwt-ink-muted);
}
</style>

<!--
DORA, the research group that has studied engineering performance for over a decade, surveyed nearly 5,000 technology professionals and landed on one sentence: AI is an amplifier. It doesn't fix a struggling organization. It takes whatever is already true about a team and produces more of it.

CircleCI shows what that looks like in pipeline data, not a survey: 28 million workflows, throughput up 59% year over year. Almost all of that sits with the top 5% of teams, who nearly doubled their output. The median team improved 4%. The bottom quarter didn't move at all.

Same tools. Same models. Radically different outcomes. That is the bridge into this talk: what the amplifier amplifies is your developer experience.

A quick word on sources, because I want to be straight with you. DORA's 2026 return-on-AI report has been criticized for leaning on narrative over new research. So I'm not resting anything on DORA alone. CircleCI's pipeline data and Atlassian's workforce research, two completely separate studies, reach the same conclusion on their own.
-->

---
layout: image-full
image: /images/slides/devex-integral-dev-lifecycle.jpg
imageAlt: "Illustration of developer experience at the center of the software lifecycle: planning, coding, testing and deployment"
headline: "DevEx touches every stage. Now so do agents."
---

<!--
DevEx isn't one tool or one team. It's the ease of use, the reliability, the documentation, the build process, the test framework and the deploy path, all of it, every stage of the lifecycle. Planning, coding, testing, deploying. Here's what's different now: agents are showing up at every one of those stages too. Which means every stage has a new question attached to it. Not just "is this easy for me," but "is this easy for me and the agent working next to me, and can I trust what comes back." That's the lens for the rest of the talk.
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

<style>
/* Widen the boxes on this slide only: the layout's 5rem side padding drops to
   2rem, which lines the boxes up with the footer's edges. The root element
   carries this slide's scoped hash, so no :deep() is needed here. */
.wwt-comparison {
  padding-left: 2rem !important;
  padding-right: 2rem !important;
  /* Column flex so the boxes are centered vertically in the space under the
     title (auto margins on the grid). */
  display: flex !important;
  flex-direction: column;
}
:deep(.wwt-comparison__grid) {
  margin-block: auto !important;
}
/* Equal-height boxes: the grid already stretches both columns to the same
   height, so let each card fill its column. */
:deep(.wwt-comparison__card) {
  flex: 1;
}

/* Quote styling for the definitions: no bullets, quote first, attribution last.
   :deep() because the layout renders the list, and !important to beat its own
   scoped padding rule. */
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
</style>

<!--
These definitions haven't changed. What changed is the actor: "developer" now sometimes means a human, sometimes an agent acting on a human's behalf, and increasingly a human orchestrating several agents at once. The roots (tools, process, cognitive load, flow, and now trust in agent output) still determine the fruit.
-->

---
layout: comparison
title: Experience is the cause. Productivity is the effect.
left:
  title: "The roots: DevEx"
  points:
    - "The daily journey: tools, processes, cognitive load and flow state."
    - "Now with a new root: trust in what an agent hands back."
right:
  title: "The fruit: Productivity"
  points:
    - "The outcome: high-quality, impactful software that drives business value."
    - "Measured downstream, on what ships, not on what gets typed."
---

<!--
Those two definitions are not the same thing, and the difference matters. Developer productivity is how effective and efficient developers are. DevEx is the experience they have using tools and services. At its core it's about the practitioner. Productivity is driven by the experience, not the other way around. Productivity is a metric. DevEx is a feeling. Sustainable productivity isn't forced. It's a natural outcome of a good experience. DevEx is the leading indicator, because it measures the developer's lived reality. Productivity is the lagging indicator, because it measures the business impact after the fact. And the roots just grew a new one: whether you trust what the agent gives you.
-->

---
layout: image-feature
side: left
image: /images/slides/cornell-devex.jpg
imageAlt: "Title page of the 2012 IEEE paper 'Developer experience: Concept and definition' by Fagerholm and Münch"
---

## DevEx isn't new

> "...developer experience could be defined as a means for capturing how developers think and feel about their activities within their working environments, with the assumption that an improvement of the developer experience has positive impacts on characteristics such as sustained team and project performance."

_Fagerholm and Münch, "Developer experience: Concept and definition," 2012._

Source: <a href="https://ieeexplore.ieee.org/document/6225984" target="_blank">IEEE Xplore</a>

<!--
But DevEx isn't a new thing. The first mention of "developer experience" as a concept was in a paper presented at the 2012 IEEE International Conference on Software and System Process in Zurich, and it has references going back to 1985 on "programmer performance and the effects of the workplace." The line that stands out: DevEx is a means for capturing how developers think and feel about their activities at work, with the assumption that improving it has positive effects on sustained team and project performance.

And a lot of today's interest in DevEx is driven top-down by companies trying to sell you something, with very little focus on developers themselves. That doesn't mean there's no value in the frameworks, but we need to be careful about how we use them.

Paper: https://ieeexplore.ieee.org/document/6225984
-->

---
layout: image-feature
side: left
image: /images/slides/cornell-devex.jpg
imageAlt: "Title page of the 2012 IEEE paper 'Developer experience: Concept and definition' by Fagerholm and Münch"
---

## DevEx isn't new

> "New ways of working such as globally distributed development or the integration of self-motivated external developers into software ecosystems will require a better and more comprehensive understanding of developers' feelings, perceptions, motivations and identification with their tasks in their respective project environments."

_Fagerholm and Münch, "Developer experience: Concept and definition," 2012._

<!--
The same paper makes a second point. In 2012 the new ways of working were globally distributed teams and external developers joining software ecosystems. Their argument: when the way of working changes, you need a better understanding of how developers feel, what they perceive and what motivates them. Agentic tooling is the newest way of working those authors couldn't have anticipated. A teammate that isn't a person, writing code that a person has to answer for. Their lens still applies. The question is the same one: how does this feel to the people doing the work?
-->

---
layout: default
---

# The bar moved

<div class="cmp">
<div>
<p class="cmp__label">Then</p>
<div class="term"><p class="term__cmd"><b>$</b> git push heroku main</p></div>
<p class="cmp__cap">Ship your own code, effortlessly.</p>
</div>
<div v-click>
<p class="cmp__label cmp__label--now">Now</p>
<div class="term"><p class="term__cmd"><b>$</b> agent "fix flaky test"</p></div>
<p class="cmp__cap">Direct, review and "trust" an agent's code, effortlessly(?).</p>
</div>
</div>

<style>
/* Then / now: two terminal cards side by side. Sized so each command stays on
   one line in its column. */
.cmp {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  margin-top: 2rem;
}
.cmp__label {
  margin: 0 0 0.5rem;
  font-size: 20px;
  font-weight: 600;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  color: var(--wwt-ink-muted);
}
.cmp__label--now {
  color: var(--wwt-primary-base);
}
.cmp__cap {
  margin: 1rem 0 0;
  font-size: 24px;
  line-height: 1.35;
  color: var(--wwt-ink-muted);
}
.term {
  background: var(--wwt-accent7-base);
  color: #fff;
  border-radius: 14px;
  padding: 1.5rem 1rem 1.5rem 1.25rem;
  box-shadow: 0 10px 30px rgba(10, 11, 25, 0.25);
  font-family: "Fira Code", ui-monospace, Menlo, Consolas, monospace;
}
.term__cmd {
  margin: 0;
  font-size: 24px;
  line-height: 1.4;
  white-space: nowrap;
}
.term__cmd b {
  color: var(--wwt-primary-light);
  margin-right: 0.5rem;
}
</style>

<!--
Heroku set the DevEx bar for a decade: a git push and you're live. [click] In this era the bar moved. It's no longer "can I ship my own code effortlessly," it's "can I direct, review and trust an agent's code effortlessly." The tools changed. The underlying want, remove friction between idea and running software, did not.
-->

---
layout: timeline
title: We've been here before
events:
  - date: "2008"
    label: An empty room in Toronto
    detail: Andrew Clay Shafer pitches "Agile Infrastructure" at Agile 2008. One person shows up, Patrick Debois.
  - date: Jun 2009
    label: 10+ deploys a day
    detail: Allspaw and Hammond at Velocity. Flickr ships dozens of times a day, with Dev and Ops as one team.
  - date: "2009"
    label: DevOpsDays Ghent
    detail: Debois turns a hashtag into an event. Two people and a shared complaint become an industry.
  - date: "2026"
    label: AI-native engineering
    detail: Same fight, new weapons. A culture problem sold as a tooling problem.
---

Source: WWT, "Is AI-native Engineering Really DevOps 2.0 (or even Agile 3.0)?"

<!--
DevOps didn't start with a plan. It started with an empty session. Andrew Clay Shafer pitched "Agile Infrastructure" at Agile 2008 in Toronto, the idea that operations deserved the same iterative treatment development had gotten. Nobody came, except a Belgian consultant, Patrick Debois, who was tired of work flying over the wall. A year later, John Allspaw and Paul Hammond got on stage at Velocity and talked about ten-plus deploys a day at Flickr. Debois saw it, tweeted the hashtag, and built an event. That's DevOpsDays Ghent. Two guys in a hallway became an industry.

Here's why it matters now. DevOps was never a universal win. In 2024 only 20% of teams qualified as elite in DORA's data, and the low tier grew from 17% to 25%. In 2025 DORA dropped the tiers for team profiles, and the top two profiles together are only 40% of the industry. Most organizations ran DevOps as ceremony without substance: change approval boards under a friendlier name, quarterly release trains in a sprint costume.

Now AI-native engineering is repeating it. GitLab calls it the AI Paradox: AI speeds up coding, then fragmented toolchains turn that speed into a bottleneck somewhere else. Sixty percent of teams run more than five tools, and 49% run more than five AI tools. MuleSoft found half of AI agents operate in silos and only 54% of organizations have centralized governance for them. The old bottleneck was typing. The new one is integration, review and recovery. If you only make the fast part faster, it's a faster typewriter. And if the agent that writes the code and the people who live with it stay on opposite sides of a wall, that's Debois's 2008 complaint, one layer higher.
-->

---
layout: boxes
title: Three frameworks, one shared assumption
boxes:
  - title: DORA (2014)
    detail: Speed and stability, commit to deploy. Four key metrics.
  - title: SPACE (2021)
    detail: Productivity is multi-dimensional. Satisfaction, well-being, collaboration.
  - title: DX Core 4 (2024)
    detail: Unifies DORA and SPACE and links engineering effort to business impact.
---

All three assume a human is the one typing.

<!--
In 2014 DORA set the gold standard for measuring DevOps pipeline health, proving that speed and stability are not trade-offs. In 2021 SPACE added a human-centric model: productivity is multi-dimensional, and satisfaction, well-being and collaboration count. In 2024 DX Core 4 tried to unify the two and tie engineering effort to business outcomes. Largely, these frameworks are aimed at the business and its bottom line, not the developer. Anyone using them? Good value in all three.

Here is the twist for this talk: every one of them quietly assumes a human is the one typing. When an agent writes the code, what do they still measure? That is the rest of this talk.
-->

---
layout: image-feature
side: right
image: /images/slides/conversation-shift.png
imageAlt: "Bar chart of intended audience: DORA reaches DevOps teams and engineering leaders, SPACE reaches the C-suite, and GetDX Core 4 reaches the highest level of the business"
---

## The audience moved up

Each framework pulled the conversation a little further from the developer and a little closer to the boardroom.

<style>
/* Charts must not be cropped: show the whole image inside its panel instead of
   filling it. :deep() because the layout renders the image element. */
:deep(.wwt-image-feature__image) {
  background-size: contain !important;
  background-repeat: no-repeat;
  background-position: center;
  background-color: #114365;
}
</style>

<!--
Look at who each framework talks to. DORA speaks to DevOps teams and engineering leaders. SPACE reaches up to the C-suite. Core 4 is built to be a shared language for the whole organization, all the way up. That's a reasonable thing to want, and it's also why these frameworks end up aimed at the business and its bottom line, not at the developer. The chart is illustrative, not survey data. The shift is the point: the conversation moved from pipeline metrics to business-aligned frameworks, and the practitioner got less airtime on the way.
-->

---
layout: boxes
title: "DORA: five metrics, one blind spot"
boxes:
  - title: Deployment Frequency
    detail: How often you ship. Misleading alone once AI writes 30% to 70% of committed code.
  - title: Lead Time for Changes
    detail: Commit to production. Pair it with AI attribution.
  - title: Change Failure Rate
    detail: Share of changes that cause a failure in production.
  - title: Failed Deployment Recovery Time
    detail: The new name for Mean Time to Recovery.
  - title: Deployment Rework Rate
    detail: Joined the original four in 2024.
---

None of the five can tell you whether a person or a model wrote the change.

<style>
/* Tighter card type so the grid and any closing line clear the footer.
   :deep() because the layout and BoxCard render these elements. */
:deep(.wwt-boxes__grid) {
  gap: var(--wwt-space-4) !important;
  margin-top: var(--wwt-space-4) !important;
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
DORA has tracked five metrics since 2024, when Deployment Rework Rate joined the original four and Mean Time to Recovery became Failed Deployment Recovery Time. They are still the right metrics. They tell you what is happening. They don't tell you why, and they can't tell you whether a person or a model wrote the change. That's a real attribution gap. And once AI writes somewhere between 30% and 70% of committed code, deployment frequency and lead time on their own turn misleading. Pair them with AI attribution, and look at throughput by percentile, not average. We'll come back to that. Source: WWT, "Your AI adoption number is lying to you."
-->

---
layout: image-feature
side: left
image: /images/slides/space-5-dimensions.png
imageAlt: "Radar chart of the five SPACE dimensions comparing a balanced team with a struggling team. The struggling team scores lower on four dimensions and highest on Activity."
---

## Activity is the easy dimension to fake

The struggling team scores lower on four dimensions, and highest on Activity.

<style>
/* Charts must not be cropped: show the whole image inside its panel instead of
   filling it. :deep() because the layout renders the image element. */
:deep(.wwt-image-feature__image) {
  background-size: contain !important;
  background-repeat: no-repeat;
  background-position: center;
}
</style>

<!--
SPACE gave us five dimensions: satisfaction and well-being, performance, activity, communication and collaboration, and efficiency and flow. On this radar, the balanced team is stronger almost everywhere. The struggling team wins on exactly one axis: activity. That was already a trap with humans. With agents it's a trap you can fall into in an afternoon, because an agent can inflate commits, PRs and tickets closed in minutes. The other four dimensions are still about people: whether they're satisfied, whether they collaborate, whether they're in flow. The chart is illustrative, from the old version of this talk.
-->

---
layout: image-feature
side: right
image: /images/slides/getdx-four-pillars.png
imageAlt: "Stacked bar chart of how a startup, a mature tech company and a legacy enterprise split engineering time between new capabilities, maintenance and bugs, and technical debt. The legacy enterprise spends the least on new capabilities."
---

## Where does the time go?

An agent buys you capacity. What you spend it on is the DevEx question.

<style>
/* Charts must not be cropped: show the whole image inside its panel instead of
   filling it. :deep() because the layout renders the image element. */
:deep(.wwt-image-feature__image) {
  background-size: contain !important;
  background-repeat: no-repeat;
  background-position: center;
}
</style>

<!--
DX Core 4 asks one question the others skip: what share of engineering time goes to new capabilities versus maintenance and debt? Look at the legacy enterprise bar. Most of the time goes to keeping the lights on. Now add an agent. If it turns capacity into more features, you've bought more code to maintain. Code is a liability, not an asset. Its long-term operating cost outweighs the cost of writing it. Hold that thought, because it comes back at the end: where does the freed capacity go? The chart is illustrative. It's not survey data, so don't quote the percentages.
-->

---
layout: stats
title: Throughput is a vanity metric
clicks: 0
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
/* Source line, pinned above the footer (the stats layout has no body slot). */
/* Show every stat at once, with no click-through. The layout reveals stats with
   v-clicks, so keep them visible here and tell Slidev (clicks: 0) that this
   slide has no click steps. */
:deep(.slidev-vclick-hidden) {
  opacity: 1 !important;
  pointer-events: auto !important;
}
.wwt-stats::after {
  content: "Sources: CircleCI 2026 State of Software Delivery and its July 2026 follow-up.";
  position: absolute;
  left: 5rem;
  right: 5rem;
  bottom: 3.5rem;
  font-size: var(--wwt-text-caption);
  color: var(--wwt-ink-muted);
}
</style>

<!--
Lines of code were always gameable. Now a defensible-looking diff is free, so volume measures nothing. CircleCI split the same pipeline data by branch type. Feature-branch throughput rose for nearly every team, a 15% gain for the median team. Main-branch throughput, the code that actually reaches customers, fell 7% for that same median team. And the main-branch success rate hit 70.8%, the lowest in five years, against a 90% benchmark. CircleCI's July 2026 follow-up shows it recovering to 76.7%, still short of the mid-80s teams hit in 2023 and 2024.

Developers are producing more code than ever. Very little of the increase is reaching production. If velocity is the only thing you measure, the measurement is hiding the problem.
-->

---
layout: stats
title: The verification tax has a price tag
clicks: 0
stats:
  - value: "250"
    label: hours lost a year
    caption: 5 changes a day, success rate down from 90% to 70%
  - value: "12"
    label: engineers' worth of friction
    caption: Same drop at 500 changes a day
  - value: "$900K"
    label: a year, agent-heavy workflows
    caption: 50 developers, about 3,000 changes a month
  - value: "$700K+"
    label: recovered
    caption: By validating earlier in the loop
---

<style>
/* Size every stat value from its column's width so all columns match and none
   wraps. Each .wwt-stat becomes a size container and the value is set in
   container-width units (cqi). nowrap and overflow-wrap: normal stop the
   theme's break-anywhere rule splitting values. */
:deep(.wwt-stat) {
  container-type: inline-size;
}
:deep(.wwt-stat__value) {
  font-size: 20cqi !important;
  white-space: nowrap;
  overflow-wrap: normal;
}
/* Show every stat at once, with no click-through (clicks: 0 in the frontmatter
   tells Slidev this slide has no click steps). */
:deep(.slidev-vclick-hidden) {
  opacity: 1 !important;
  pointer-events: auto !important;
}
/* Source line, pinned above the footer (the stats layout has no body slot). */
.wwt-stats::after {
  content: "Source: CircleCI 2026 State of Software Delivery and its July 2026 follow-up. Modeled scenarios, not measurements.";
  position: absolute;
  left: 5rem;
  right: 5rem;
  bottom: 3.5rem;
  font-size: var(--wwt-text-caption);
  color: var(--wwt-ink-muted);
}
</style>

<!--
Slow feedback has a cost, and CircleCI modeled it. A team pushing five changes a day whose main-branch success rate drops from 90% to 70%, at a 60-minute recovery time, loses roughly 250 hours a year to debugging and blocked releases. At 500 changes a day, where CircleCI's top teams operate, that same drop equals twelve full-time engineers lost to friction that never shows up on a headcount report. In dollars: a 50-developer team shipping about 3,000 changes a month can spend roughly $900,000 a year on unoptimized, agent-heavy workflows, much of it agents sitting idle waiting for feedback. Move validation earlier in the loop and you recover $700,000 or more of that. These are modeled scenarios, so say so. But notice who's waiting: now it's the agents too.
-->

---
layout: stats
title: "Tokenmaxxing: activity, not outcomes"
clicks: 0
stats:
  - value: "85,000"
    label: employees on a leaderboard
    caption: Reportedly tracked at one company
  - value: "60T"
    label: tokens in a single month
    caption: Consumed by those employees
  - value: "4"
    label: months to burn a year's budget
    caption: At another company
---

<style>
/* Size every stat value from its column's width so all columns match and none
   wraps. Each .wwt-stat becomes a size container and the value is set in
   container-width units (cqi). nowrap and overflow-wrap: normal stop the
   theme's break-anywhere rule splitting values. */
:deep(.wwt-stat) {
  container-type: inline-size;
}
:deep(.wwt-stat__value) {
  font-size: 24cqi !important;
  white-space: nowrap;
  overflow-wrap: normal;
}
/* Show every stat at once, with no click-through (clicks: 0 in the frontmatter
   tells Slidev this slide has no click steps). */
:deep(.slidev-vclick-hidden) {
  opacity: 1 !important;
  pointer-events: auto !important;
}
/* Source line, pinned above the footer (the stats layout has no body slot). */
.wwt-stats::after {
  content: "Source: industry press reports, as summarized in WWT's post on how AI amplifies engineering teams.";
  position: absolute;
  left: 5rem;
  right: 5rem;
  bottom: 3.5rem;
  font-size: var(--wwt-text-caption);
  color: var(--wwt-ink-muted);
}
</style>

<!--
This year gave us the clearest example of the vanity-metric mistake. Several major tech companies briefly built internal leaderboards ranking employees by how many AI tokens they consumed. It has a name now: tokenmaxxing. One company reportedly tracked 85,000 employees and 60 trillion tokens in a single month. Another burned through an entire year's AI budget in four months. Both walked it back within weeks, for the obvious reason. Measuring tokens consumed without measuring what shipped rewards activity, not outcomes. It's Goodhart's Law with a billing page. These figures are reported, not audited, so attribute them. Don't name the companies.
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

Worth knowing before someone asks: METR tried to repeat the study in 2026 and the design broke down. Too many developers refused to work without AI, even when they were paid to, so there was no clean control group. That tells you something too. The dependence is real enough to get in the way of measuring the effect. And METR's own follow-up pointed toward a speedup, but METR calls that data unreliable. Treat both as snapshots, not verdicts.
-->

---
layout: boxes
title: Who pays the verification tax?
boxes:
  - title: Quiet failures
    detail: 61% of developers name code that looks correct but isn't reliable. It compiles. The tests pass.
  - title: The experience gap
    detail: Less experienced developers report the biggest gains, and the most "looks correct" failures.
  - title: Tool sprawl
    detail: Four AI tools per team on average. For one popular assistant, 52% of use is on personal accounts.
  - title: The fix
    detail: Not a ban, and not less access. Senior review on AI-assisted code, and a sanctioned tool that beats the shadow one.
---

Source: Sonar 2026 State of Code Developer Survey; MIT Project NANDA.

<style>
/* Tighter card type so the grid and any closing line clear the footer.
   :deep() because the layout and BoxCard render these elements. */
:deep(.wwt-boxes__grid) {
  gap: var(--wwt-space-4) !important;
  margin-top: var(--wwt-space-4) !important;
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
Who actually pays? Start with the failure mode. Junior-written code tends to fail loudly: a compile error, an obvious crash. AI-generated errors are quiet. It compiles, the tests pass, the logic reads fine, and weeks later it misbehaves under a condition nobody tested. Sixty-one percent of developers named exactly that. Second, the experience gap: less experienced developers report the largest productivity gains and the highest rates of that quiet failure. The response isn't to cut their access. It's to put senior review specifically on top of AI-assisted code, backed by tooling that catches issues no matter who wrote the first draft. Third, sprawl. The average team uses four AI tools, and a lot of that runs through personal accounts. MIT's NANDA research calls it the shadow AI economy: official tools underdeliver, so people route around them. A ban doesn't fix that. A sanctioned option that's genuinely better does. And accountability for what ships still sits with the person who approved it, not the model that wrote it.
-->

---
layout: stats
title: Where teams actually start
clicks: 0
stats:
  - value: "7"
    label: team archetypes
    caption: DORA's statistical profiles
  - value: "~38%"
    label: in genuine difficulty
    caption: Process gaps, tech debt, heavy overhead
  - value: "~40%"
    label: already performing well
    caption: Stable systems, healthy delivery
---

<style>
/* Size every stat value from its column's width so all columns match and none
   wraps. Each .wwt-stat becomes a size container and the value is set in
   container-width units (cqi). nowrap and overflow-wrap: normal stop the
   theme's break-anywhere rule splitting values. */
:deep(.wwt-stat) {
  container-type: inline-size;
}
:deep(.wwt-stat__value) {
  font-size: 24cqi !important;
  white-space: nowrap;
  overflow-wrap: normal;
}
/* Show every stat at once, with no click-through (clicks: 0 in the frontmatter
   tells Slidev this slide has no click steps). */
:deep(.slidev-vclick-hidden) {
  opacity: 1 !important;
  pointer-events: auto !important;
}
/* Source line, pinned above the footer (the stats layout has no body slot). */
.wwt-stats::after {
  content: "Source: DORA 2025 State of AI-Assisted Software Development, via WWT.";
  position: absolute;
  left: 5rem;
  right: 5rem;
  bottom: 3.5rem;
  font-size: var(--wwt-text-caption);
  color: var(--wwt-ink-muted);
}
</style>

<!--
DORA sorted its survey into seven statistical team archetypes, and the distribution matters if you're deciding how fast to expand agentic workflows. Roughly 38% of teams are in genuine difficulty: fundamental process gaps, unresolved tech debt, or overhead heavy enough to absorb any efficiency gained elsewhere. Roughly 40% are already performing well. The rest sit in between. For that first group, adding AI without fixing the platform underneath makes existing problems more visible and more expensive, not less. The right first investment is the platform, not the tooling layer on top. Be honest about which group you're in before you scale.
-->

---
layout: boxes
title: Four pillars of world-class DevEx
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
The three original pillars from the ACM Queue framing (feedback loops, cognitive load, flow state) all survive contact with agentic tooling. They just get harder. The fourth is emerging in 2026 conversations: calibrated trust and governance. Teams that treat "which agent can touch which part of the codebase, under what review policy" as a deliberate design decision see fewer disasters than teams that just let the agent open PRs.
-->

---
layout: boxes
title: "Feedback loops, agent edition"
boxes:
  - title: Check the output early
    detail: Linting and static analysis in the IDE and pre-commit hooks, before a PR exists.
  - title: Tests ship with the change
    detail: Agents deliver a test alongside every change, not after it.
  - title: Self-healing test automation
    detail: Stops teams disabling flaky tests. Reported coverage moves from 30-50% to 80-95%.
  - title: Progressive delivery, auto-rollback
    detail: Small blast radius, telemetry in charge. Aims a 72-minute median recovery at seconds.
---

Source: WWT, "AI doesn't fix broken engineering teams, it amplifies them."

<style>
/* Tighter card type so the grid and any closing line clear the footer.
   :deep() because the layout and BoxCard render these elements. */
:deep(.wwt-boxes__grid) {
  gap: var(--wwt-space-4) !important;
  margin-top: var(--wwt-space-4) !important;
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
Fast, high-quality feedback loops is the first pillar, and it's where the verification tax bites hardest. Four moves. One: shift left. Put static analysis and linting where the agent's output lands, in the IDE and in pre-commit hooks, so problems die before a PR exists. Two: make verification part of generation. Agents that ship a test with the change, a rollback plan with the deploy and a rationale with the diff. Three: self-healing test automation. As AI increases volume, test suites break more often, and teams under pressure start disabling flaky tests instead of fixing them. Automated recovery breaks that cycle. Organizations using it report coverage moving from the 30 to 50% range to 80 to 95%, with payback dropping from 12 to 24 months to about three. Four: progressive delivery with automatic rollback. Ship to a small slice of traffic, let telemetry govern the rollout, and revert automatically if error budgets break. Applied well, that turns a 72-minute recovery into seconds. That's human oversight that scales.
-->

---
layout: boxes
title: "Cognitive load, agent edition"
boxes:
  - title: Small batches
    detail: Small, reviewable diffs. A stranger's reasoning has to fit in your head.
  - title: A rationale with every diff
    detail: The agent says what and why, not just what changed.
  - title: One set of conventions
    detail: Standard style, linting and docs that humans and agents both read.
  - title: An independent verification layer
    detail: Teams without one were 80% more likely to report more AI-linked outages.
---

Source: Sonar 2026, via WWT.

<style>
/* Tighter card type so the grid and any closing line clear the footer.
   :deep() because the layout and BoxCard render these elements. */
:deep(.wwt-boxes__grid) {
  gap: var(--wwt-space-4) !important;
  margin-top: var(--wwt-space-4) !important;
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
The old cognitive-load pillar was about limited working memory: wrestling with complex systems or bad docs leaves less room for solving problems. Agents change the shape of that load. It used to be recalling syntax. Now it's verifying a stranger's reasoning, which is a heavier tax. So make that reasoning small and legible. Small batches, because a four-thousand-line diff can't be understood. A rationale with every diff. Standardized style and linting, meaningful commit messages and centralized documentation, the same boring basics from the old list, now read by humans and agents. And an independent verification layer. Sonar found teams without deterministic verification tooling were 80% more likely to report increased outage frequency tied to AI adoption, and 46% more likely to say AI had degraded code quality overall. High rework is still the signal that cognitive load is too high.
-->

---
layout: boxes
title: "Flow state, agent edition"
boxes:
  - title: High-signal notifications
    detail: Agent check-ins batched and prioritized, not pinged all day.
  - title: Review with context
    detail: PRs arrive with what a reviewer needs to finish in one pass.
  - title: One standard environment
    detail: Automated setup, shared by humans and agents.
  - title: Safe to say "I don't trust this"
    detail: Psychological safety to push back on agent output without becoming the bottleneck.
---

<!--
Flow is where deep, creative work happens, and it needs clear goals, immediate feedback and protection from interruptions. It can take more than fifteen minutes to regain focus after a single one. Agents add a new kind of interruption: you get pulled into reviewer mode several times an hour. So treat agent check-ins like any other notification source. Batch them, prioritize them, make them high-signal. Give reviewers contextual tooling so a review is one pass, not a scavenger hunt. Standardize environments so humans and agents work from the same setup. And the one people forget: psychological safety. If saying "I don't trust this output" feels like slowing the team down, people will approve things they shouldn't. Remember, only 48% always verify before committing.
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
-->

---
layout: timeline
title: "If it can happen there..."
events:
  - date: Dec 2025
    label: Elevated permissions
    detail: Bypasses two-person approval, deletes and rebuilds the environment. 13-hour outage.
  - date: "Mar 2, 2026"
    label: AI-assisted changes
    detail: 120,000 lost orders. 1.6 million website errors.
  - date: "Mar 5, 2026"
    label: Worse
    detail: "~6.3M lost orders, a 99% drop in North American order volume, ~6 hours down. Amazon disputes AI as the primary cause."
  - date: "Amazon's fix"
    label: Mandatory review, reinstated
    detail: Senior-engineer sign-off on AI changes. A human, back in the loop.
---

<!--
In December 2025 one of Amazon's internal AI agents, a system called Kiro built to handle operational and coding work autonomously, was pointed at a production issue and decided the right move was to delete the environment and rebuild it. [click] It ran under an engineer's elevated permissions, so the two-person approval that normally gates a change that size didn't apply. Result: a thirteen-hour outage.

[click] In March 2026, an incident tied to AI-assisted changes caused 120,000 lost orders and 1.6 million website errors. [click] Three days later a second, worse incident took the U.S. site down for about six hours, a 99% drop in North American order volume, roughly 6.3 million lost orders. Amazon disputes that AI was the primary cause and has called it user error. That is worth saying out loud, even though it doesn't change what happened.

[click] The part to remember: the response was to reinstate mandatory senior-engineer review for AI-assisted changes. A human back in the loop, because an agent had been handed disposal authority instead of proposal authority. If it can happen at Amazon, a company with that much operational sophistication, "we're careful" isn't a strategy.
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
layout: stats
title: Your adoption number is lying to you
clicks: 0
stats:
  - value: "42%"
    label: of committed code is AI-assisted
    caption: Expected to reach 65% by 2027
  - value: "72%"
    label: use AI tools daily
    caption: Of developers who've tried them
  - value: "35%"
    label: use personal accounts
    caption: Your official number can't see them
---

<style>
/* Size every stat value from its column's width so all columns match and none
   wraps. Each .wwt-stat becomes a size container and the value is set in
   container-width units (cqi). nowrap and overflow-wrap: normal stop the
   theme's break-anywhere rule splitting values. */
:deep(.wwt-stat) {
  container-type: inline-size;
}
:deep(.wwt-stat__value) {
  font-size: 24cqi !important;
  white-space: nowrap;
  overflow-wrap: normal;
}
/* Show every stat at once, with no click-through (clicks: 0 in the frontmatter
   tells Slidev this slide has no click steps). */
:deep(.slidev-vclick-hidden) {
  opacity: 1 !important;
  pointer-events: auto !important;
}
/* Source line, pinned above the footer (the stats layout has no body slot). */
.wwt-stats::after {
  content: "Source: Sonar 2026 State of Code Developer Survey. Shadow-use context: MIT Project NANDA (preliminary).";
  position: absolute;
  left: 5rem;
  right: 5rem;
  bottom: 3.5rem;
  font-size: var(--wwt-text-caption);
  color: var(--wwt-ink-muted);
}
</style>

<!--
Ask most engineering leaders how AI adoption is going and you'll get a number: seats, or the percent of the org that used AI this month. Maybe a slide with a big satisfied 87% on it. It feels like progress. It tells you how many people picked up the tool, and nothing about whether your delivery system got faster, safer or more expensive. Look at Sonar's numbers. AI is 42% of committed code, heading to 65% by 2027, and 72% of developers who've tried it use it daily. That's about as strong an adoption signal as exists. And remember the 96% who don't fully trust it, and the 48% who always verify. High adoption, low trust, inconsistent verification. A pure adoption metric will never show you that. Also: 35% use AI tools on personal accounts, and MIT's preliminary research puts it above 90% of employees using personal AI tools for work. The gap between your official number and that one is a governance and security blind spot. DORA describes the early phase as a J-curve: adoption correlates with more delivery instability first, because code volume outruns the review and deploy infrastructure. You only know you're in one if you track more than the adoption number.
-->

---
layout: boxes
title: Measure in four layers
boxes:
  - title: AI footprint
    detail: Share of code that's AI-assisted. Sanctioned vs. shadow gap. Agent- vs. human-initiated PRs.
  - title: Delivery
    detail: DORA's five, by percentile, not average. Add AI attribution.
  - title: Verification
    detail: Merge Efficiency Ratio. Review time and no-review merges by author type. Cost per shipped change.
  - title: Outcome
    detail: AI-attributed change failure rate. Incidents per PR. Perceived vs. measured gap. Pilot-to-production rate.
---

Source: WWT, "Your AI adoption number is lying to you."

<style>
/* Tighter card type so the grid and any closing line clear the footer.
   :deep() because the layout and BoxCard render these elements. */
:deep(.wwt-boxes__grid) {
  gap: var(--wwt-space-4) !important;
  margin-top: var(--wwt-space-4) !important;
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
Here's the structure I'd use for a dashboard. Layer one, AI footprint: how much of your pipeline AI is touching. Percent of committed code that's AI-assisted is the real denominator for everything else. Add the gap between sanctioned and shadow use, and the share of PRs an agent opened without a human starting them. Most organizations don't track that last one, and no industry figure exists yet, which is itself a signal. Layer two, delivery: DORA's five metrics, with throughput by percentile, not average. Layer three, verification, where the friction moved: Merge Efficiency Ratio, review time and no-review-merge rate split by author type, and cost per shipped change. Layer four, outcome: AI-attributed change failure rate against your overall number, incidents per PR, the perceived-versus-measured productivity gap, and your pilot-to-production conversion rate. Two of these have no published baseline yet. Establish your own before you set targets, and revisit as your team's AI fluency grows.
-->

---
layout: stats
title: The verification layer, measured
clicks: 0
stats:
  - value: "+441%"
    label: median PR review time
    caption: Low vs. high AI-adoption periods
  - value: "+31%"
    label: PRs merged with no review
    caption: Same comparison, 22,000 developers
  - value: "+242.7%"
    label: incidents per PR
    caption: Odds of an incident per merged change more than tripled
  - value: "−31%"
    label: cost per shipped change
    caption: Elite teams, while main-branch throughput grew 72%
---

<style>
/* Size every stat value from its column's width so all columns match and none
   wraps. Each .wwt-stat becomes a size container and the value is set in
   container-width units (cqi). nowrap and overflow-wrap: normal stop the
   theme's break-anywhere rule splitting values. */
:deep(.wwt-stat) {
  container-type: inline-size;
}
:deep(.wwt-stat__value) {
  font-size: 20cqi !important;
  white-space: nowrap;
  overflow-wrap: normal;
}
/* Show every stat at once, with no click-through (clicks: 0 in the frontmatter
   tells Slidev this slide has no click steps). */
:deep(.slidev-vclick-hidden) {
  opacity: 1 !important;
  pointer-events: auto !important;
}
/* Source line, pinned above the footer (the stats layout has no body slot). */
.wwt-stats::after {
  content: "Sources: Faros AI 2026 telemetry (22,000 developers); CircleCI 2026 Q2 report. Via WWT.";
  position: absolute;
  left: 5rem;
  right: 5rem;
  bottom: 3.5rem;
  font-size: var(--wwt-text-caption);
  color: var(--wwt-ink-muted);
}
</style>

<!--
This is the verification layer in real telemetry. Faros AI looked at 22,000 developers and compared low and high AI-adoption periods. Median PR review time rose 441%. PRs merging with no review at all rose 31%. Read those two together. Rising review time means someone is looking. A rising no-review rate means the safety net is being skipped. And incidents per PR rose 242.7%, so the odds of a production incident per merged change more than tripled. Paired with the no-review rate, that's the clearest sign that speed and safety have decoupled. Now the good news, from CircleCI: elite organizations grew main-branch throughput 72% in a year while cutting cost per shipped change 31%. More throughput at lower cost per change is the proof AI is paying for itself. The elite teams are the ones who built the verification layer.
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

Each of these gets its own slide next: what changes, and what to do about it.
-->

---
layout: boxes
title: "Cycle time, agent edition"
boxes:
  - title: Count the time to understand
    detail: Cycle time ends when the team understands what shipped, not when it merges.
  - title: Small batches, still
    detail: Enforce batch size on agent output too. Big agent diffs stall in review.
  - title: Watch for rubber stamps
    detail: A fast merge on unreviewed code isn't a win.
  - title: Validate earlier
    detail: CI/CD and test automation the agent can run before it asks a human.
---

<!--
Cycle time can look great right up until an unreviewed agent change causes an incident. So change what it measures: include the time to understand what shipped. Keep the old levers, because they still work: small batch sizes, test automation, CI/CD and removing blockers. But enforce them on agent output too, because agents will happily produce a diff nobody can review. And watch for rubber-stamped merges. A fast merge on unreviewed code is not a win, it's a deferred incident.
-->

---
layout: boxes
title: "PR review time, agent edition"
boxes:
  - title: Small PRs, enforced in CI
    detail: Cap diff size automatically. Agents will open the 4,000-line PR.
  - title: Descriptions that explain
    detail: Intent, scope and test evidence in every agent PR description.
  - title: Rotate reviewers
    detail: Spread the load so review isn't one person's invisible tax.
  - title: Visible SLAs, two numbers
    detail: Track review time beside the no-review merge rate.
---

<!--
PR review time is often the real bottleneck now. Generation got fast and review didn't. The old playbook still applies, with a sharper edge. Enforce small-PR guidelines in automation, not in a wiki page. Require clear descriptions: what the change is for, what it touches and what proves it works. Rotate reviewers, the reviewer-roulette idea, so the work spreads. And publish SLAs, but always show two numbers together: review time and no-review merge rate. Review time alone can be gamed by simply not reviewing.
-->

---
layout: boxes
title: "Rework rate, agent edition"
boxes:
  - title: Split human from AI
    detail: Track rework on AI-authored changes separately.
  - title: Tighten specs and scope
    detail: A rising AI rework rate means clearer acceptance criteria, not abandoning the tooling.
  - title: Enforce the definition of done
    detail: Tests, rationale and review are part of done for agent work.
  - title: Close the feedback loop
    detail: Feed rework causes back into prompts, rules and repo guidance.
---

<!--
Rework rate is the share of work redone after it's committed. Split it by author: human-authored and AI-authored. If the AI number climbs, the answer is almost never "stop using it." It's tighten the specs and the scope: clearer acceptance criteria, smaller tasks. Make the definition of done explicit for agent work and enforce it. And close the loop: when you find why something was reworked, put that lesson where the agent will see it next time, in prompts, rules and repo guidance.
-->

---
layout: boxes
title: "Meeting load, agent edition"
boxes:
  - title: Name "agent sync"
    detail: Coordinating what three agents did overnight is real work. Put it on the ledger.
  - title: End status theater
    detail: No meetings where a human narrates what an agent already logged.
  - title: Async by default
    detail: Agent logs and PR summaries replace status updates.
  - title: Protect the quiet time
    detail: Keep the meeting-free blocks. Don't let approvals eat them.
---

<!--
Who spends more time in meetings than developing? Agents add a new category: agent sync. Coordinating what three agents are doing overnight is real work, and it's invisible if you don't name it. So add it to the ledger. Watch for status-theater meetings where a human narrates what an agent already logged. The agent's log is the status update. Lean on async tools and practices, and protect your meeting-free time, because approvals and check-ins will quietly colonize it.
-->

---
layout: boxes
title: "Time to first commit, agent edition"
boxes:
  - title: Time to first trusted agent task
    detail: "The new-hire metric: how fast until they can direct and review an agent."
  - title: A second onboarding track
    detail: Agentic workflows, permission tiers and review conventions.
  - title: Ready-to-run starters
    detail: Templates and automated setup, with agent configuration included.
  - title: Small first tasks
    detail: Short, scoped "good first issues", with mentorship paired to tooling.
---

<!--
New-hire onboarding sets the tone for a developer's experience, especially on smaller teams. Time to first commit still matters, and it gets a sibling: time to first trusted agent task. Onboarding now has a second track: how your team uses agents, what each permission tier allows and what your review conventions are. Keep the old basics: ready-to-run starters, automated environment setup, clear contribution guidelines, small first tasks and real mentorship paired with tooling.
-->

---
layout: boxes
title: "Perceived focus time, agent edition"
boxes:
  - title: Count agent check-ins
    detail: Approvals and check-ins are their own interruption category.
  - title: Fewer, better pings
    detail: Batch and prioritize notifications from agents.
  - title: Fast builds, real caching
    detail: Agents waiting on slow builds burn money and your attention.
  - title: Errors a human can read
    detail: Clear error messages help the agent and the person.
---

<!--
Perceived focus time is subjective, and it's critical for productivity and job satisfaction. Count agent check-ins and approvals as their own interruption category, otherwise your focus numbers will quietly lie. Reduce notification overload by batching. Invest in faster builds, incremental builds and caching: CircleCI found agents idling while they wait for feedback is a big part of that $900,000 figure. And improve error messages and debugging tools, because they help the agent as much as the human.
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

If AI change failure rate runs meaningfully above your human baseline, that isn't an argument against the tooling. It's a signal to tighten governance and review before scaling usage.
-->

---
layout: boxes
title: Build a healthy measurement culture
boxes:
  - title: No silver bullet
    detail: No framework is one. Agentic tooling included.
  - title: Improvement, not judgment
    detail: Never a way to rank people or justify headcount cuts.
  - title: Explain the why
    detail: Every new agent metric comes with its reason.
  - title: Involve your team
    detail: Set permission tiers with the team, not for them.
  - title: Trends, not absolutes
    detail: Baseline first, then watch the direction.
  - title: Numbers plus voices
    detail: Combine the data with the qualitative. Do people trust this?
---

<style>
/* Tighter card type so the grid and any closing line clear the footer.
   :deep() because the layout and BoxCard render these elements. */
:deep(.wwt-boxes__grid) {
  gap: var(--wwt-space-4) !important;
  margin-top: var(--wwt-space-4) !important;
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
Building a healthy measurement culture is foundational to any DevEx initiative. No framework is a silver bullet, agentic tooling included. Aim for continuous improvement, never judgment, and never a way to justify headcount cuts. Explain the why behind every new agent metric. Involve the team in setting permission tiers instead of handing down policy. Watch trends, not absolutes. And combine the numbers with the qualitative: do people actually trust this? Discuss it with your teams. Don't just decide and spring it on them. That's not very practitioner-centric, is it?
-->

---
layout: process
title: Putting it into practice
steps:
  - title: Start small and contained
    detail: A high-velocity, non-critical surface. Internal tooling or a docs pipeline.
  - title: Measure outcomes, not activity
    detail: Main-branch throughput, 90% success, 60-minute recovery, reviewer load.
  - title: Set expectations early
    detail: Before the J-curve dip. Many AI initiatives lose funding over a temporary dip.
  - title: Reinvest the returns
    detail: Into quality, security and debt. Code is a liability, not an asset.
---

<style>
/* Sentence-length steps are too wide for the layout's across-the-page columns.
   Lay them out as rows: number | step name | detail. The markup is unchanged,
   so the click-through reveal still works. :deep() because the layout renders
   the list. */
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
Four steps before you scale agentic workflows further. One: start on a high-velocity, non-critical surface, like internal tooling or a documentation pipeline, anywhere an early mistake has a contained blast radius. Two: measure what reflects outcomes. Main-branch throughput, success rate against a 90% benchmark, recovery time against a 60-minute benchmark, and reviewer load in whatever form you can track. Three: set expectations with leadership before the adoption curve dips, not after. DORA's research shows many AI initiatives lose funding not because the technology fails, but because a temporary dip gets mistaken for failure. Four: when returns show up, reinvest deliberately. The capacity freed by reducing rework should go to quality, security and paying down the debt the push for speed created, not straight into more feature pressure. That's how you end up back at the start of the same dip.
-->

---
layout: quote
dark: true
attribution: DORA research
---

"We don't measure AI by the code it writes, but by the bottlenecks it clears."

<!--
If you take one line from the research side of this talk, take this one. The organizations getting real value from AI aren't the ones generating the most code. They're the ones that built the discipline to verify it, ship it and free their people to do the work that needs human judgment. Don't panic. Build the verification layer first.
-->

---
layout: default
---

# Ask the people doing the work

<img class="post" src="/images/slides/bluesky-devex-culture-post.jpg" alt="Bluesky post from Jeremy Meiss, November 18, 2024: if your company does not have a process for gathering feedback on your product and tools, you will not have a good Developer Experience" />

<p class="post-cap">Then act on what they tell you.</p>

<style>
/* The post is a wide screenshot, so show it whole instead of cropping it into a
   half-width image panel. */
.post {
  display: block;
  width: 88%;
  margin: 1.5rem auto 0;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(10, 11, 25, 0.18);
}
.post-cap {
  margin: 1.25rem 0 0;
  text-align: center;
  font-size: 28px;
  color: var(--wwt-ink-muted);
}
</style>

<!--
Investing in developer experience is a direct investment in your organization's capacity to innovate. I posted this in late 2024, and it holds up with agents in the room: if you don't have a process for gathering feedback, internal and external, on the tools you use, you won't have a good developer experience, and I seriously question the commitment. Surveys, retros, office hours, whatever fits. Ask the people working with the agents how it's really going. Then act on the answer.
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

And a final thought: black lives matter, trans rights are human rights, love is love, abortion is healthcare, and fuck ICE.
-->
