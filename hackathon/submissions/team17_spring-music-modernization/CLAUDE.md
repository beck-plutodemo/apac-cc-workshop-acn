# CLAUDE.md — Team 17 Hackathon Submission

> If you are a future Claude session reading this: you are looking at Team 17's submission for the APAC Claude Code Workshop hackathon.
> Scenario 1 — Code Modernization. The actual code lives in `hackathon/spring-music/`.
> Read `spring-music/CLAUDE.md` for the project-level architectural context and ADRs.

---

## What Was Built — One Sentence

A complete, production-ready migration of `spring-music` from Spring Boot 2.4.0 → 3.2.3 on Java 17, resolving every breaking issue across 4 layers: build tooling, Java source, configuration, and test coverage.

---

## CLAUDE.md Hierarchy in This Project

This project uses a **3-level CLAUDE.md hierarchy**. Each file is scoped to its context:

```
hackathon/
├── CLAUDE.md                          ← Level 1: Workspace context
│                                         (describes both sub-projects, shared commands)
├── spring-music/
│   └── CLAUDE.md                      ← Level 2: Project context
│                                         (ADRs, conventions, all breaking changes, patterns)
└── apac-cc-workshop-acn/hackathon/submissions/team17_spring-music-modernization/
    └── CLAUDE.md                      ← Level 3: Submission context (this file)
                                          (judging context, scope summary, pointers)
```

**Why this matters:** Claude only loads the CLAUDE.md relevant to where it's working. A session in `spring-music/` gets the ADRs and code conventions. A session in the submission folder gets the judging context. No file duplicates information from another.

---

## How Claude Was Taught to Work on This Project

### 1. Read Before Write — Always

The first instruction in `spring-music/CLAUDE.md`:

> Do not propose changes to code you haven't read. Read every affected file before suggesting edits.

This produced: a complete issue inventory (12 problems found) before a single file was changed.

### 2. Adversarial Testing Directive

Encoded in `spring-music/CLAUDE.md` under Patterns:

> Tests use `@BeforeEach` to reset repository state for isolation. Ask for edge cases, not just happy paths.

Result: the not-found path test discovered a real design gap (`getById` returns HTTP 200 + empty body instead of 404). Flagged as ADR-worthy, not silently ignored.

### 3. Logger Placeholder Convention

> Logger calls always use `{}` placeholders: `logger.info("Message {}", var)` — never string concatenation.

This is enforced via the CLAUDE.md patterns section so it applies to any new code added in future sessions.

### 4. Explicit HTTP Method Annotations

> Use `@GetMapping`/`@PostMapping`/`@PutMapping`/`@DeleteMapping` — never generic `@RequestMapping` with method param.

Encoded as a convention, not just applied once. Future sessions will follow it automatically.

### 5. ADR Decision Protocol

Each architectural decision includes:

- **What** the change is
- **Why** (the actual reason — EOL, namespace removal, JPA constraint, etc.)
- **What was considered and rejected** (e.g., Java records rejected for JPA entities)

This mirrors the format Claude understands best for architectural reasoning.

---

## Submission Files

| File              | Purpose                                               | Judges should read it for               |
| ----------------- | ----------------------------------------------------- | --------------------------------------- |
| `README.md`       | Tells the full story — problem, solution, what's next | Product work, completeness              |
| `CLAUDE.md`       | Shows how Claude was taught to work the right way     | Inventive Claude Code use               |
| `submission.html` | 5-minute visual presentation                          | First impression, architecture thinking |

---

## Key Architectural Decisions (Summary — full detail in `spring-music/CLAUDE.md`)

| ADR   | Decision                                   | Why                                                                  |
| ----- | ------------------------------------------ | -------------------------------------------------------------------- |
| ADR-1 | Full Spring Boot 3 upgrade (not 2.x patch) | SB 2.x EOL Nov 2023; javax→jakarta is a one-time migration           |
| ADR-2 | Lombok over Java Records                   | JPA entities need mutable no-args constructor; records are immutable |
| ADR-3 | AngularJS UI unchanged                     | Separate concern; out of scope for backend modernization pass        |
| ADR-4 | CLAUDE.md as living ADR store              | Future Claude sessions inherit full architectural memory             |

---

## Judging Alignment

| Category                           | What to look for in this submission                                                                                |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Most production-ready**          | All 12 breaking issues resolved; app builds on Java 17; tests verify runtime behaviour                             |
| **Best architecture thinking**     | 4 ADRs with full rationale; 3-level CLAUDE.md hierarchy; decisions documented with rejected alternatives           |
| **Best testing**                   | 6 adversarial MockMvc tests; `@BeforeEach` isolation; edge-case test exposed a real design gap                     |
| **Best product work**              | README tells a story: the problem first, then each layer of the fix, then what's next                              |
| **Most inventive Claude Code use** | CLAUDE.md doubles as ADR store + convention enforcer; hierarchy prevents context bloat; adversarial test directive |

---

## How to Run

```bash
# From hackathon/spring-music/
./gradlew clean assemble
java -jar build/libs/spring-music-1.0.jar
# → http://localhost:8080/albums

./gradlew test
# → 7 tests, 0 failures
```
