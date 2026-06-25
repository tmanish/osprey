<div align="center">
<img src="docs/assets/osprey-mark.png" alt="Osprey" width="84" />

# Osprey

**A user-centered approach to agent orchestration.**

*Concept and Design by [Manish Todkari](#about-the-designer), Senior Product Designer*

<a href="https://tmanish.github.io/osprey/">View the formatted documentation (recommended) →</a>
<br/>

<a href="https://tmanish.github.io/osprey/Osprey.html">View the live prototype →</a>

</div>

---

Osprey is an orchestration platform for building, assigning, and supervising teams of autonomous agents. You assemble a group of agents, design the work they'll do, hand out the tasks, and then watch the whole thing run, live.

But the reason this project exists isn't the orchestration engine. It's the interface. Most tools in this space are built engine-first: powerful underneath, bewildering on top, usable only by the person who built them. In this emerging agentic orchestration space, very few product designers have spent the time to understand the technology and make it usable and human-friendly, to take something genuinely new and stop it from feeling intimidating or complex. I built Osprey the other way around. It starts from the people who have to *use* an orchestration system, the person designing the automation and the person responsible for trusting it once it's running, and works backward to the screen.

This document explains how Osprey works from a user's point of view, and lays out the design principles behind it. If you're building an agent platform of your own, this is meant to be borrowed from.

## The problem with how orchestration tools are usually designed

Autonomous agents are a genuinely new idea for most people. Asking someone to learn that new idea *and* fight an unfamiliar, intimidating interface at the same time is how good technology fails to get adopted.

The common failure modes are predictable:

- **The tool thinks in the machine's terms, not the user's.** It exposes graph theory, model identifiers, and internal jargon, and expects the user to translate their actual goal into that vocabulary before anything happens.
- **It optimizes for the builder and forgets the operator.** Enormous effort goes into the editor; the "is it working?" view is an afterthought of raw logs and numbers. But trust is won or lost in the running, not the building.
- **It overwhelms.** Everything is dense, everything competes for attention, so nothing stands out, and the user can't tell at a glance what matters.

Osprey is an answer to all three.

## How Osprey works

Osprey is built around a deliberately ordinary use case, a small team of agents producing a research-and-writing deliverable, because the goal is to make the *interaction model* legible to users before the domain gets complicated. The same orchestration patterns extend directly to the hard cases: complex payment systems, regulatory workflows, and other critical, consequential operations. In those domains the right way to build it is in collaboration with a product designer and a system architect, working together to identify the agent roles, their authority, and where a human has to stay in the loop.

The product is built around three jobs a person does, in the order they do them. Each has its own dedicated space, reachable from a simple rail down the left side of the screen.

### 1. Build your team, *Groups*

You start by assembling a **group of agents**, your workforce for a job. Each agent has a name, a role (Researcher, Writer, Reviewer, and so on), and two settings that make it behave like a real, finite worker rather than an infinite abstraction: how many things it can do at once, and how reliably it succeeds. Agents appear as cards with a colored monogram, so the same worker is recognizable everywhere it shows up later.

The mental model on purpose: *you are hiring a team*, not configuring software. That framing does a lot of quiet work. It makes the next two steps feel like delegation, which people already understand, instead of programming, which they often don't.

### 2. Design the work, *Build*

Next you lay out the workflow on a canvas. You drag in steps, connect them by dragging from one step to the next, and the connections draw themselves as clean arrows. A step can be a task you hand to an agent, a decision that branches the flow, a fan-out that runs several things at once, or a gather-point that waits for them all to finish.

Selecting a step opens a panel where you say what it should do and who should do it. The system quietly checks your work as you go. If a step is left disconnected or unreachable, it tells you in plain language rather than letting you discover the problem at run time.

The design goal here is *direct manipulation*: you build the thing by touching the thing. There is no separate configuration screen standing between your intent and the picture of it. What you draw is what runs.

### 3. Watch it work, *Monitor*

This is where most tools give up, and where Osprey spends its care. When you run the workflow, the monitor answers a person's questions, in the order a person actually asks them:

- **Is it working?** A single, prominent progress figure leads, not buried in a chart.
- **What is each agent doing right now?** Every agent gets its own lane with a live progress bar and its current task. The abstract "fleet" becomes a row of named individuals you can watch in parallel.
- **What's happened so far?** A running log narrates the job in plain sentences, "Search corpus A done", "Revise draft failed, retrying", "Quality gate needs revision", so you can follow the story without decoding anything.
- **Where did it get stuck, and why?** Failures and retries surface in warning colors against an otherwise calm screen, so problems find you instead of you hunting for them.

You can step through one move at a time, pause, resume, change the speed, or stop, the same controls you'd expect from anything you'd want to inspect carefully.

## The principles behind it

These are the ideas that make the experience work. They're the part worth taking with you.

### Speak the user's language, not the machine's

Every label, color, and layout choice translates the system's internal state into something a person can read at a glance. Steps show their status as a word, *running*, *done*, *failed*, not just a color, so nobody has to memorize a legend. Agents are named individuals, not opaque identifiers. The log tells a story in sentences. The interface is constantly doing the work of translation so the user never has to.

### Color means something, or it isn't used

There are exactly four status colors, and they map to the four things you ever need to know at a glance: **active**, **complete**, **needs attention**, **failed**. Everything idle stays neutral and quiet. This is the single most important discipline in the whole design. Because color is reserved for meaning, scanning a live run is effortless. Your eye is pulled only to what's happening, what broke, and what's waiting on a decision.

### Built on a custom design system

Osprey isn't assembled from an off-the-shelf component kit. I built it on my own design system, and proving that system out on a problem this demanding is one of the purposes of this prototype. An agentic interface stresses everything at once, dense state, live motion, hierarchy under pressure, so it's an honest test of whether the typography scale, spacing, color tokens, and component primitives hold up, or where they need to bend. Every screen here is an answer in the system's own vocabulary.

### Borrow a familiar language so the new ideas get the attention

Osprey speaks a visual dialect people already read fluently, clean, modern, Material-style chrome. This is deliberate. The agents and workflows are the genuinely new concepts; the buttons, cards, and navigation should feel instantly familiar so the user spends their attention on the ideas that are new, not on relearning where things live.

### Design for the operator, not just the builder

Half of orchestration is supervision, so half the design goes there. The monitor isn't a debug console bolted onto the editor. It's a first-class workspace built around the questions of the person who has to trust the system: did it work, what did it do, where did it stall. Lead with the outcome; keep the mechanism one layer down, available but never in the way.

### Make the picture boringly correct

A workflow drawn as a diagram only earns trust if the diagram is *exactly* right, every arrow meeting its step, at every zoom level, every time. The moment a connection looks even slightly off, the user stops trusting the picture, and a picture you can't trust is worse than no picture. Getting this invisibly, relentlessly correct was the hardest part of the build, and it's non-negotiable: the diagram has to disappear as a thing you think about, so you can think about your work instead.

### Restraint is a feature

There is almost no decorative motion, no shadow theater, nothing that moves or shines for its own sake. Transitions exist only to explain a change of state. Density is tuned to feel like a calm instrument, not a busy dashboard. The maturity of an operations tool shows in what it refuses to add. Every element has to earn its place or it's removed.

## How this is different from what's out there

Most agent and workflow tools descend from developer automation software and inherit its assumptions: the user is technical, the editor is the product, and the running is something you read in a log. Osprey rejects all three.

- It treats **the responsible operator as a first-class user**, not an afterthought. Supervision gets a purpose-built space, not a console.
- It makes **understanding-at-a-glance the central design problem**, and builds the color system, the agent lanes, and the information hierarchy around solving it.
- It uses a **familiar, mainstream visual language** instead of inventing a bespoke one, so a new category of software feels approachable on first contact.
- It leads with **outcomes**, not telemetry. Did it work, what did it produce, with the deep detail available but out of the way.

These aren't features on a comparison checklist. Together they're the difference between a tool someone demos once and a tool someone is willing to depend on.

## What this is, and where it goes

Osprey is a working design prototype. The engine that runs the workflows is a high-fidelity simulator. It schedules work across your agents, respects their limits, models how long things take and when they fail, retries, and routes decisions, so the *experience* can be proven against realistic behavior before being wired to live agents. The cockpit was built and instrumented first, because the cockpit is what determines whether the thing is usable at all.

The honest path from here is about closing the distance between "a polished orchestration console" and "something anyone could use to automate real work":

- **Start with the trigger.** Real automation begins with *when something happens*, a schedule, an incoming message, a form submitted, not a manual Run button. The first step of a workflow should be the event that sets it off.
- **Speak in outcomes, not graph theory.** "Do these at the same time" and "wait until they're all done" instead of fan-out and join.
- **Keep a human in the loop.** Approval steps that pause and ask a person, and a place where pending decisions wait, because "draft it, but let me approve before it sends" is the most common business pattern there is.
- **Connect to the tools people already use**, so a step can actually touch their real work.

None of these require tearing down what's here. They build on it. And the principles above, speak the user's language, reserve color for meaning, design for the operator, make the picture boringly correct, and add nothing that doesn't earn its place, are the foundation worth keeping no matter what you build on top.

## About the designer

**Manish Todkari** is a senior product designer working at the intersection of AI, FinTech, and complex product systems, with deep experience designing for major financial institutions. His work focuses on making powerful technology easier to understand, operate, and trust — especially where clarity, control, and human judgment matter.

Osprey is a self-initiated exploration of where interface craft is heading as software gains the ability to act on our behalf.

The patterns here are free to learn from and build on. Attribution appreciated.

---

<div align="center">
<sub>Osprey, a design concept · © 2026 Manish Todkari. All rights reserved.</sub>
</div>
