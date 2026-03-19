# Scenario 4 — Data & Analytics

## "The Dashboard Nobody Trusts"

Somewhere in the business there are 40 dashboards across three BI tools. Executives make decisions by gut because the numbers never match. One metric, the one everyone says is *the* metric, is calculated four different ways depending on who you ask. A new VP wants one number, one definition, defended in a room full of people who each think their version is right.

**You pick the domain, the metric, the stack, and how deep into data science you want to go.** The only rule: the disagreement has to be *plausible*. Pick a metric where reasonable people could genuinely calculate it differently.

---

## Pick Your Domain (or invent your own)

| Domain | The contested metric | Why nobody agrees |
|---|---|---|
| **Manufacturing** | OEE (Overall Equipment Effectiveness) | Does planned maintenance count as downtime? Startup scrap? |
| **SaaS / subscription** | Churn | Logo vs. revenue churn. Does a downgrade count? When does the clock start? |
| **E-commerce / retail** | Customer Lifetime Value | Which margin? Which discount rate? Cohort vs. predictive? |
| **Logistics / delivery** | On-Time Delivery | Promised date vs. revised date. Partial shipments. Whose clock? |
| **Fintech / lending** | Default rate | 30/60/90 days past due? Principal only? After recoveries? |
| **Healthcare ops** | Bed utilization | Midnight census vs. hourly. Does observation count? |
| **Ad tech / media** | Attribution / conversion | Last-touch vs. multi-touch. Which lookback window? |

---

## Challenges

Go dashboard-heavy, go model-heavy, or split the room. Nobody finishes all ten.

**1 — The Room.** *(PM)* Interview three stakeholders. Role-play it with Claude. They want different things and they're all partially right. Write the requirements doc that threads the needle.

**2 — The Mess.** *(Data Eng)* Generate plausible raw data for your domain. Include realistic noise: gaps, mislabeled categories, that one source system reporting in the wrong timezone. The ugliness is the point.

**3 — The Definition.** *(Architect)* Define the metric once. Document every assumption, every edge case, every "what counts." This is your semantic layer's first citizen, the thing everything else inherits from.

**4 — The Engine.** *(Dev)* Build the metric calculation. As code, with an API. Not a SQL view buried in a BI tool. Testable, versioned, explainable.

**5 — The One.** *(Dev)* One dashboard that replaces the 40. Wireframe first. Then a working prototype. Drill-down from top-level to the thing an operator actually fixes.

**6 — The Reconciliation.** *(Tester)* Your number vs. the four existing calculations. Where do they diverge and *why*? This is the artifact that wins the room.

**7 — The Watchdog.** *(Data Sci)* Anomaly detection on the metric. When it moves in a way that's statistically weird, flag it before someone asks. Choose your weapon: simple control charts to full forecasting model.

**8 — The Diplomacy.** *(PM)* Change management plan. How do you retire 40 dashboards without a revolt? Migration path, sunset dates, who to convince first.

**9 — The Simulator.** *(Stretch)* What-if engine. Change an input, see the metric move. Interactive. The thing the VP plays with in the meeting.

**10 — The Question.** *(Stretch)* Natural-language query over your semantic layer. "Why was Tuesday worse than Monday?" Get a real answer, not a chart dump.

---

## OPTIONAL — Start From Data, Not From Zero

Don't want to generate the mess yourself? Pick one:

- **Sentinel KYC** ([github.com/beck-source/sentinel-kyc](https://github.com/beck-source/sentinel-kyc)): auditing & reporting on Know-Your-Customer data. *Requires an API key.* Good fit for fintech/compliance metrics.
- **AdventureWorks for Postgres** ([github.com/lorint/AdventureWorks-for-Postgres](https://github.com/lorint/AdventureWorks-for-Postgres)): the classic sales/inventory sample DB. Good fit for retail, logistics, or revenue metrics.

**If you use one:** Skip the *generation* part of Challenge 2, but not the *inspection* part. Go find the noise that's already in there. Challenge 3 still needs you to pick which metric is contested.

---

> **Hint:** Challenge 6 is the one the VP actually cares about. Don't skip it to make the dashboard prettier.
