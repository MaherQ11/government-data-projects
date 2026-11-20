# Case Study: Matching Two Project Lists That Don't Agree

**Organization:** Holy Makkah Municipality, Project Management Office (PMO)
**Role:** Data Analyst Trainee — built with a teammate
**Tools:** Python, pandas, Streamlit (Arabic interface), Excel · built with AI-assisted coding (Claude Code)
**Scale:** ~930 projects in the five-year portfolio × ~540 projects (109 columns) in the PMO file

> The data is internal. The tool was developed and tested on synthetic files with the same structure; the real files never left the municipality's computer.

---

## The Problem

The municipality keeps two lists of the same projects:
- the **five-year project portfolio**, and
- the **PMO projects file**, with contract, contractor and cost details.

To report on running projects, each portfolio project has to be found in the PMO file. Doing this by hand was slow and error-prone because the two files rarely write a project the same way:

- PMO names start with the contract number (`42-Opening mountain roads...`) and are **cut off at 100 characters**.
- Hidden spaces and line breaks inside names.
- The same word written differently (Arabic letter variants such as ا/أ/إ, ي/ى, ه/ة) and spelling mistakes.
- **Contract numbers repeat** across different projects, so they can't be used alone.
- **Same name, different project:** yearly renewal contracts, or the same work in different locations (north vs south, different districts).

## What We Built

A Python tool with an Arabic Streamlit interface, in two parts.

### 1. Matching
For each **running** project in the portfolio, find it in the PMO file and copy its PMO row next to it.

1. **Clean the names:** remove hidden characters, strip the contract-number prefix, unify Arabic letter variants, remove spaces.
2. **Search in order of confidence:** exact match → one name contains the other (handles cut-off names) → contract number confirmed by another field → 80%+ similar name **with matching cost**.
3. **Break ties** between candidates by name, then cost, then date. A matching cost beats a slightly closer name.
4. **Never guess:** every result gets a label — *confirmed (name + cost)*, *confirmed (name + date)*, *name only*, **needs review**, or *not found*. Unclear cases go to a person.

### 2. Duplicate check
Finds rows inside the PMO file that might be the same project, checked in 5 steps: **name → contractor → contract number → cost → date**.
- A location rule: names that differ in direction, district, unit, contract or phase are **different projects**.
- Only rows that pass **all 5 steps** count as confirmed duplicates.
- **Nothing is deleted** — rows are only marked and hidden with an Excel filter.

## Results

Tested against the team's manual matching on **118 running projects**:

| | Count |
|---|---|
| Projects the tool confirmed | **67** |
| Projects the team matched by hand | 61 |
| Agreement between tool and team | 60 of 61 |
| The one disagreement | The tool was right (name, cost and date matched to the day) |
| **Matches the team had missed** | **6** |

The duplicate check found **26 groups** of similar-looking projects — mostly yearly renewal contracts — and **0 confirmed duplicates**. Instead of merging records that looked alike, the tool showed the PMO file was clean.

## What I Learned

- **Messy text needs rules, not just fuzzy matching.** Most of the accuracy came from cleaning names and using cost and dates as confirmation.
- **A tool should say "I'm not sure."** Labelling unclear cases for review is what made the team trust the results.
- **Check the tool against people.** Comparing against the manual work showed both where the tool was right and where people had missed matches.
- **Sensitive data can stay protected:** building and testing on synthetic files with the same structure meant the real data never had to be shared.
