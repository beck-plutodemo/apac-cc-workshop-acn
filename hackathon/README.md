# Mini-Hackathon — APAC Claude Code Workshop

Welcome to the Mini-Hackathon session! This document covers the hackathon brief and submission instructions. See the [root README](../README.md) for the full workshop agenda.

---

## Mini-Hackathon Brief

**Duration:** 60 minutes (14:45 – 15:15 SGT / 17:45 – 18:15 AEDT)

**Objective:** Use Claude Code to build a meaningful improvement or new feature on top of the [inventory-management](https://github.com/beck-source/inventory-management) starter app (or your own project, if agreed with your facilitator).

**Teams:** You will be assigned to a team at the start of the session. Teams are typically 2–4 participants.

**Challenge:** Your team must use Claude Code to:

1. Identify a problem or opportunity in the starter app
2. Implement a solution using Claude Code as your primary coding assistant
3. Document what you built and how Claude Code helped

**Judging Criteria:** To be communicated in person by your facilitator.

---

## Submission Instructions

Each team must submit their work by **uploading a folder** to `hackathon/submissions/` in this repository.

### Folder Naming Convention

```
submissions/
└── teamN_hackathon-name/
```

Replace `N` with your team number and `hackathon-name` with a short slug describing your submission.

**Examples:**

```
team1_smart-reorder
team2_claude-inventory-audit
team3_low-stock-alerts
```

### Required Files

Every submission folder **must** contain exactly these three files:

```
teamN_hackathon-name/
├── README.md          # Project overview and demo notes
├── CLAUDE.md          # Claude Code context for your project
└── submission.html    # Presentation slide (HTML format)
```

---

### `README.md` — What to Include

Your `README.md` should cover:

```markdown
# Team N — [Hackathon Name]

## Team Members

- Name, Role

## Problem Statement

What problem did you tackle and why?

## Solution Overview

What did you build? How does it work?

## How We Used Claude Code

Describe the specific Claude Code features and commands you used.

## Demo

Link to a short demo video or screenshots (optional but encouraged).

## Lessons Learned

What worked well? What would you do differently?
```

---

### `CLAUDE.md` — What to Include

Your `CLAUDE.md` gives Claude Code context about your submission project. Use it to describe:

- The purpose of your project
- Key files and their roles
- Any conventions or patterns Claude should follow
- Commands to build/run/test the project

You can generate a starter `CLAUDE.md` by running `/init` in your project directory with Claude Code.

---

### `submission.html` — Presentation Slide

Your `submission.html` is a **single self-contained HTML file** that acts as a presentation slide. It will be displayed during the judging session.

**Requirements:**

- Single HTML file (inline all CSS and JS — no external dependencies)
- Renders correctly when opened directly in a browser
- Covers: team name, problem, solution, key Claude Code moments, outcome
- Keep it visual — use a clear layout, not a wall of text

**Minimal template to get started:**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Team N — Hackathon Submission</title>
    <style>
      body {
        font-family: sans-serif;
        background: #0f0f0f;
        color: #f0f0f0;
        margin: 0;
        padding: 2rem;
      }
      h1 {
        color: #e8912d;
      }
      h2 {
        color: #a78bfa;
        margin-top: 2rem;
      }
      ul {
        line-height: 1.8;
      }
      .tag {
        background: #1e1e2e;
        border: 1px solid #a78bfa;
        border-radius: 4px;
        padding: 2px 8px;
        font-size: 0.85rem;
        margin-right: 4px;
      }
    </style>
  </head>
  <body>
    <h1>Team N — Your Hackathon Name</h1>
    <p><strong>Team Members:</strong> Name 1, Name 2</p>

    <h2>Problem</h2>
    <p>Describe the problem you solved.</p>

    <h2>Solution</h2>
    <p>Describe what you built.</p>

    <h2>How We Used Claude Code</h2>
    <ul>
      <li>Used <code>/init</code> to scaffold the project</li>
      <li>Used Claude Code to generate unit tests</li>
      <li>...</li>
    </ul>

    <h2>Outcome</h2>
    <p>What was the result? What would you do next?</p>
  </body>
</html>
```

---

## Submitting via GitHub

1. Fork or clone this repository
2. Create your folder under `hackathon/submissions/teamN_your-name/`
3. Add your three files (`README.md`, `CLAUDE.md`, `submission.html`)
4. Open a Pull Request to this repository with the title: `Submission: Team N — Your Hackathon Name`
5. A facilitator will merge your PR before judging begins

> **Deadline:** All PRs must be open before the judging session starts at **15:15 SGT**.

---

## Questions?

Speak to your facilitator or raise a hand during the session. Good luck!
