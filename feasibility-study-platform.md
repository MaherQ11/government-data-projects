# Case Study: A Guided Platform for Municipal Feasibility Studies

**Organization:** Holy Makkah Municipality
**Role:** Data Analyst Trainee — one of three trainees building the platform, supervised by three engineers
**Tools:** Cloudflare Workers, Cloudflare KV, Claude API, PowerPoint / PDF export
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
- The platform turns the choices into the written section and exports it to **PowerPoint or PDF**.

### Economic section — under review
The most complex section, because the right analysis depends on the type of project. Instead of one long form:
- The platform asks a **sequence of questions** about the project.
- The answers lead to the right **scenario**, and each scenario gets its own **input template** with just the fields it needs.
- All scenarios have been built and are waiting for the engineers' approval.

## Results So Far

| | Before | With the platform |
|---|---|---|
| Strategic section | ~1 week (estimated) | **Under 1 day** for an engineer who knows the project |
| Quality | Written by hand | Approved by the engineers, who rated the output **excellent** |

## What I'm Learning

- **Guide people instead of giving them a blank page.** Linked lists that narrow each choice turn a week of research into a series of decisions.
- **Handle complexity with questions, not bigger forms.** A few questions up front decide which inputs matter, so engineers only fill in what their scenario needs.
- **Get each section approved before building the next.** The engineers' review of the strategic section shaped how the economic section was designed.
