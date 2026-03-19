# Scenario 1 — Code Modernization

## "The Monolith"

Northwind Logistics runs on something old. It works — mostly — but the people who built it are gone, the docs are a folder of outdated Word files, and the board just approved "modernization" without defining what that means.

You have **3 hours** to prove modernization is possible without a big-bang rewrite.

You pick the language, the era, the architecture, the decomposition strategy. The only rule: generate something ugly enough that fixing it is interesting.

---

## Pick Your Legacy (or invent your own)

| Flavor | What Claude generates for you |
|---|---|
| **PHP 5 monolith** | `index.php`, SQL strings concatenated inline, sessions in globals |
| **Enterprise Java 2010** | Spring XML config, `AbstractSingletonProxyFactoryBean`, WAR on WebLogic |
| **Stored-proc architecture** | 40 T-SQL procs that *are* the business logic, app is a thin shell |
| **Early Node callback hell** | Express 3, callbacks 6 deep, logic in Mongoose pre-save hooks |
| **Rails 2 majestic monolith** | Fat models, `lib/` doing unspeakable things, cron + rake jobs |
| **Classic ASP / VB6** | COM components, ADO recordsets, inline VBScript |
| **SOAP service tangle** | WSDL files, an ESB that's actually just a queue |
| **COBOL + batch** | Fixed-width files, JCL, nightly batch that can't be interrupted |

**Modernize toward:** Strangler fig • Containerize-and-ship • Event-driven • API façade • Serverless extraction • DB-first split. Your call.

---

## Challenges

Pick a lane or pair up. Nobody finishes all ten — that's the point.

**1 — The Stories.** *(PM)* Write user stories for the three most important business capabilities in this system. You decide what they are. Acceptance criteria that a tester could actually execute.

**2 — The Patient.** *(Architect)* Generate the legacy monolith. 4–6 modules, shared database, at least two circular dependencies, one God class. Make it realistic — including the parts that make you wince.

**3 — The Map.** *(Architect)* Produce a decomposition plan. Strangler fig, branch-by-abstraction, your call. Name the seams. Rank the services by extraction risk.

**4 — The Pin.** *(Tester)* Write characterization tests against the monolith before anyone touches it. You're not testing correctness — you're pinning behavior.

**5 — The Cut.** *(Dev)* Extract your first service. Clean API contract. The monolith still works. Prove both.

**6 — The Fence.** *(Dev)* Build an anti-corruption layer between old and new. The monolith's data model should not leak into your new service.

**7 — The Contract.** *(Tester)* Contract tests between the monolith and the new service. Both sides. If one changes, the other screams.

**8 — The Pipeline.** *(Infra)* CI/CD that builds and deploys both monolith and service. Independently. One failing doesn't block the other.

**9 — The Second Cut.** *(Stretch)* Extract a second service. This one talks to the first via events, not HTTP. Handle the dual-write problem.

**10 — The Weekend.** *(Stretch)* Write the cutover runbook. Steps, rollback triggers, the 3am decision tree. The one ops will actually follow.

---

## OPTIONAL — Bring Your Own Monolith

Don't want to spend time generating the legacy? We've got one lying around.

**[https://github.com/rishikeshradhakrishnan/spring-music](https://github.com/rishikeshradhakrishnan/spring-music)**

Spring Music is a Spring Boot sample app built for Cloud Foundry. It stores the same domain objects across relational, document, and key-value stores using bean profiles and Spring Cloud Connectors. It was never meant to be realistic — it was meant to demo persistence options. Which is exactly why it's a perfect stand-in for *"someone built this to prove a point and then it accidentally became production."*

**If you use it:**
- **Skip Challenge 2** (The Patient) — you already have one.
- **Challenge 1** still applies — reverse-engineer the business capabilities from what's in the repo.
- Everything from **Challenge 3 onward** works as-is. The seams are there. Find them.

---

> **Hint:** Your `CLAUDE.md` should know what "done" means for this codebase before Challenge 5.
