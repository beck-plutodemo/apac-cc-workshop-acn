# Scenario 2 — Cloud Migration

## "The Lift, the Shift, and no Regrets"

Contoso Financial runs three workloads on-prem: a customer-facing web app, a nightly batch reconciliation job, and a reporting database that five teams query directly. The CFO signed the cloud contract. The CTO wants "cloud-native, not lift-and-shift." They are not aligned. The clock is running.

You pick the target cloud and migration pattern. You won't deploy to live cloud today — you'll produce **cloud-ready artifacts that run locally** with production-equivalent architecture. That's how real migration teams validate before committing.

**Your local environment is your cloud:** Docker Compose with services mapped to cloud primitives. A MinIO container is your S3. A Postgres container is your RDS. A Redis container is your ElastiCache. Name things accordingly.

---

## Challenges

**1 — The Memo.** _(PM)_ Write the decision memo. Lift-and-shift first then optimize? Or refactor on the way in? Pick a side. Make the case. Name the risks you're accepting. One page. No hedging.

**2 — The Discovery.** _(Architect)_ Generate the current state. Three workloads, their configs, their ugly dependencies on each other. Include the thing nobody documented — a hardcoded IP, a shared filesystem mount, a batch job that writes directly to the reporting DB schema. Make it real.

**3 — The Options.** _(Architect)_ Three target architectures on your chosen cloud. Scored on cost, risk, speed, and operability. One recommendation. One page. Reference actual services by name (ECS vs. EKS vs. App Service — your call).

**4 — The Container.** _(Dev)_ Containerize the web app. Write the Dockerfile. It runs locally via `docker compose up`. The same image, no changes, would run on ECS/Cloud Run/AKS. Prove it: document the exact `docker push` \+ service config that would deploy it. Bonus: multi-stage build, non-root user, health check endpoint.

**5 — The Rewire.** _(Data Eng)_ Migrate the batch reconciliation job — but kill the 2am cron. Redesign it as event-driven: triggers on file arrival in object storage (MinIO locally, S3/GCS in prod). Containerize it. Don't break downstream consumers; write a compatibility shim if you have to.

**6 — The Foundation.** _(Infra)_ Infrastructure-as-code for everything. Write Terraform (or Pulumi/CDK — your call) that provisions the full target architecture from an empty account. Networking, compute, managed data services. It won't run today — it needs to _read right_. Idempotent. No hardcoded secrets.

**7 — The Proof.** _(Tester)_ Pre-migration validation suite. What must be true before cutover? Write it as executable tests against the local Docker environment — these same tests run post-cutover in cloud. Smoke tests, contract tests, data integrity checks. The definition of "migration succeeded."

**8 — The Bill.** _(Architect)_ Cost model. Current on-prem vs. target cloud. 12-month projection with assumptions stated. Use the cloud provider's public pricing. Prove you didn't just move the invoice — show the optimization path to year-2 costs.

**9 — The Disaster.** _(Stretch)_ DR plan for the containerized architecture. Multi-region or warm standby — your call. Write actual failover runbook steps, not just a diagram. What breaks first? What's the RTO/RPO you're promising?

**10 — The Undo.** _(Stretch)_ The rollback plan. For each workload, at each migration stage. The one nobody wants to write but everyone needs at 4am. Assume something went wrong mid-cutover. What's the exact sequence?

---

**Hint:** Challenge 2 is a trap if you make it too clean. Real discovery finds things that complicate Challenge 3\. And the thing nobody documented in Challenge 2 should show up as a gap in Challenge 6's IaC if your team isn't talking to each other.
