# Implementation Plan: Physical AI Book - Docusaurus Setup & Content Development

**Branch**: `001-book-specification` | **Date**: 2025-12-09 | **Spec**: [specs/001-book-specification/spec.md](spec.md)
**Input**: Feature specification from `/specs/001-book-specification/spec.md`

**Note**: This plan follows Spec-Driven Development (SDD) workflow. See `.specify/templates/commands/plan.md` for execution structure.

## Summary

Build a beginner-to-intermediate Physical AI learning book using Docusaurus v3.x as the static site generator. The book contains 1 chapter with 3 progressive lessons, each with runnable Python code examples (simulators for lessons 1-2, real hardware for lesson 3). Development organized in phases: (1) Docusaurus setup + configuration, (2) content scaffolding + example code organization, (3) CI/CD pipeline + example testing. Key technical decisions: Docusaurus v3 for documentation-first approach (constitution principle III), Python 3.9+ for learner-friendly syntax, GitHub Actions for automated example testing, and strict dependency pinning with quarterly maintenance cycles.

## Technical Context

**Language/Version**: Python 3.9+ (examples); Node.js 18+ (Docusaurus build system)
**Primary Dependencies**: Docusaurus v3.x, React 18.x (Docusaurus theme), Python standard library + commonly-used packages (RPi.GPIO, DHT library, pytest for tests)
**Storage**: Filesystem (markdown docs + Python scripts in `examples/`); no database required
**Testing**: pytest for Python example code; Docusaurus build validation (linting, link checking, search index generation)
**Target Platform**: Static site hosted on Vercel or GitHub Pages; Python examples run on Raspberry Pi 4 (Linux-based) with simulator fallback
**Project Type**: Static documentation site + code examples repository
**Performance Goals**: Docusaurus build < 2 minutes; beginner completes lesson checkpoint in < 30 minutes; code examples execute in < 5 seconds; offline-capable (static export)
**Constraints**: Markdown-only content (no videos); examples must be standalone and reproducible; all dependencies pinned; zero external API calls required
**Scale/Scope**: 1 chapter, 3 lessons, 3 code examples (+ tests), 1 glossary, 1 troubleshooting guide; ~9,000 words total initial content

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

**Principle I: Hands-On Learning First**
- ✅ PASS: All 3 lessons include runnable code examples; checkpoint exercises require code modification
- ✅ PASS: Example code tested in CI pipeline (Docusaurus build includes pytest execution)
- ✅ PASS: Lessons 1-2 include simulator setup instructions; lesson 3 includes hardware setup guide

**Principle II: Progressive Complexity**
- ✅ PASS: 3 lessons organized sequentially (What is Physical AI → Understanding Sensors → First Project)
- ✅ PASS: Difficulty indicators (🔰 beginner for 1-2, 🚀 intermediate for 3) explicitly defined
- ✅ PASS: Glossary includes all first-use terms; no unexplained concepts assumed

**Principle III: Documentation-First**
- ✅ PASS: All content in Docusaurus markdown (`docs/` directory)
- ✅ PASS: Sidebar configuration version-controlled in `sidebars.js`
- ✅ PASS: Code examples stored in `examples/` with markdown references

**Principle IV: Clear Intent & Accessibility**
- ✅ PASS: Lesson structure: concrete examples → theory → practice (per spec)
- ✅ PASS: Code comments explain "why" not "what"; diagrams included for sensor concepts
- ✅ PASS: External dependencies minimized (Python stdlib + 2-3 hardware packages)

**Principle V: Code Quality & Testing**
- ✅ PASS: All examples follow PEP 8 style; error handling included (try-catch patterns)
- ✅ PASS: Non-trivial examples (lessons 2-3) include pytest test cases
- ✅ PASS: Dependencies pinned in `requirements.txt` (FR-024)

**Principle VI: Versioning & Maintenance**
- ✅ PASS: Book version tracked (initial: v1.0.0); CHANGELOG.md maintained
- ✅ PASS: Quarterly maintenance cycle (FR-026); 1-week SLA for breaking changes (FR-028)

**GATE RESULT**: ✅ ALL PRINCIPLES PASS - Plan is aligned with constitution

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
├── plan.md              # This file (/sp.plan command output)
├── research.md          # Phase 0 output (/sp.plan command)
├── data-model.md        # Phase 1 output (/sp.plan command)
├── quickstart.md        # Phase 1 output (/sp.plan command)
├── contracts/           # Phase 1 output (/sp.plan command)
└── tasks.md             # Phase 2 output (/sp.tasks command - NOT created by /sp.plan)
```

### Source Code (repository root)

```text
book-repo/
├── docs/                                 # Docusaurus content (markdown)
│   ├── intro.md                         # Welcome, prerequisites, audience
│   ├── getting-started.md               # Setup: hardware/software requirements
│   ├── fundamentals/
│   │   ├── chapter-01-overview.md       # Chapter intro, learning objectives
│   │   ├── lesson-01-what-is-physical-ai.md
│   │   ├── lesson-02-understanding-sensors.md
│   │   ├── lesson-03-first-physical-ai-project.md
│   ├── glossary.md                      # Auto-generated from terms
│   ├── troubleshooting.md               # Common errors + solutions
│   └── _category_.json                  # Sidebar ordering (Docusaurus v3)
│
├── examples/                            # Runnable Python code
│   ├── chapter-01/
│   │   ├── README.md                    # Setup, dependencies, expected output
│   │   ├── requirements.txt             # Pinned versions (e.g., RPi.GPIO==0.7.0)
│   │   ├── lesson-01-hello-sensors/
│   │   │   ├── sensor_simulator.py      # Mock sensor for testing
│   │   │   ├── basic_read.py            # Main lesson code
│   │   │   ├── test_basic_read.py       # pytest test case
│   │   ├── lesson-02-multi-sensor/
│   │   │   ├── multi_sensor_simulator.py
│   │   │   ├── data_logger.py
│   │   │   ├── test_data_logger.py
│   │   ├── lesson-03-smart-room/
│   │   │   ├── smart_room_monitor.py
│   │   │   ├── test_smart_room_monitor.py
│   │   │   ├── config.json              # Sensor/actuator definitions
│   │   │   └── hardware_setup_guide.md  # Real hardware instructions
│   │
│   └── conftest.py                      # pytest configuration
│
├── docusaurus.config.js                 # Docusaurus v3 configuration
├── sidebars.js                          # Navigation structure
├── package.json                         # Node dependencies (Docusaurus, linters)
├── .github/workflows/
│   ├── build-and-test.yml              # CI: Build site + run Python tests
│   └── deploy.yml                       # Deploy to Vercel/GitHub Pages
│
├── CHANGELOG.md                         # Version history
├── requirements.txt                     # Python dependencies (root level)
└── .prettierrc                          # Markdown formatter config
```

**Structure Decision**: **Option A: Static Documentation Site + Examples Repository**

This structure separates documentation (Docusaurus-managed) from example code (Python-managed). Rationale:
- **Separation of concerns**: Docs can be updated independently of code examples
- **Constitution alignment**: Principle III requires docs in `docs/` and examples in `examples/`
- **CI simplicity**: Docusaurus build validates links/markdown; separate pytest pipeline validates Python code
- **Scalability**: As new chapters added, structure scales linearly (new `chapter-N` directories)
- **Learner clarity**: Examples grouped by chapter for easy discovery

## Complexity Tracking

**Status**: No violations. All principles passed. No justification needed.

---

## Development Phases

### Phase 0: Docusaurus Initialization & Configuration

**Goal**: Set up Docusaurus v3 project with all build tools configured and working.

**Deliverables**:
1. `docusaurus.config.js` — Main config with:
   - Site metadata (title, tagline, URL)
   - Theme configuration (Docusaurus default theme + custom branding)
   - Plugins: search (Algolia or built-in), analytics (optional)
   - Markdown features: code highlighting, syntax validation
2. `sidebars.js` — Navigation structure with lesson hierarchy
3. `package.json` — All Node dependencies with pinned versions
4. `.prettierrc` — Markdown formatting rules
5. `.github/workflows/build-and-test.yml` — CI pipeline:
   - Lint markdown (Prettier)
   - Validate Docusaurus build (no warnings)
   - Lint code examples (ESLint)
   - Execute pytest on all Python examples
   - Validate internal/external links
   - Generate search index
6. `.github/workflows/deploy.yml` — Deploy to Vercel/GitHub Pages on merge to main

**Estimated Duration**: 2-3 hours

**Success Criteria**:
- `npm install` succeeds with no security warnings
- `npm run build` completes in < 2 minutes
- `npm run start` launches local dev server at http://localhost:3000
- Initial placeholder content renders without errors

---

### Phase 1: Content Scaffolding & Lesson Templates

**Goal**: Create all markdown lesson files with structured templates and cross-linking.

**Deliverables**:
1. `docs/intro.md` — Welcome page with:
   - Audience description (beginner to intermediate)
   - Prerequisites (basic Python, no AI background required)
   - Learning time estimate (~3-5 hours for full chapter)
   - Next steps / chapter roadmap
2. `docs/getting-started.md` — Setup guide:
   - Hardware list + alternatives (simulator option)
   - Software installation (Python 3.9+, IDE recommendation)
   - Troubleshooting common setup issues
3. `docs/fundamentals/chapter-01-overview.md` — Chapter intro:
   - Learning outcomes (3 bullet points per spec)
   - Chapter map (3 lessons, estimated time per lesson)
   - Prerequisites and difficulty levels
4. `docs/fundamentals/lesson-01-what-is-physical-ai.md` (and 02, 03):
   - Lesson objectives (3-5 key learning goals)
   - Content sections with:
     - Concrete examples first
     - Conceptual explanation
     - Glossary callouts for new terms
     - Code snippet inline or with `include` directive
     - Checkpoint exercise description
   - Links to `examples/chapter-01/lesson-0X/`
5. `docs/glossary.md` — All terms with definitions from spec
6. `docs/troubleshooting.md` — FAQs:
   - Common sensor errors
   - Simulator vs. hardware troubleshooting
   - Python environment issues
   - Build/deployment questions
7. `docs/_category_.json` — Docusaurus v3 category ordering metadata

**Estimated Duration**: 8-10 hours (includes content writing, review, revision)

**Success Criteria**:
- All 6 markdown files created and valid
- Docusaurus build succeeds with no broken links
- Search indexes all lesson titles and glossary terms
- Sidebar navigation renders with correct hierarchy

---

### Phase 2: Example Code Development & Testing Infrastructure

**Goal**: Implement all Python examples with simulators (lessons 1-2) and hardware support (lesson 3).

**Deliverables**:
1. `examples/chapter-01/README.md` — Setup instructions:
   - Dependencies installation (`pip install -r requirements.txt`)
   - Simulator vs. hardware choice
   - How to run each lesson example
   - Expected outputs for verification
2. `examples/chapter-01/requirements.txt` — Pinned Python dependencies:
   - `RPi.GPIO==0.7.0` (or compatible cross-platform library)
   - `Adafruit-DHT==1.2.3` (or mock sensor library)
   - `pytest==7.4.0` (testing)
   - Other standard library imports only
3. Lesson 1.1 code:
   - `sensor_simulator.py` — Mock temperature sensor class
   - `basic_read.py` — Main lesson code (15-20 lines, read sensor, print output)
   - `test_basic_read.py` — pytest cases (e.g., "test_sensor_returns_valid_range")
4. Lesson 1.2 code:
   - `multi_sensor_simulator.py` — Mock 3-sensor environment
   - `data_logger.py` — Read + log to CSV (30-40 lines, error handling)
   - `test_data_logger.py` — Test CSV output, error paths
5. Lesson 1.3 code:
   - `smart_room_monitor.py` — Main logic (50-60 lines, decision rules, logging)
   - `config.json` — Sensor/threshold definitions (learner-editable)
   - `test_smart_room_monitor.py` — Test logic, state transitions
   - `hardware_setup_guide.md` — Raspberry Pi wiring, library installation for real sensors
6. `examples/conftest.py` — pytest configuration:
   - Fixtures for mock sensors
   - Mocking strategies for hardware access
   - Coverage reporting
7. CI integration:
   - GitHub Actions runs `pytest` on all examples
   - Failures block build (FR-004: examples must be executable)

**Estimated Duration**: 12-16 hours (includes simulator development, test writing, verification)

**Success Criteria**:
- All 3 lesson examples execute without errors
- All pytest tests pass with 80%+ code coverage
- `npm run build` includes pytest execution and passes
- Each example's expected output matches documented expected output
- Lessons 1-2 run in < 2 seconds; lesson 3 < 5 seconds

---

### Phase 3: Documentation Polish & Link Validation

**Goal**: Final review, link checking, search testing, and offline export validation.

**Deliverables**:
1. Link validation report:
   - All internal links working (`/docs/glossary` → `docs/glossary.md`)
   - All external links reachable (test with curl in CI)
   - Code example links point to correct files
2. Search index validation:
   - Search for "sensor" → returns lesson titles + glossary
   - Search for "Fahrenheit" → returns checkpoint exercise
   - Search for error terms → returns troubleshooting section
3. Offline export test:
   - `npm run build -- --out-dir build/` creates static export
   - Test in browser without server: file:///build/index.html works
4. Version metadata:
   - `CHANGELOG.md` created with v1.0.0 entry
   - `package.json` version bumped to 1.0.0
   - `docs/intro.md` displays version badge
5. Deployment verification:
   - Merge to main triggers GitHub Actions
   - Deploy to staging environment first
   - Verify site is live and responsive

**Estimated Duration**: 4-6 hours

**Success Criteria**:
- CI pipeline reports all checks pass (link validation, search, offline export)
- 100% of internal links valid
- Site deploys without errors
- Site loads in < 3 seconds on slow 3G

---

## Phase Integration Points

| Phase | Inputs | Outputs | Gate |
|-------|--------|---------|------|
| 0 | Tech stack selection | Working Docusaurus instance | `npm run build` passes |
| 1 | Spec + Phase 0 setup | All markdown files + navigation | No broken links in build |
| 2 | Phase 1 structure + Spec | Runnable examples + tests | `pytest` passes; SC-001 met |
| 3 | Phases 1-2 complete | Deployed site + offline export | Live site accessible; search works |

---

## Key Technical Decisions

### Decision 1: Docusaurus v3 (Not v2 or Hugo)
**Rationale**: React-based components enable future interactivity (e.g., embedded simulators); strong Markdown support aligns with Constitution III; large community; built-in search + offline export.
**Alternatives considered**: Hugo (simpler, less flexible); Next.js (overkill for static content); Sphinx (Python-centric, less modern UI).
**Tradeoff**: Requires Node.js + npm; learning curve for team unfamiliar with JavaScript tooling.

### Decision 2: Python for All Examples
**Rationale**: Beginner-friendly syntax; largest community for IoT/physical computing; cross-platform (Windows/Mac/Linux/RPi); easy simulators with unittest.mock.
**Alternatives considered**: JavaScript/Node.js (less ideal for hardware); C++ (too steep for beginners); Rust (overkill for learning book).
**Tradeoff**: Examples don't directly transfer to commercial projects using C++/Rust, but pedagogically sound for learning.

### Decision 3: Strict Dependency Pinning + Quarterly Maintenance
**Rationale**: Ensures reproducibility (FR-024); prevents surprise breakage when learners revisit old chapters; manageable maintenance cycle (quarterly).
**Alternatives considered**: Floating versions (lower maintenance, higher risk); annual maintenance (too infrequent).
**Tradeoff**: Requires dedicated maintenance effort; dependencies may become outdated between quarters (mitigated by CI warning, FR-027).

### Decision 4: Simulator First, Hardware Second
**Rationale**: Reduces hardware cost barrier (Lesson 1-2 on any computer); Lesson 3 project motivates hardware investment; simulators teach core concepts without device dependency.
**Alternatives considered**: Hardware-only (higher barrier); simulator-only (less hands-on satisfaction).
**Tradeoff**: Maintains two code paths (mocks + real hardware); requires documenting both.

---

## Risks & Mitigation

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|-----------|
| Docusaurus breaking changes in minor version update | Build fails between maintenance cycles | Low | Pin Docusaurus to patch version (e.g., `^3.0.0` → `3.0.5`); test minors in CI before adopting |
| Python library API changes (RPi.GPIO, etc.) | Example code breaks; learners hit errors | Medium | Strict pinning (FR-024); monitor library changelogs; 1-week fix SLA (FR-028) |
| Learner hardware incompatibility (Pi 3 vs 4, sensor variants) | Checkpoint fails on student hardware | Medium | Provide simulator fallback for all; troubleshooting guide; ask for hardware feedback in checkpoint submission |
| Search index bloat (future chapters) | Docusaurus build time increases | Low (v1) | Monitor build time; consider search optimization in future phases; archive old versions if needed |
| Broken external links in troubleshooting | Learner confusion | Medium | CI validates all links; quarterly review (Constitution governance); link checker tool in CI |

---

## Success Metrics (from Specification)

| Metric | Target | Verification |
|--------|--------|--------------|
| SC-001: Code examples execute in CI | 100% pass | pytest in GitHub Actions |
| SC-002: Docusaurus build clean | No warnings | CI logs |
| SC-003: Beginner completes lesson < 30 min | Achieved | User testing / checkpoint timing |
| SC-004: Intermediate adapts example | Yes | Review checkpoint submissions |
| SC-005: Code quality 90%+ | Measured | pytest coverage; linting in CI |
| SC-006: Dependencies pinned | 100% | requirements.txt validation |
| SC-007: Search finds glossary | Top 3 results | Manual search testing |
| SC-008: Progress indicator visible | Yes | Docusaurus page layout review |
| SC-009: Offline export works | Yes | `npm run build` + file:// test |
