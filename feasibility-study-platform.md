# Case Study: A Guided Platform for Municipal Feasibility Studies

**Organization:** Holy Makkah Municipality
**Role:** Data Analyst Trainee — one of three trainees building the platform, supervised by three engineers
**Tools:** Cloudflare Workers, Cloudflare KV, Claude API, Word export · auto-deployed from GitHub
**Status:** In progress — 1 of 5 sections approved, the second under review

> The project data is internal. This page describes the problem, the approach and the results so far.

---

## The Problem

Before a municipal project goes ahead, the engineers prepare a **summarized feasibility study** with five sections:

1. **Strategic** — how the project fits national and municipal strategy
2. **Economic**
3. **Commercial**
4. **Administrative**
5. **Financial**

Each study was written by hand. The strategic section alone draws on many sources, and preparing it took **about a week** (estimated).

## What We're Building

A web platform that walks the engineer through each section and produces the study document.

### Strategic section — approved
- The engineer picks from **drop-down lists** instead of writing from scratch.
- The lists are **linked to each other**: every choice narrows down the next list to the options that fit, using a mapping between strategy levels.
- The platform turns the choices into the written section and exports it to **Word**, with tables that match the on-screen preview.
- No limit on how many strategy links a project has; older studies are converted automatically, and duplicates can be merged with one click.

### Economic section (roads, bridges and tunnels) — under review
The most complex section, because the right analysis depends on the type of project. Instead of one long form, the platform asks a **sequence of questions**:

1. What type of project is it?
2. Is it new, an expansion, or currently closed?
3. Is a traffic count available?

The answers decide which **input template** appears, with just the fields that scenario needs:
- A road with no traffic count needs **5 required fields**.
- A closed bridge with two traffic movements needs **18 required fields** (33 with optional ones).
- With no traffic count, roads are estimated per resident, and bridges and tunnels from existing vs. target capacity.

**Built on the official standard.** The calculations follow the **Saudi Highway Code (SBC 203)**: its discount rate, 30-year analysis period, value of travel time, and its formulas for travel time and fuel. Any input without a source is labelled **"needs confirmation"**, so assumptions are never hidden.

**Tested on a real project.** On a real municipal bridge project, the time and fuel benefits matched the department's own study, and the platform added the investment-return figures (net present value, rate of return, payback period).

### Next
Gap calculators for municipal services — parks, flood drainage, public toilets, pedestrian bridges and municipal buildings — measuring what exists against per-resident standards or targets.

## Results So Far

| | Before | With the platform |
|---|---|---|
| Strategic section | ~1 week (estimated) | **Under 1 day** for an engineer who knows the project |
| Quality | Written by hand | Approved by the engineers, who rated the output **excellent** |

## What I'm Learning

- **Guide people instead of giving them a blank page.** Linked lists that narrow each choice turn a week of research into a series of decisions.
- **Handle complexity with questions, not bigger forms.** A few questions up front decide which inputs matter, so engineers only fill in what their scenario needs.
- **Follow the official standard and label every assumption.** Engineers trust numbers they can trace back to a code page or a source.
- **Get each section approved before building the next.** The engineers' review of the strategic section shaped how the economic section was designed.
