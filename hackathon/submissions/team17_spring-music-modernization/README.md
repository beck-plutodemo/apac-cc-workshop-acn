# Team 17 — Spring Music Modernization

## Team Members

- Charan Raghupatruni — Developer / Architect

---

## The Problem

The `spring-music` app compiles. It runs. It looks fine.

But it cannot survive its next upgrade.

**What we found in 60 minutes of archaeology:**

| Issue                                        | Severity     | Impact                                                               |
| -------------------------------------------- | ------------ | -------------------------------------------------------------------- |
| `jcenter()` repository in `build.gradle`     | **Critical** | jcenter shut down Feb 2022 — new contributors can't build            |
| `javax.persistence.*` / `javax.validation.*` | **Critical** | Spring Boot 3.x requires `jakarta.*` — app won't start               |
| `spring.profiles: mysql` in YAML             | **Silent**   | Deprecated in 2.4, silently ignored in 3.x — profiles don't activate |
| `com.mysql.jdbc.Driver`                      | **Breaking** | Removed from MySQL Connector 8+ — runtime crash on connect           |
| `MySQL55Dialect`, `ProgressDialect`          | **Breaking** | Renamed in Hibernate 6 — startup failure                             |
| Gradle 6.7 + legacy `buildscript {}` DSL     | **High**     | Incompatible with Spring Boot 3.x plugin                             |
| JUnit 4 (`@RunWith(SpringRunner.class)`)     | **Medium**   | No JUnit 5 features, no isolation primitives                         |
| 1 empty `contextLoads()` test                | **High**     | Zero behavioural coverage — nothing pins controller semantics        |

This is the real modernization problem: not a big-bang rewrite, but a quiet accumulation of time-bombs that nobody is watching.

---

## What We Built

A complete, layered migration from **Spring Boot 2.4.0 → 3.2.3** on **Java 17 LTS**, covering every layer of the stack.

### Layer 1 — Build

- Migrated `buildscript {}` + `apply plugin:` → modern `plugins {}` block
- Removed `jcenter()` (shut down); `mavenCentral()` only
- Gradle 6.7 → **8.5**
- JUnit 4 → **JUnit 5** via `useJUnitPlatform()`
- Added **Lombok** — eliminates ~60 lines of hand-written getters/setters
- `mysql:mysql-connector-java` → `com.mysql:mysql-connector-j` (artifact renamed)

### Layer 2 — Java Source

| Before                          | After                               | Why                                   |
| ------------------------------- | ----------------------------------- | ------------------------------------- |
| `javax.persistence.*`           | `jakarta.persistence.*`             | Spring Boot 3.x uses Jakarta EE 10    |
| `javax.validation.Valid`        | `jakarta.validation.Valid`          | Same Jakarta EE 10 migration          |
| `@RequestMapping(method = GET)` | `@GetMapping`                       | Idiomatic, explicit, readable         |
| `logger.info("Id: " + id)`      | `logger.info("Id: {}", id)`         | No string alloc when log level is off |
| 60 lines of getters/setters     | `@Data @Builder @NoArgsConstructor` | Lombok — same bytecode, 1/4 the code  |
| Raw `CrudRepository`            | `CrudRepository<Album, String>`     | Type safety, no unchecked warnings    |

### Layer 3 — Configuration

- `spring.profiles: mysql` → `spring.config.activate.on-profile: mysql` (fixed for all DB profiles)
- `com.mysql.jdbc.Driver` → `com.mysql.cj.jdbc.Driver`
- `MySQL55Dialect` → `MySQLDialect` (Hibernate 6 renamed API)
- `ProgressDialect` → `PostgreSQLDialect`

### Layer 4 — Tests

Replaced the empty `contextLoads()` stub with **6 adversarial MockMvc integration tests**:

1. GET `/albums` on empty repository → `[]`
2. PUT `/albums` → album persists, auto-generated ID returned
3. GET `/albums/{id}` (found) → correct fields returned
4. GET `/albums/{id}` (unknown ID) → revealed missing `@ResponseStatus(NOT_FOUND)` — a real design gap, now documented
5. POST `/albums` → title mutation verified
6. DELETE `/albums/{id}` → confirmed removal via follow-up GET

Each test resets repository state in `@BeforeEach` — isolation guaranteed.

---

## Architecture Decisions

Four decisions were made explicitly, documented in `spring-music/CLAUDE.md` as ADRs:

**ADR-1: Full Spring Boot 3 upgrade, not 2.x patch**
Spring Boot 2.x reached EOL in November 2023. The javax→jakarta migration is a one-time, non-reversible change. Patching to 2.7.x would only delay this work.

**ADR-2: Lombok over Java Records for the `Album` entity**
Java Records are immutable. JPA entities require a mutable no-args constructor for proxy generation. `@Data` + `@Builder` + `@NoArgsConstructor` satisfies both constraints.

**ADR-3: AngularJS UI left unchanged**
AngularJS 1.x is EOL, but replacing the frontend is a separate, significant concern. Out of scope for a backend modernization pass. Documented as next step.

**ADR-4: CLAUDE.md as a living Architecture Decision Record**
Every breaking change is documented in `spring-music/CLAUDE.md` with before/after and rationale. The goal: any future Claude session (or developer) that opens this project has full architectural memory without reading git history.

---

## How We Used Claude Code

| What we did                                                         | Outcome                                                                 |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Full codebase scan before writing a single line                     | Identified all 12 issues simultaneously — nothing missed                |
| Asked Claude to generate adversarial tests, not happy paths         | Tests discovered the missing `NOT_FOUND` status as an actual design gap |
| Used CLAUDE.md as the primary architectural document                | 4 ADRs encoded — future sessions won't repeat the same analysis         |
| Maintained a CLAUDE.md hierarchy (workspace → project → submission) | Each file scoped correctly; Claude never reads irrelevant context       |
| TodoWrite task list throughout                                      | Full traceability of what was done in what order                        |

---

## What's Next

- `@ResponseStatus(HttpStatus.NOT_FOUND)` on `getById` — proper REST semantics (test already exposes this)
- Replace AngularJS 1.x → Vue 3 (last remaining legacy layer)
- `docker-compose.yml` — one command to test all DB profiles
- GitHub Actions CI pipeline using the modernized Gradle 8.5 build
- OpenAPI/Swagger docs on `/api-docs`

---

## Running It

```bash
cd hackathon/spring-music

# Build
./gradlew clean assemble

# Run (H2 in-memory — no external dependencies)
java -jar build/libs/spring-music-1.0.jar
# → http://localhost:8080

# Run with MySQL
java -jar -Dspring.profiles.active=mysql build/libs/spring-music-1.0.jar

# Tests
./gradlew test
```
