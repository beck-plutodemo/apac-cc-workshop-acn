# Scenario 5 — Agentic Solution

## "The Intake"

Somewhere in the business, inbound is drowning a human. Requests arrive through four different channels, get hand-triaged into a dozen internal teams, and the average time-to-first-response is measured in hours that nobody is proud of. Someone senior wants an agent. Someone in Legal wants to know what could possibly go wrong. Both are right.

**You pick the domain, the tools, the guardrails. Greenfield.** The only constraint: the agent has to make a *real decision* — classify something, route it somewhere, take an action — not just chat.

---

## Build on the Claude Agent SDK

This scenario is built on the **Claude Agent SDK** — the same agent harness that powers Claude Code, available in Python and TypeScript. It gives you the agent loop, tool calling, subagents, permissions, and session management out of the box, so your three hours go into *your* agent instead of plumbing.

**Start here before you write a line:**

- **Overview** — [docs.claude.com/en/api/agent-sdk/overview](https://docs.claude.com/en/api/agent-sdk/overview)
- **Python reference** — [docs.claude.com/en/api/agent-sdk/python](https://docs.claude.com/en/api/agent-sdk/python)
- **TypeScript reference** — [docs.claude.com/en/api/agent-sdk/typescript](https://docs.claude.com/en/api/agent-sdk/typescript)
- **Custom tools** — [docs.claude.com/en/api/agent-sdk/custom-tools](https://docs.claude.com/en/api/agent-sdk/custom-tools)
- **Permissions & approvals** — [docs.claude.com/en/api/agent-sdk/permissions](https://docs.claude.com/en/api/agent-sdk/permissions)

Auth is an API key in `ANTHROPIC_API_KEY`. Read the overview first. Skim permissions before Challenge 5.

---

## Pick Your Intake (or invent your own)

| Domain | What's flooding in | What the agent decides |
|---|---|---|
| **Professional services** | Emails, Slack, web forms, one partner who still faxes | Which of 12 internal teams owns this |
| **IT helpdesk** | Tickets, chat, "urgent" emails to the CIO | P1 vs. P4, which queue, auto-resolve the password resets |
| **Insurance claims** | PDFs, photos, voicemail transcripts | Fast-track, investigate, or deny — and why |
| **Code review** | PRs across 30 repos | Auto-approve the trivials, flag the scary ones, assign a human |
| **Compliance / KYC** | Onboarding docs, sanctions-list hits | Clear, escalate, or request-more-info |
| **Sales lead routing** | Form fills, inbound email, conference badge scans | Which rep, which tier, is this even real |

---

## Challenges

Pick a lane or pair up. Nobody finishes all ten.

**1 — The Mandate.** *(PM)* Define the agent's job. What it decides alone. What it escalates. What it must never touch. One page. Legal reads this.

**2 — The Bones.** *(Architect)* Agent architecture. Tools, memory, state, guardrails. An ADR for how you're structuring it. A diagram someone can argue with.

**3 — The Triage.** *(Dev)* Build the core agent. Ingest a request, classify it, enrich it with context, route it. Log the reasoning — not just the answer.

**4 — The Hands.** *(Dev)* Give it tools. At minimum: a knowledge lookup, a system-of-record check, an action that writes somewhere. The agent decides when to use them. Build these as custom tools in the SDK.

**5 — The Brake.** *(Dev)* Human-in-the-loop. For which decisions? Confidence threshold, category, or something smarter? Build the approval surface using the SDK's permission hooks. Make it fast to approve, easy to override.

**6 — The Attack.** *(Tester)* Adversarial eval set. Prompt injection in the request body. Ambiguous asks. Things that look urgent but aren't. Try to make it misroute, leak, or escalate wrong.

**7 — The Scorecard.** *(Tester)* Golden dataset — 30+ labeled requests. Eval harness. Accuracy, precision per category, escalation rate. A number you can defend.

**8 — The Glass.** *(Infra)* Observability. Every decision traceable. Why did it route this request here? Searchable. Replayable.

**9 — The Colleague.** *(Stretch)* A second, specialist agent. Triage agent hands off, specialist does deeper work, hands back. Use the SDK's subagent primitive.

**10 — The Loop.** *(Stretch)* Feedback mechanism. When a human overrides the agent, that signal goes somewhere useful. Close the loop.

---

> **Hint:** Challenge 6 is where you earn the room. Challenge 1 is where you earn Legal's trust. Don't skip to Challenge 3.
