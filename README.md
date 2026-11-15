# Actuarial Safety Reporting System (ASRS)

An industry-wide system for collecting and sharing anonymous lessons from actuarial reporting.

**[Browse the reports](actuarial_safety_reporting_system.csv)** · **[Submit a report](#how-to-submit-a-report)**

## What is ASRS?

ASRS is an open register of mistakes and near misses that practitioners run into during the reporting cycle, whether for Solvency II, IFRS 17, statutory accounts or pension schemes.

Each report explains what went wrong, how to notice it and how to prevent it, and is tagged by category and reporting framework so you can find the lessons that apply to you. Reports are anonymous and focus on causes in the process, data, assumptions and systems, not on who made the mistake.

## Why?

ASRS is inspired by the [Aviation Safety Reporting System](https://asrs.arc.nasa.gov/), which NASA has run since 1976. Pilots, air traffic controllers, cabin crew and mechanics report incidents and near misses voluntarily and confidentially. The reports are de-identified and the lessons are shared across the industry, so a mistake that one crew made, or nearly made, does not have to be repeated by another.

Actuarial reporting has hidden hazards of its own: an input file left over from last quarter, an outdated assumption, a broken spreadsheet link, a step skipped under deadline pressure. Most of these errors are caught and quietly fixed, and the lesson never leaves the team. ASRS collects them in one place, so that companies can find and mitigate these pitfalls without having to experience the error first-hand.

## How it works

1. You submit a report by email or through GitHub.
2. We review it, remove anything that could identify a person, company or client, and add it to the register.
3. Anyone can browse, search and download the register.

## How to submit a report

Near misses count. An error caught before sign-off teaches the same lesson as one that reached the regulator, and it is much easier to share.

### By email (anonymous)

Send your report to [gregor@osmodelling.com](mailto:gregor@osmodelling.com?subject=ASRS%20report) using the [template](#report-template) below. We may reply to clarify details. We then anonymise the report, add it to the register and delete your email. Your name, email address and employer are never published or shared.

### Through GitHub (public)

Fill in the [report form](https://github.com/open-source-modelling/actuarial_safety_reporting_system/issues/new?template=report.yml). It asks the same questions as the [template](#report-template) below.

> [!WARNING]
> GitHub issues are public as soon as you submit them, and they show your GitHub username. Anonymise your report before posting it, or use email instead.

### Report template

Answer what you can; a short report is better than none. If you are unsure of the [category](#categories), leave it blank and we will choose one.

```text
Title:
[One line, e.g. "Model silently used last quarter's yield curve"]

Category:
[Data / Assumptions / Model / Systems / Process / Reporting / Communication / Other]

Reporting framework:
[e.g. Solvency II, IFRS 17, US GAAP, IAS 19, local statutory]

What happened?
[Context: line of business, step in the process. What went wrong, and why?]

How could someone notice it?
[The check, reconciliation or warning sign that revealed the error, or would have.]

How can it be prevented?
[The control or process change that would stop it from happening again.]
```

### What not to include

Keep your report general enough that nobody can tell who you are or where it happened. Please leave out:

- names of people, employers, clients or other companies
- absolute amounts; use relative terms instead, such as "technical provisions were overstated by about 5%"
- personal data about policyholders, scheme members or colleagues
- combinations of details that could identify your employer, such as a niche product in a small market
- anything you are not allowed to share under your employment contract, a confidentiality agreement or professional rules

By submitting a report, you agree that it may be edited, anonymised and published in this repository under its [licence](LICENSE).

## The register

For this first version, all reports are stored in a single CSV file: [`actuarial_safety_reporting_system.csv`](actuarial_safety_reporting_system.csv). GitHub displays it as a searchable table, and you can download it for Excel, R or Python.

| Column | Contents |
| --- | --- |
| `ID` | Sequential number, assigned when the report is added |
| `title` | One-line summary |
| `category` | Main type of error, from the [categories](#categories) below |
| `framework` | Reporting framework(s), e.g. `Solvency II; IFRS 17`, or `General` |
| `description_of_error` | What happened and why, with enough context to understand it |
| `how_to_notice` | The check, reconciliation or warning sign that reveals the error |
| `how_to_prevent_it` | The control or process change that prevents it |
| `timestamp` | Date the report was added to the register (YYYY-MM-DD) |

### Categories

Each report gets the one category that best describes where the error came from.

| Category | Use it for |
| --- | --- |
| Data | Incorrect, incomplete or misinterpreted input data |
| Assumptions | Outdated, inappropriate or misapplied assumptions, including economic inputs such as yield curves |
| Model | Errors in model logic, code, formulas or configuration |
| Systems | Software, IT infrastructure and interfaces, e.g. broken spreadsheet links, failed jobs or overwritten files |
| Process | Missed, repeated or out-of-order steps, and manual workarounds |
| Reporting | Errors when moving results into reports, templates or disclosures, e.g. wrong units, sign conventions or template mapping |
| Communication | Misunderstood requirements, handovers or regulatory interpretation |
| Other | Anything that does not fit the categories above |

### Example

An illustrative report (not a real one):

- **title:** Model silently used last quarter's yield curve
- **category:** Assumptions
- **framework:** Solvency II
- **description_of_error:** Quarterly valuation of life business. The cash-flow model read the risk-free rate curve from a fixed file path. The new quarter's curve was saved under a different file name, so the model silently used the previous quarter's curve.
- **how_to_notice:** The analysis of change shows a much smaller economic variance than the movement in interest rates would suggest. Comparing a few spot rates in the model with the published EIOPA curve confirms it.
- **how_to_prevent_it:** Have the model check each input's reference date against the valuation date and stop on a mismatch. Show the curve's reference date in the run log and on the sign-off checklist.

### Using the data

To load the register in Python:

```python
import pandas as pd

url = (
    "https://raw.githubusercontent.com/open-source-modelling/"
    "actuarial_safety_reporting_system/main/actuarial_safety_reporting_system.csv"
)
reports = pd.read_csv(url, encoding="utf-8-sig")
```

If Excel puts everything in one column (common with European regional settings), import the file with **Data › From Text/CSV** instead of opening it directly.

## How long will ASRS run?

The repository will stay live and keep accepting reports for at least one year, until at least November 2027. The more practitioners contribute, the more useful it becomes for everyone, so please submit a report and share ASRS with your colleagues.

## Disclaimer

Reports are voluntary, personal accounts and are not verified. They are shared for learning, not as professional advice; consider whether a lesson applies to your own situation. Submitting a report here does not replace your internal incident process or any obligation to report an error to your regulator, auditor or professional body.

## Contact

Questions or ideas? Email [gregor@osmodelling.com](mailto:gregor@osmodelling.com) or [open an issue](https://github.com/open-source-modelling/actuarial_safety_reporting_system/issues).

ASRS is maintained by [Open-Source Modelling](https://github.com/open-source-modelling). See [LICENSE](LICENSE) for the licence terms.
