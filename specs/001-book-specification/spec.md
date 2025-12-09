# Feature Specification: Physical AI Book - Comprehensive Learning Guide

**Feature Branch**: `001-book-specification`
**Created**: 2025-12-09
**Status**: Draft
**Input**: Create a detailed specification for a physical AI book including book structure with chapters and lessons, content guidelines and lesson format, and Docusaurus-specific requirements for organisation.

## User Scenarios & Testing

### User Story 1 - Beginner Learns AI Fundamentals (Priority: P1)

A beginner with no AI background wants to understand physical AI concepts through hands-on experimentation. They need clear progression from basic theory to runnable code.

**Why this priority**: Core value proposition—the book must deliver hands-on learning to beginner audiences. Without this, the book fails its primary mission.

**Independent Test**: Can be fully tested by: A beginner follows one lesson from intro → fundamentals chapter, runs the example code, modifies it, and successfully explains the output. Delivers: Understanding of one core concept + ability to experiment.

**Acceptance Scenarios**:

1. **Given** a beginner reads Lesson 1.1 (Introduction to Sensors), **When** they run the provided Python example, **Then** they see real sensor data and understand what each value means.
2. **Given** a beginner completes Lesson 1.3 exercises, **When** they attempt the checkpoint challenge, **Then** they can modify example code to solve a new problem independently.

---

### User Story 2 - Intermediate Developer Applies Concepts in Projects (Priority: P2)

An intermediate developer wants to build a practical physical AI project using concepts from the book. They need complete working code examples and clear patterns to extend.

**Why this priority**: Supports intermediate audience; demonstrates real-world applicability; needed for project-based learning pathway.

**Independent Test**: Can be fully tested by: Following one complete application chapter (e.g., "Building a Home Automation System"), copying project structure, running it locally, and adapting one component for a different scenario.

**Acceptance Scenarios**:

1. **Given** an intermediate developer has completed Chapter 2, **When** they start the "Home Automation" project, **Then** the provided code compiles/runs without errors on their local setup.
2. **Given** an intermediate developer wants to swap out a sensor component, **When** they locate the abstraction layer in project structure, **Then** they can do so with clear documentation on the interface.

---

### User Story 3 - Instructor Uses Book to Teach Physical AI (Priority: P3)

An instructor wants to use this book as a teaching resource, assigning lessons and exercises to students. They need clear structure, exercise answers, and assessment guidelines.

**Why this priority**: Extends audience reach to educational settings; adds value through structured curriculum; lower priority than individual learner paths but important for adoption.

**Independent Test**: Can be fully tested by: Instructor assigns Lesson 1.2, student completes checkpoint, instructor has clear rubric to evaluate understanding.

**Acceptance Scenarios**:

1. **Given** an instructor assigns a lesson checkpoint, **When** students submit their modified code, **Then** instructor has a grading rubric and sample solutions available.
2. **Given** a student completes a checkpoint exercise, **When** they check the checkpoint solutions published on the book site, **Then** they can compare their code against the reference solution and grading criteria (correctness, code quality, error handling).

---

### Edge Cases

- What happens when a learner skips a lesson but tries to run code from a later lesson that depends on earlier concepts?
- How does the system handle learners with different hardware (e.g., different sensor brands)?
- What if provided code examples break due to library updates after book release?
- How are platform-specific paths handled (Windows vs. Linux vs. macOS) in examples?

## Requirements

### Functional Requirements

**Book Structure & Organization**
- **FR-001**: Book MUST contain exactly 1 chapter in initial release: "Physical AI Fundamentals"
- **FR-002**: Chapter MUST contain exactly 3 lessons with clear learning progression
- **FR-003**: Each lesson MUST include: (a) learning objectives, (b) conceptual explanation, (c) runnable code example, (d) checkpoint exercise
- **FR-004**: All code examples MUST be executable and tested in the book's build pipeline
- **FR-005**: Book MUST include a glossary defining all domain-specific terms used

**Content Guidelines**
- **FR-006**: Each lesson explanation MUST use concrete examples before abstract definitions
- **FR-007**: Code comments MUST explain "why" not "what"; behavior of code should be self-evident
- **FR-008**: Each lesson MUST include a difficulty indicator: 🔰 (beginner) or 🚀 (intermediate)
- **FR-009**: Lessons MUST build progressively; no unexplained concepts from prior lessons assumed
- **FR-010**: All external dependencies (libraries, hardware, tools) MUST be documented with version requirements

**Docusaurus-Specific Requirements**
- **FR-011**: All content MUST live in `docs/` directory following Docusaurus folder structure
- **FR-012**: Book MUST have a `sidebars.js` configuration organizing lessons hierarchically
- **FR-013**: Each lesson MUST be a separate markdown file with consistent naming: `lesson-[number]-[title].md`
- **FR-014**: Code examples MUST be stored in `examples/chapter-[number]/` with README per chapter
- **FR-015**: Navigation structure MUST support both linear (lesson-by-lesson) and topic-based (search/browse) discovery
- **FR-016**: Build process MUST validate all internal links and code examples compile without errors
- **FR-017**: Search functionality MUST index lesson content, code examples, and glossary terms

**Accessibility & Consistency**
- **FR-018**: Glossary MUST be auto-generated from canonical terms defined in spec
- **FR-019**: All images/diagrams MUST include alt text describing the content
- **FR-020**: Lesson length MUST be constrained: 1000-3000 words (ensures digestibility)

**Checkpoint Solutions & Grading**
- **FR-021**: Checkpoint solutions MUST be published openly on the book site after each lesson release
- **FR-022**: Each checkpoint MUST include a grading rubric evaluating: (a) correctness (code runs and solves the problem), (b) code quality (readability, maintainability, style), (c) error handling (graceful degradation, user feedback)
- **FR-023**: Grading rubric MUST use a consistent point scale (e.g., 1-5 stars or 0-100 points) applicable across all checkpoints

**Dependency Management & Maintenance**
- **FR-024**: All dependencies MUST be pinned to specific versions (no floating "latest" or "*" constraints); versions documented in `requirements.txt` and code comments
- **FR-025**: Example code MUST be tested against pinned dependencies in CI on every commit
- **FR-026**: Quarterly maintenance cycle MUST execute: pull latest upstream versions, test all examples, pin new versions, publish update notes
- **FR-027**: When dependencies become outdated (>6 months since last pinned version), CI MUST display clear warning on book build but MUST NOT block reading
- **FR-028**: Breaking dependency changes MUST trigger immediate manual testing and example updates (SLA: fix within 1 week of breaking change discovery)

### Key Entities

- **Chapter**: Collection of related lessons; contains metadata (chapter number, title, learning outcomes)
- **Lesson**: Atomic learning unit; contains objectives, explanation, runnable code, checkpoint exercise
- **Code Example**: Executable snippet; linked from lesson; stored in `examples/` with metadata (language, dependencies, runtime, expected output)
- **Glossary Term**: Canonical definition of domain-specific terminology; linked throughout book
- **Checkpoint**: Exercise at end of lesson; includes starter code, acceptance criteria, optional solution

---

## Success Criteria

### Measurable Outcomes

- **SC-001**: All code examples execute successfully in CI/CD pipeline (100% pass rate)
- **SC-002**: Docusaurus build completes without warnings or broken links
- **SC-003**: Beginner readers can complete Lesson 1 and pass checkpoint in under 30 minutes without prior AI experience
- **SC-004**: Intermediate readers can adapt one code example to a new scenario within the same topic area
- **SC-005**: 90% of code in examples includes error handling and follows production-quality standards
- **SC-006**: All external dependencies have pinned versions; no floating version constraints ("latest", "*")
- **SC-007**: Search returns glossary definitions within first 3 results when searching for key terms
- **SC-008**: Lesson navigation shows clear progress indicator and estimated reading/practice time
- **SC-009**: Book supports offline reading via Docusaurus static export feature

---

## Content Structure Details

### Chapter 1: Physical AI Fundamentals

**Learning Outcomes**: By chapter end, learner will: (1) understand what physical AI is and why it matters, (2) know basic sensor types and how they work, (3) write simple Python scripts to read sensor data

#### Lesson 1.1: What is Physical AI?

**Objectives**:
- Define physical AI and differentiate from traditional AI/ML
- Identify real-world applications (robotics, IoT, smart homes)
- Understand hardware-software interaction model

**Content Structure**:
- Opening analogy (e.g., "AI seeing the world through sensors")
- 2-3 concrete examples (home thermostat, robotics arm, environmental monitor)
- Simple diagram showing sensor → processing → action loop
- Glossary additions: Physical AI, sensor, actuator, embedded system

**Code Example**: Basic "Hello Sensors" program reading a temperature sensor
- Runtime: ~2 minutes
- Hardware: **Simulator provided** (browser-based or Python mock); no physical hardware required for lesson 1
- Deliverable: Console output showing simulated temperature readings

**Checkpoint Exercise**: Student modifies code to convert Celsius to Fahrenheit; validates output range is reasonable

---

#### Lesson 1.2: Understanding Sensors

**Objectives**:
- Identify common sensor types (temperature, motion, light, pressure)
- Understand analog vs. digital signals
- Read sensor data programmatically

**Content Structure**:
- Table comparing sensor types, use cases, and output ranges
- Waveform diagrams (analog vs. digital, aliasing risk)
- Step-by-step guide: "From sensor pins to data value"
- Error handling: what happens when sensor is disconnected

**Code Example**: Multi-sensor data collection and logging
- Reads 3 sensors (temperature, humidity, motion)
- Logs to CSV file with timestamps
- Includes try-catch for sensor read failures
- **Hardware**: Simulator provided (all sensors mock in browser or Python environment); no physical hardware required

**Checkpoint Exercise**: Student adds a new sensor type (light intensity); integrates into logging script

---

#### Lesson 1.3: Building Your First Physical AI Project

**Objectives**:
- Design simple monitoring system
- Integrate multiple sensors and outputs
- Implement basic decision logic (if sensor reading > threshold, trigger action)

**Content Structure**:
- Case study: "Smart Room Monitor" (lights, temperature, occupancy)
- Architecture diagram: sensors → data processing → outputs
- Configuration file approach (JSON-based sensor definitions)
- Testing strategy: unit tests for logic, integration test with mock sensors

**Code Example**: Smart room monitor
- Reads temp + motion sensor
- If motion AND temp > 25°C, trigger fan
- If no motion for 10 min, dim lights
- Logs all decisions with reasoning
- **Hardware**: Real sensors **REQUIRED** (Raspberry Pi + DHT22 temperature + PIR motion sensor); simulator reference provided for learning but project requires hands-on hardware setup

**Checkpoint Exercise**: Extend system to add humidity sensor and implement "comfort zone" logic; write test case validating new behavior

---

## Docusaurus Organization

### Directory Structure
```
book-repo/
├── docs/
│   ├── intro.md                          # Welcome, audience, prerequisites
│   ├── getting-started.md                # Setup instructions, hardware list
│   ├── fundamentals/
│   │   ├── chapter-01-overview.md        # Chapter intro + learning map
│   │   ├── lesson-01-what-is-physical-ai.md
│   │   ├── lesson-02-understanding-sensors.md
│   │   ├── lesson-03-first-physical-ai-project.md
│   ├── glossary.md                       # Auto-generated from spec
│   ├── troubleshooting.md
├── examples/
│   ├── chapter-01/
│   │   ├── README.md                     # Setup, dependencies, expected output
│   │   ├── lesson-01-hello-sensors/
│   │   │   ├── basic_read.py
│   │   │   ├── test_basic_read.py
│   │   ├── lesson-02-multi-sensor/
│   │   ├── lesson-03-smart-room-monitor/
│   ├── package.json                      # If includes Node-based tools
├── docusaurus.config.js                  # Docusaurus configuration
├── sidebars.js                           # Navigation structure
├── .github/workflows/
│   ├── build-and-test.yml               # Run example code, build site
├── CHANGELOG.md
```

### Sidebar Configuration (sidebars.js)

```javascript
module.exports = {
  tutorialSidebar: [
    'intro',
    'getting-started',
    {
      label: 'Fundamentals',
      items: [
        'fundamentals/chapter-01-overview',
        'fundamentals/lesson-01-what-is-physical-ai',
        'fundamentals/lesson-02-understanding-sensors',
        'fundamentals/lesson-03-first-physical-ai-project',
      ],
    },
    'glossary',
    'troubleshooting',
  ],
};
```

### Build & Test Pipeline

**Pre-Build Validation**:
- Lint markdown (Prettier)
- Extract and execute all code examples in CI
- Validate all internal links exist
- Ensure all external links are reachable (or mark as external)

**Post-Build Validation**:
- Docusaurus build completes without warnings
- Search index generated correctly
- Static export succeeds (offline functionality)

---

## Clarifications

### Session 2025-12-09

- Q1: Who should have access to checkpoint solutions and how detailed should the grading rubric be? → A: Solutions published openly after lesson release; rubric includes correctness, code quality, and error handling
- Q2: How much hardware abstraction and fallback support should the book provide? → A: Simulators for lessons 1-2 only; lesson 3 requires real hardware
- Q3: How should the book handle dependency maintenance and outdated code? → A: Strict version pinning with quarterly batch updates; outdated dependencies trigger CI warning

---

## Assumptions

1. **Target Hardware**: Raspberry Pi 4 or similar (Linux-based SBC); examples provided for simulators as fallback
2. **Programming Language**: Python 3.9+ for all examples (most beginner-friendly for physical AI projects)
3. **Reading Time**: ~1 hour per lesson (including practice); ~3 hours per chapter
4. **Prerequisite Knowledge**: Basic programming (variables, loops, functions); no AI/ML background assumed
5. **Deployment**: Docusaurus hosted on Vercel or GitHub Pages; no server-side backend required
6. **Version Lifecycle**: Book updated quarterly to test and pin dependency updates; major updates (new chapters) every 6 months; breaking dependency changes trigger 1-week fix SLA
7. **Accessibility Scope**: WCAG AA compliance (alt text, keyboard navigation, color contrast); not WCAG AAA
8. **Hardware Cost**: Example hardware budget under $100 USD for complete beginner setup
9. **Internet Dependency**: Initial setup requires internet (package downloads); lessons work offline afterward

---

## Out of Scope (Explicitly)

- Advanced topics (neural networks, reinforcement learning, computer vision)
- Commercial product development or deployment strategies
- Multi-language support (English only in v1)
- Mobile/tablet-specific interfaces
- Server-side backend implementation
- Live collaboration or real-time student tracking
- Certification or formal accreditation
- Video tutorials (markdown + code only)

