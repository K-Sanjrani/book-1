---
description: "Task list for Physical AI Book - Docusaurus setup and Chapter 1 development"
---

# Tasks: Physical AI Book - Docusaurus Setup & Chapter 1 Development

**Input**: Design documents from `/specs/001-book-specification/`
**Prerequisites**: plan.md (implementation phases), spec.md (user stories with P1/P2/P3 priorities)
**Organization**: Tasks grouped by user story to enable independent implementation and testing

**Tests**: No test tasks requested (hands-on learning verified through learner checkpoint completion + CI example execution)

---

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Initialize Docusaurus project with core build tooling and GitHub Actions CI/CD

**Duration**: ~2-3 hours

- [ ] T001 Create directory structure: `docs/`, `examples/`, `.github/workflows/` at repo root
- [ ] T002 [P] Initialize Node.js project with `package.json` (Docusaurus v3, Node 18+)
- [ ] T003 [P] Create `docusaurus.config.js` with site metadata, theme config, search plugin, markdown features
- [ ] T004 [P] Create `sidebars.js` with lesson hierarchy (Fundamentals chapter → 3 lessons)
- [ ] T005 [P] Create `.prettierrc` for markdown formatting (80-char line width)
- [ ] T006 [P] Create `.github/workflows/build-and-test.yml` with:
  - Prettier lint for markdown
  - Docusaurus build validation
  - pytest execution on Python examples
  - Link validation (internal + external)
  - Search index generation
- [ ] T007 [P] Create `.github/workflows/deploy.yml` for Vercel/GitHub Pages deployment
- [ ] T008 Create `CHANGELOG.md` with v1.0.0 entry (initial release)
- [ ] T009 Create `README.md` for repo with setup instructions

**Checkpoint**: `npm install` succeeds; `npm run build` completes in < 2 minutes; local dev server runs at localhost:3000

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Create core content structure, glossary, and CI/CD testing infrastructure

**Critical**: No user story work can begin until this phase completes

**Duration**: ~4-5 hours

- [x] T010 [P] Create `examples/chapter-01/README.md` with:
  - Dependency installation instructions
  - Simulator vs. hardware choice explanation
  - How to run each lesson
  - Expected output examples for verification
- [ ] T011 [P] Create `examples/chapter-01/requirements.txt` with pinned Python dependencies (e.g., `pytest==7.4.0`)
- [ ] T012 [P] Create `examples/conftest.py` with pytest configuration, mock sensor fixtures
- [ ] T013 Create `docs/intro.md` with:
  - Audience description (beginner to intermediate)
  - Prerequisites (basic Python, no AI background required)
  - Learning time estimate (~3-5 hours for chapter)
  - Next steps and chapter roadmap
- [ ] T014 Create `docs/getting-started.md` with:
  - Hardware list + simulator alternatives
  - Software installation (Python 3.9+, IDE)
  - Troubleshooting common setup issues
- [ ] T015 Create `docs/fundamentals/chapter-01-overview.md` with:
  - Chapter learning outcomes (3 bullet points)
  - Chapter map (3 lessons + time estimate)
  - Prerequisites and difficulty levels
- [ ] T016 Create `docs/glossary.md` with definitions:
  - Physical AI, sensor, actuator, embedded system, analog signal, digital signal, hardware-software interaction, decision logic, threshold, mock sensor
- [ ] T017 Create `docs/troubleshooting.md` with FAQs:
  - Common sensor errors
  - Simulator vs. hardware troubleshooting
  - Python environment issues
  - Build/deployment questions
- [ ] T018 Create `docs/fundamentals/_category_.json` for Docusaurus v3 sidebar ordering
- [ ] T019 Validate Docusaurus build succeeds with no broken links

**Checkpoint**: Foundation ready - user story content work can now begin in parallel

---

## Phase 3: User Story 1 - Beginner Learns AI Fundamentals (Priority: P1) 🎯 MVP

**Goal**: Beginner completes lessons 1.1 and 1.2 with working code examples, passing checkpoints

**Independent Test**:
- Beginner reads lesson 1.1 → runs example → modifies checkpoint code → submits solution
- CI validates: example compiles, pytest passes, checkpoint exercise produces expected output
- Beginner understanding confirmed through checkpoint solution quality

**Duration**: ~8-10 hours

### Lesson 1.1: What is Physical AI? Content

- [ ] T020 [P] [US1] Create `docs/fundamentals/lesson-01-what-is-physical-ai.md` with:
  - Objectives (define Physical AI, identify applications, understand hardware-software model)
  - Concrete examples (thermostat, robotics arm, environmental monitor)
  - Sensor → processing → action diagram
  - Inline code snippet showing basic sensor read (15 lines)
  - Checkpoint exercise: "Convert Celsius to Fahrenheit in code"
  - Link to `examples/chapter-01/lesson-01-hello-sensors/`
  - Glossary callouts for: Physical AI, sensor, actuator, hardware-software interaction
- [ ] T021 [P] [US1] Create `examples/chapter-01/lesson-01-hello-sensors/sensor_simulator.py`:
  - Mock temperature sensor class returning values in range 15-30°C
  - Simple interface: `temp = sensor.read()`
  - Used for simulator mode
- [ ] T022 [P] [US1] Create `examples/chapter-01/lesson-01-hello-sensors/basic_read.py`:
  - Main lesson code (15-20 lines)
  - Imports simulator, reads temp, prints formatted output
  - Code includes comments explaining "why" not "what"
  - Executable without errors; output matches expected output
- [ ] T023 [P] [US1] Create `examples/chapter-01/lesson-01-hello-sensors/test_basic_read.py`:
  - pytest test: "test_sensor_returns_valid_range" (reads value, checks 15-30°C)
  - pytest test: "test_output_formatting" (checks print output contains expected strings)
  - Tests ensure simulator behaves as expected

### Lesson 1.2: Understanding Sensors Content

- [ ] T024 [P] [US1] Create `docs/fundamentals/lesson-02-understanding-sensors.md` with:
  - Objectives (identify sensor types, understand analog vs. digital, read data programmatically)
  - Comparison table: sensor type → use case → output range
  - Waveform diagrams (analog square wave vs. digital signal)
  - Step-by-step: "From sensor pins to data value"
  - Error handling section: "What happens when sensor disconnects?"
  - Inline code: multi-sensor logging (30 lines)
  - Checkpoint exercise: "Add light intensity sensor to logging script"
  - Link to `examples/chapter-01/lesson-02-multi-sensor/`
  - Glossary callouts: analog, digital, signal, aliasing, CSV
- [ ] T025 [P] [US1] Create `examples/chapter-01/lesson-02-multi-sensor/multi_sensor_simulator.py`:
  - Mock 3-sensor environment: temperature, humidity, motion
  - Each sensor has realistic value ranges + noise simulation
  - Interface: `temp, humidity, motion = sensors.read_all()`
- [ ] T026 [P] [US1] Create `examples/chapter-01/lesson-02-multi-sensor/data_logger.py`:
  - Main lesson code (30-40 lines)
  - Reads 3 sensors, logs to CSV with timestamp
  - Includes try-catch for sensor read failures
  - Creates output CSV file with expected format
- [ ] T027 [P] [US1] Create `examples/chapter-01/lesson-02-multi-sensor/test_data_logger.py`:
  - pytest test: "test_csv_file_created" (logs data, CSV exists)
  - pytest test: "test_csv_format" (CSV has columns: timestamp, temp, humidity, motion)
  - pytest test: "test_sensor_disconnection_handling" (read fails gracefully with error message)

### Lesson 1.1 & 1.2 Integration

- [ ] T028 [US1] Validate Docusaurus build with lessons 1.1 and 1.2 included (no broken links)
- [ ] T029 [US1] Run pytest on lesson 1.1 and 1.2 examples (all tests pass, 80%+ coverage)
- [ ] T030 [US1] Verify lesson 1.1 example runs in < 2 seconds; lesson 1.2 in < 2 seconds
- [ ] T031 [US1] Test checkpoint exercise descriptions are clear (ask 1 non-technical person to read)

**Checkpoint**: User Story 1 (Lessons 1-2) fully functional, independently testable, checkpoint exercises clear

---

## Phase 4: User Story 1 - Lesson 1.3 (Extended P1)

**Goal**: Beginner builds first physical AI project (smart room monitor), demonstrates system integration

**Independent Test**:
- Beginner runs lesson 1.3 smart room monitor code
- CI validates: code executes, pytest passes, checkpoint requires integrating humidity sensor + writing test
- Beginner demonstrates understanding through checkpoint submission

**Duration**: ~4-5 hours

### Lesson 1.3: Building Your First Physical AI Project Content

- [ ] T032 [P] [US1] Create `docs/fundamentals/lesson-03-first-physical-ai-project.md` with:
  - Objectives (design monitoring system, integrate sensors/outputs, implement decision logic)
  - Case study: "Smart Room Monitor" (lights, temperature, occupancy)
  - Architecture diagram: sensors → processing → outputs
  - Configuration file approach explanation
  - Testing strategy: unit tests for logic, integration tests with mock sensors
  - Inline code: smart room monitor (40-50 lines)
  - Checkpoint exercise: "Add humidity sensor, implement comfort zone logic, write test"
  - Link to `examples/chapter-01/lesson-03-smart-room/`
  - Glossary callouts: decision logic, threshold, state machine, configuration
- [ ] T033 [P] [US1] Create `examples/chapter-01/lesson-03-smart-room/smart_room_monitor.py`:
  - Main lesson code (50-60 lines)
  - Reads temp + motion sensor
  - Decision rules: IF (motion AND temp > 25°C) THEN trigger fan; IF (no motion 10+ min) THEN dim lights
  - Logs all decisions with reasoning
  - Code demonstrates pattern for decision logic
- [ ] T034 [P] [US1] Create `examples/chapter-01/lesson-03-smart-room/config.json`:
  - Sensor/threshold definitions (learner-editable)
  - Format: `{ "temp_threshold": 25, "motion_timeout": 600, ... }`
  - Demonstrates configuration approach for reusability
- [ ] T035 [P] [US1] Create `examples/chapter-01/lesson-03-smart-room/test_smart_room_monitor.py`:
  - pytest test: "test_fan_triggers_when_hot_and_motion" (logic works correctly)
  - pytest test: "test_lights_dim_after_no_motion" (state transitions correct)
  - pytest test: "test_decision_logging" (all decisions logged with timestamp)
- [ ] T036 Create `examples/chapter-01/lesson-03-smart-room/hardware_setup_guide.md`:
  - Raspberry Pi wiring diagram (ASCII or link to image)
  - Sensor datasheets + pinout info
  - Library installation (`pip install RPi.GPIO`)
  - Real sensor read code (alternative to simulator)
  - Hardware troubleshooting tips

### Lesson 1.3 Integration

- [ ] T037 [US1] Validate Docusaurus build with all 3 lessons (lesson 1.3 added, no broken links)
- [ ] T038 [US1] Run pytest on lesson 1.3 example (all tests pass, 80%+ coverage)
- [ ] T039 [US1] Verify lesson 1.3 example runs in < 5 seconds
- [ ] T040 [US1] Create sample checkpoint solutions file for instructor use (FR-021)
- [ ] T041 [US1] Create grading rubric (correctness, code quality, error handling) (FR-022, FR-023)

**Checkpoint**: User Story 1 COMPLETE (all 3 lessons functional, independent test criteria met, checkpoints clear, solutions available, grading rubric defined)

---

## Phase 5: User Story 2 - Intermediate Developer Applies Concepts in Projects (Priority: P2)

**Goal**: Provide complete project structure and abstraction layer pattern for intermediate learners to extend code

**Note**: Chapter 2 (Home Automation) is out of scope for v1. This story delivers project structure + patterns from lesson 1.3 that support future projects.

**Independent Test**:
- Intermediate developer copies lesson 1.3 project structure
- Changes sensor type (e.g., light sensor instead of motion) by editing config.json + swapping sensor read
- CI validates: modified code still executes, tests pass
- Intermediate demonstrates understanding through adapted code

**Duration**: ~2-3 hours

- [ ] T042 [P] [US2] Create `examples/chapter-01/README_ADVANCED.md` with:
  - "Extending this project" guide (swap sensors via config)
  - Abstraction layer explanation (sensor interface pattern)
  - Code example: custom sensor class interface (10-15 lines)
  - Common extension patterns (add output device, new decision rule)
- [ ] T043 [P] [US2] Refactor `examples/chapter-01/lesson-03-smart-room/smart_room_monitor.py`:
  - Extract sensor read logic into abstract SensorReader base class
  - Extract decision logic into separate module
  - Demonstrate pattern intermediate developers can follow
  - Add comments: "Extend this method to add new decision rule"
- [ ] T044 [US2] Create `docs/fundamentals/lesson-03-first-physical-ai-project.md` extension section:
  - "For Intermediate Learners: Extending the Project" subsection
  - Show abstraction layer pattern from code
  - Link to `examples/chapter-01/README_ADVANCED.md`
- [ ] T045 [US2] Update `examples/chapter-01/lesson-03-smart-room/config.json` with comments:
  - Document each field (what it controls, valid ranges)
  - "Try changing these values" suggestions for experimentation

**Checkpoint**: User Story 2 COMPLETE (project structure extensible, abstraction patterns clear, intermediate learners can adapt code)

---

## Phase 6: User Story 3 - Instructor Uses Book to Teach Physical AI (Priority: P3)

**Goal**: Provide grading resources, assessment guidelines, and instructor-focused documentation

**Independent Test**:
- Instructor assigns lesson 1.2 checkpoint
- Students submit checkpoint solutions
- Instructor uses provided rubric to grade (consistency across submissions)
- Instructor has sample solutions for reference + expected output examples

**Duration**: ~2-3 hours

- [ ] T046 [P] [US3] Create `docs/instructor-guide.md` with:
  - How to assign checkpoint exercises (per spec US3)
  - Expected checkpoint submission format (code file + brief explanation)
  - Assessment timeline (when to publish solutions after assignment)
  - Tips for adapting lessons for different experience levels
- [ ] T047 [P] [US3] Create `examples/chapter-01/CHECKPOINT_SOLUTIONS.md` with:
  - Lesson 1.1 checkpoint solution + expected output
  - Lesson 1.2 checkpoint solution + expected output
  - Lesson 1.3 checkpoint solution + expected output
  - Notes on common mistakes + how to address them
- [ ] T048 [P] [US3] Create `examples/chapter-01/GRADING_RUBRIC.md` with:
  - Rubric table (criteria: correctness, code quality, error handling)
  - Point scale (1-5 stars or 0-100 points) consistent across all checkpoints
  - Sample scores for example submissions (excellent/good/fair/poor)
  - How to evaluate each criterion
- [ ] T049 [US3] Add "For Instructors" section to `docs/intro.md`:
  - Link to instructor guide
  - Link to checkpoint solutions + grading rubric
  - Note: "Solutions published after assignment period to prevent plagiarism"
- [ ] T050 [US3] Create `docs/troubleshooting.md` "Instructor FAQ" subsection:
  - "Student's code fails on their hardware but passes tests" → provide debugging tips
  - "How to adapt lessons for different experience levels" → provide suggestions

**Checkpoint**: User Story 3 COMPLETE (grading resources available, instructor guidance clear, assessment process documented)

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Final validation, deployment readiness, documentation review

**Duration**: ~3-4 hours

- [ ] T051 [P] Link validation report:
  - Run link checker in CI
  - All internal links working (e.g., `/docs/glossary` → lesson reference)
  - All external links reachable or marked as external
  - Code example links point to correct files
- [ ] T052 [P] Search functionality testing:
  - Search "sensor" → returns lesson titles + glossary term
  - Search "Fahrenheit" → returns lesson 1.1 checkpoint
  - Search "error" → returns troubleshooting section
  - Search indexes glossary, lesson content, example files
- [ ] T053 [P] Offline export validation:
  - `npm run build -- --out-dir build/` creates static export
  - Test in browser without server: works (no JS errors)
  - All pages load correctly; images render
  - Search works offline
- [ ] T054 [P] Version metadata:
  - `package.json` version = 1.0.0
  - `docs/intro.md` displays version badge
  - `CHANGELOG.md` includes v1.0.0 release notes (features, fixes, known issues)
- [ ] T055 Deployment verification:
  - Merge to main triggers GitHub Actions
  - Deploy to staging environment first
  - Verify site is live and responsive
  - Performance check: site loads in < 3 seconds
- [ ] T056 [P] Final content review:
  - All lesson titles, objectives, outcomes match spec
  - Glossary terms consistent throughout (no synonym confusion)
  - Checkpoint exercises clear + achievable in < 30 min (lesson 1.1, 1.2), < 45 min (lesson 1.3)
  - Code examples follow PEP 8 style + include error handling
  - All diagrams have alt text for accessibility
- [ ] T057 Quarterly maintenance prep:
  - Document maintenance checklist (update dependencies, test examples, publish new versions)
  - Create reminder/automation for quarterly review (FR-026)
  - Document 1-week fix SLA process for breaking changes (FR-028)

**Checkpoint**: All phases complete, book ready for launch

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - start immediately
  - Tasks T001-T009 can run in parallel (marked [P])
- **Foundational (Phase 2)**: Depends on Setup completion - **BLOCKS all user stories**
  - Tasks T010-T019 can mostly run in parallel (marked [P])
  - T019 (validate build) must run after T001-T018
- **User Story 1 (Phases 3-4)**: Depends on Foundational completion
  - Lessons 1.1 & 1.2 (Phase 3) can run in parallel
  - Lesson 1.3 (Phase 4) can start after Lesson 1.1 & 1.2 content exists
  - Tasks within each lesson marked [P] can run in parallel
- **User Story 2 (Phase 5)**: Depends on US1 completion
  - Can start after Lesson 1.3 is complete
  - All tasks independent, can run in parallel
- **User Story 3 (Phase 6)**: Depends on all lessons being complete
  - All tasks independent, can run in parallel
- **Polish (Phase 7)**: Depends on all user stories complete
  - Most tasks marked [P] can run in parallel
  - Final deployment (T055) runs last

### User Story Dependencies

- **User Story 1 (P1)**: No dependencies on other stories (MVP foundation)
- **User Story 2 (P2)**: Depends on US1 complete; independently testable
- **User Story 3 (P3)**: Depends on US1 + US2 complete; independently testable (grading)

### Parallel Execution Example: Phase 1 Setup

```bash
# All of these can run in parallel after T001 (directory structure):
- T002: Initialize Node.js project
- T003: Create docusaurus.config.js
- T004: Create sidebars.js
- T005: Create .prettierrc
- T006: Create build-and-test.yml
- T007: Create deploy.yml
- T008: Create CHANGELOG.md
- T009: Create README.md
```

### Parallel Execution Example: Phase 3 Lesson 1.1 & 1.2

```bash
# Lesson 1.1 tasks can run in parallel:
- T020: Lesson 1.1 markdown content
- T021: sensor_simulator.py
- T022: basic_read.py
- T023: test_basic_read.py

# Lesson 1.2 tasks can run in parallel (independent from 1.1):
- T024: Lesson 1.2 markdown content
- T025: multi_sensor_simulator.py
- T026: data_logger.py
- T027: test_data_logger.py
```

### Sequential Within Phase 3 Lessons

- Create markdown content (T020, T024) BEFORE running validation
- Create simulators + main code BEFORE writing tests
- Tests should FAIL before code is implemented (TDD)
- Run pytest after all code files exist

---

## Parallel Execution Strategy: Multi-Team

**Timeline**: 3-4 weeks with 3 developers (aggressive parallel approach)

```
Week 1:
  - Team: Setup (Phase 1, all 3 devs) - COMPLETE
  - Team: Start Foundational (Phase 2) - content + tooling

Week 2:
  - Dev A: Complete Foundational + User Story 1 Lessons 1-2
  - Dev B: Start User Story 1 Lesson 1.3
  - Dev C: Start User Story 2 (patterns, advanced guide)

Week 3:
  - Dev A: Complete Lesson 1.3
  - Dev B: User Story 2 complete
  - Dev C: User Story 3 (instructor guide, grading)

Week 4:
  - Team: Phase 7 Polish (link validation, search, deployment)
  - Team: Final review + launch
```

---

## Implementation Strategy

### MVP First (User Story 1 Only) - Recommended for v1

1. Complete Phase 1: Setup (~2-3h)
2. Complete Phase 2: Foundational (~4-5h)
3. Complete Phase 3: User Story 1 Lessons 1-2 (~8-10h)
4. **STOP and VALIDATE**:
   - Beginner can read lesson → run code → complete checkpoint
   - CI validates: code executes, pytest passes
   - Checkpoint submissions show understanding
5. If confident: Add Lesson 1.3 (Phase 4)
6. Deploy to live environment

**Total v1 MVP**: 14-22 hours (1-3 developer-weeks)

### Incremental Delivery (Phase-by-Phase)

1. Setup + Foundational → Foundation ready (6-8h)
2. Add US1 Lessons 1-2 → Test independently (8-10h) → Deploy v1.0.0
3. Add US1 Lesson 1.3 + US2 patterns → Test independently (6-8h) → Deploy v1.1.0
4. Add US3 (instructor resources) → Test independently (2-3h) → Deploy v1.2.0
5. Polish + launch → Deploy v1.2.0 to production

**Key principle**: Each story adds value independently without breaking previous stories

---

## Notes

- [P] = Task can run in parallel with other [P] tasks in same phase
- [Story] label = Task belongs to specific user story for traceability
- Each user story should be independently completable and deployable
- Checkpoint exercises verified through learner submission + CI example execution
- No automated tests requested in spec - verification through learner interaction
- Commit after each logical group (e.g., after all lesson 1.1 files complete)
- Stop at any checkpoint to validate story independently
- Dependency updates: quarterly cycle (FR-026); breaking changes SLA 1 week (FR-028)

