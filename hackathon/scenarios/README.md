# Claude Code Hackathon: Afternoon Session

## The Setup

You have **3 hours**, a team, and Claude Code. Pick one scenario. Get as far as you can.

Each scenario has 10 challenges. You won't finish all of them. That's by design. **Depth beats breadth.** Organize your team around the challenges you pick and work in parallel as much as possible (use Claude to help with that too). Be wise about which challenges you select. There are hints.

---

## The Rules

1. **Tech stack is yours to choose.** One exception: Scenario 5 requires the **Claude Agent SDK**. Use Claude to help you learn it, or to migrate if you're coming from another framework.  
2. **You may need to build starter code / data / documents.** If the scenario says "a 12-year-old monolith exists," you generate it. That's part of the job. Some scenarios offer optional starter repos. Use them or don't. Part of the learning is watching Claude build something you can test against.  
3. **Play every role.** Your team needs a PM, architect, developer, tester, data engineer, and infra engineer whether you staffed for it or not. Claude Code doesn't care what your title is. The point is to see how Claude works across the SDLC, which means you may end up working in areas you normally don't.  
4. **Commit history is evidence.** We want to see the journey, not just the destination.  
5. **`CLAUDE.md` is your friend.** Teach it your conventions early.  
6. **Document your work.** Your repo must include a `README.md` (template below) explaining what you built and what you'd do next.  
7. **Build a presentation.** Use Claude Code to generate a **5-minute HTML presentation** you *could* deliver if you win the judging. It lives in your repo whether you present or not.  
8. **Claude will judge.** At the end, Claude evaluates submissions. A handful of teams present live.

---

## The Scenarios

| \# | Scenario | One-liner |
| :---- | :---- | :---- |
| 1 | **Code Modernization** | A monolith nobody understands. The board wants it "modernized." |
| 2 | **Cloud Migration** | On-prem to cloud. The CFO and CTO disagree on how. |
| 3 | **Data Engineering** | Seven systems. Zero agreement on what a "customer" is. |
| 4 | **Data Analytics** | 40 dashboards. One metric. Four different answers. |
| 5 | **Agentic Solution** (Claude Agent SDK) | 200 requests a day, triaged by hand. Build the agent. |

---

## The Judging

Claude does the judging. Top teams present live (5 minutes each).

**What definitely gets read:** your `README.md`, your `presentation.html`, and your `CLAUDE.md`. These are your pitch. Don't leave them to the last ten minutes. If Claude only sees those three files, it should still understand what you built, why it matters, how far you got, and how you taught the tool to work your way. We may go deeper into the repo, we may not. Assume those three carry the weight.

**What we're looking for** (final categories will be a surprise\!, but think along these lines):

- **Most production-ready.** Could hand it to an ops team Monday.  
- **Best architecture thinking.** ADRs, diagrams, decisions someone in two years will thank you for.  
- **Best testing.** Not coverage. Adversarial thinking, edge cases, evals.  
- **Best product work.** Stories that are actually stories. Docs that persuade.  
- **Most inventive Claude Code use.** Subagents, hooks, skills, something we didn't expect.  
- **Wildcards:** best CI/CD, best legacy archaeology, best "what if this goes wrong" thinking, furthest through the 10 with quality intact, team that questioned a scenario requirement and was *right*.

---

## Submission

Before time's up, your repo needs:

1. **`README.md`** tells the story. Use the template below.  
2. **`/decisions`** folder with ADRs and architecture notes.  
3. **Any Working code**, however far you got.  
4. **`CLAUDE.md`** so we can see how you taught it.  
5. **`presentation.html`**, your 5-minute deck built with Claude Code. Ready to present if called.

Push to a branch named `team-<name>` and drop the link in the shared channel.

---

## README Template

Copy this into your repo's `README.md` and fill it in as you go, not at the end.

```
# Team <name>

## Participants
- Name (role(s) played today)
- Name (role(s) played today)
- Name (role(s) played today)

## Scenario
Scenario <#>: <title>

## What We Built
2-3 paragraphs. What exists in this repo that didn't exist 3 hours ago.
What runs, what's scaffolding, what's faked.

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
```

---

**Pick a scenario. Start building.**  
