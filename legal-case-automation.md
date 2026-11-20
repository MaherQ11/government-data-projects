# Case Study: Automating Court Case Entry for a Legal Department

**Organization:** Holy Makkah Municipality, Legal Affairs Department
**Role:** Data Analyst Trainee — designed and built the tool
**Tools:** JavaScript browser tool (Tampermonkey userscript), Excel case table
**Status:** Tested in simulation; a supervised two-week pilot on the live platform is the next step

> The case data is internal. This page describes the problem, the approach and the results only.

---

## The Problem

Each new court notification has to be registered on the **Unified Legal Platform** (a government platform). For every case, a staff member had to:

1. Open the case.
2. Pick values from **7 drop-down lists** — including the court circuit, chosen from a list of 299.
3. **Search an Excel table** to find which legal consultant owns the case.
4. Submit, close the confirmation window, and move to the next case.

This took **4–5 minutes per case** (the department's estimate). The last check found **57 new cases** waiting — about **4.3 hours** of repetitive work.

## What I Built

A tool that runs inside the browser on top of the platform and processes the case list from start to finish, **without changing the platform itself**:

1. Opens each case in order.
2. Reads the circuit name and **turns the Arabic text into a number** (e.g. "the fifty-second" → 52).
3. Fills the 7 fields.
4. Finds the consultant from the Excel case table.
5. Submits, closes the confirmation window, and moves to the next case — even if the page reloads after submitting.

## The Key Finding: Matching Cases to Consultants

The platform and the department's Excel table number cases differently, so a direct lookup failed. Looking at the data showed the pattern:

> **Platform case number = year + internal number** — e.g. `144825114` = `1448` + `25114`

The tool now builds the platform number from the table's "year" and "internal number" columns before comparing. Result:

- **6,763** internal case numbers indexed from the table.
- **542 of 544** cases for the year 1448 matched to their consultant.
- If a case isn't found, the tool uses the default consultant and **shows an alert with the number it searched for**, so nothing is assigned silently.

## Safety Controls

Automating a legal record means a mistake matters, so the tool is built to stop rather than guess:

- Won't submit if the circuit or court can't be set correctly.
- Checks that the open window is the same case that was selected.
- Stops if a case reappears in the list after being submitted.
- An instant **stop button**, and an option to **review each case before it is sent**.
- Tested against **9 simulated scenarios**.

## Results

| | Manual | With the tool (simulation) |
|---|---|---|
| Time per case | 4–5 minutes | **~30 seconds** |
| Time per 100 cases | ~7.5 hours | **~0.8 hours** (saves ~6.7 hours) |
| Consultant lookup | Manual search in Excel | Automatic — 542 of 544 matched |

During a run, the staff member's job becomes monitoring and handling alerts. The real time saved will be measured on the platform during the pilot.

## What I Learned

- **Look at the data before writing the lookup.** The year + number pattern was the difference between a lookup that failed and one that matched 99.6% of cases.
- **In sensitive workflows, stopping is better than guessing.** Every safety check is a place where the tool hands control back to a person.
- **Present the numbers honestly.** The 30-second figure comes from simulation, and the pilot is designed to measure the real one.
