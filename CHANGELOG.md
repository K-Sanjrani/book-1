# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-12-09

### Added

- Initial release of Physical AI Book
- **Fundamentals Chapter** with 3 progressive lessons:
  - Lesson 1.1: What is Physical AI? (simulator-based)
  - Lesson 1.2: Understanding Sensors (simulator-based)
  - Lesson 1.3: Building Your First Physical AI Project (hardware-ready)
- Complete working code examples with pytest tests
- Simulator support for lessons 1-2 (no hardware required)
- Hardware setup guide for lesson 1.3 (Raspberry Pi + sensors)
- Interactive checkpoints for each lesson with starter code
- Comprehensive glossary with all domain-specific terms
- Troubleshooting guide with common issues and solutions
- Instructor resources including grading rubric and checkpoint solutions
- CI/CD pipeline with automated testing and deployment
- Docusaurus-based static site with search functionality
- Offline-capable documentation export

### Features

- ✅ Hands-on learning with executable code examples
- ✅ Progressive complexity (beginner → intermediate)
- ✅ Multiple learner personas supported (individual, instructor, intermediate developer)
- ✅ Code quality standards (PEP 8, error handling, 80%+ test coverage)
- ✅ Pinned dependencies for reproducibility
- ✅ Accessible content (alt text for images, keyboard navigation)

### Known Issues

- None identified in v1.0.0

### Future Roadmap

- **v1.1**: Advanced patterns for intermediate learners (project extension examples)
- **v1.2**: Expanded instructor resources (assessment tools, classroom integration)
- **v2.0**: Chapter 2 - Home Automation Project (advanced sensors, multi-device coordination)
- **v2.1**: Chapter 3 - Real-World IoT Systems (cloud integration, data logging)

### Maintenance Notes

- Dependencies: Python 3.9+, Node.js 18+, Docusaurus v3.0.1
- Quarterly maintenance cycle for dependency updates (see FR-026)
- Breaking change SLA: 1 week to fix (see FR-028)

---

## Version History

### How to Read Version Numbers

- **MAJOR**: Framework/library changes, significant restructuring (e.g., 1.0.0 → 2.0.0)
- **MINOR**: New chapters/sections, new examples, clarifications (e.g., 1.0.0 → 1.1.0)
- **PATCH**: Typos, small clarifications, dependency patches (e.g., 1.0.0 → 1.0.1)
