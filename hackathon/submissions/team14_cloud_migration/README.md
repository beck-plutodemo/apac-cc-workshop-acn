# Team <name>

## Participants
- Christian, Joshua (role(s) played today)
- Liew, Justin Cheng Hon (role(s) played today)
- Patel, Rakesh (role(s) played today)
- Thanatanongkul, Siriwat (role(s) played today)
- Tarnwuttipong, Varunyou (role(s) played today)
- Savangvarorose, Kanyapak (role(s) played today)

## Scenario
Scenario <2>: Cloud Migration

## What We Built

We took Contoso Financial's three on-prem workloads — a customer-facing web app, a nightly batch reconciliation job, and a shared reporting database — and produced cloud-ready artifacts that run locally with production-equivalent architecture on AWS (ECS Fargate + RDS PostgreSQL + ElastiCache + S3).

The centrepiece is a Docker Compose stack where every local service maps directly to an AWS managed equivalent: MinIO → S3, Postgres → RDS, Redis → ElastiCache, Nginx → ALB. The same container image runs locally with `docker compose up` and deploys to ECS Fargate without code changes.

We killed the 2am cron job entirely. The batch reconciliation worker is now event-driven — it triggers on file arrival in object storage (MinIO locally, S3 in prod) via bucket notifications. A compatibility shim preserves the legacy output path and webhook so downstream consumers need zero changes. We also produced a decision memo resolving the CFO/CTO conflict, a discovery document surfacing four undocumented dependencies, a three-option architecture comparison (EC2 lift vs ECS Fargate vs EKS), Terraform IaC scaffolding, a pre-migration validation test suite, a 12-month cost model showing 80% Year-2 savings, a DR runbook (RTO 30 min / RPO 5 min), and a per-workload rollback plan.

## Challenges Attempted
| # | Challenge | Status | Notes |
|---|---|---|---|
| 1 | The <name> | done / partial / skipped | |
| 2 | | | |

## Key Decisions
Biggest calls you made and why. Link into `/decisions` for the full ADRs.

## How to Run It
Exact commands. Assume the reader has Docker and nothing else.

## If We Had Another Day
What you'd tackle next, in priority order. Be honest about what's held
together with tape.

## How We Used Claude Code
What worked. What surprised you. Where it saved the most time.