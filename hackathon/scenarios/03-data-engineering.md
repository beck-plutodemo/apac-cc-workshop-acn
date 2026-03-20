# Scenario 3 — Data Engineering

## "The Swamp"

**Fabrikam Retail** has seven source systems. POS, e-commerce, loyalty, CRM, and three others acquired in mergers. None of them agree on what a "customer" is. Same person, four IDs, two spellings. The analytics team gave up and builds everything from CSV exports. The new CDO wants a single source of truth. She said 90 days.

**You pick the architecture, the stack, the way (lakehouse, warehouse, mesh — your choice).**

---

## Challenges

**1 — The Mess.** _(Data Eng)_ Generate realistic sample data from four of the seven sources. Different schemas. Conflicting keys. At least one encoding problem. Duplicates that aren't obvious. Use Claude Code for this. Give it instructions for making “bad” data (HINT: use the instructions here) and let it cook\!

**2 — The Blueprint.** _(Architect)_ Design the target. Layers, zones, whatever your pattern calls them. Where does raw live, where does truth live, who's allowed to read what.

**3 — The Intake.** _(Data Eng)_ Build ingestion for three sources. One batch file, one change-data-capture stream, one flaky REST API. All land in your raw layer.

**4 — The Customer.** _(Data Eng)_ Master the customer entity. Match records across sources. Survivorship rules. Golden record. Show your confidence score.

**5 — The Tripwire.** _(Dev)_ Data quality framework. Schema drift, null explosions, volume anomalies. What breaks the pipeline vs. what just alerts?

**6 — The Contract.** _(Tester)_ Data contracts for two downstream consumers. Producers can't break them silently. Tests that enforce it.

**7 — The Catalog.** _(PM)_ Catalog entries for your core entities. Written for an analyst, not an engineer. What is this, where did it come from, can I trust it.

**8 — The Clock.** _(Infra)_ Orchestration. Dependencies, retries, SLAs. When the 2am run fails, who gets paged and what do they see?

**9 — The Trace.** _(Stretch)_ Lineage. One bad value in a report — trace it back to the source row. Programmatically.

**10 — The Backfill.** _(Stretch)_ Five years of history needs to go through your new pipeline. Without melting it. What's the strategy?

---

**Hint:** Challenge 4 is where teams spend too long. Timebox the matching logic — "good enough" survivorship beats perfect matching you never finish.
