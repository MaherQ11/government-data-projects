# Case Study: Rebuilding a Municipal Project Portfolio Dashboard

**Organization:** Holy Makkah Municipality, Project Management Office (PMO)
**Role:** Data Analyst Trainee, in a team of three under the Director of Business Development
**Tools:** Excel, Power BI, SharePoint
**Scale:** ~1,000 projects
**Status:** Dashboard live; data cleaning still in progress

> All data in this project is internal. This page describes the problem, the approach and the results only; no project names, budgets or personal data are shown.

---

## The Problem

The PMO tracked all municipal projects on **PMWeb**, a project management platform. Its license had expired and it no longer had technical support, which caused three problems:

1. **Project status was out of date.** Projects that had been closed were not updated on time, so the platform still showed them as running.
2. **The Power BI reports were wrong.** They read from the same out-of-date data, so management was making decisions from incorrect numbers.
3. **Two sources disagreed.** The project data file did not match the municipality's **five-year project portfolio**, so there was no single trusted list of projects.

## What I Did

**1. Moved the data off PMWeb into Microsoft tools**
Exported the full project dataset from PMWeb and rebuilt the workflow on Excel and SharePoint, with Power BI on top — tools the municipality already licenses and supports.

**2. Cleaned and standardized ~1,000 project records**
- Identified which projects were actually **running, under construction or closed**.
- Standardized project names, statuses and dates so the same thing is always written the same way.
- Reconciled the project file against the five-year portfolio so both sources agree.

**3. Built a new Power BI dashboard**
- Current projects and projects under construction
- Contract notifications
- The responsible department for each project
- A filter by project year

## The Hardest Part: Near-Duplicate Projects

Many projects had **very similar names** — the same district, the same type of work, slightly different wording. They looked like duplicates, but on closer review many turned out to be **different projects**. Merging them would have deleted real projects; leaving true duplicates would have double-counted them.

**Our approach:** A teammate and I built a tool that checks every similar pair in 5 steps (name, contractor, contract number, cost, date) and only calls it a duplicate if all 5 match. Unclear cases go to the **engineers responsible for those projects**, who know the details and make the final call.

**Result:** 26 groups of similar-looking projects — mostly yearly renewal contracts — and **0 real duplicates**. Merging by name alone would have deleted real projects.

Full details: [Project Matching Tool](project-matching-tool.md)

## Results

- One **trusted project list** that matches the five-year portfolio.
- A dashboard management can rely on, built on tools with ongoing support instead of an unsupported platform.
- The dashboard is now used by the **entire PMO department** through SharePoint.
- Data preparation was the largest part of the work and is still ongoing as more records are reviewed with the engineers.

## What I Learned

- A dashboard is only as good as the data under it: the old reports looked fine but were wrong.
- For similar-looking records, a tool can find the candidates, but the final decision belongs to the people who know the projects.
- Moving to tools the organization already supports makes the work last after the project ends.
