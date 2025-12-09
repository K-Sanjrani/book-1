# Physical AI Book Constitution

## Core Principles

### I. Hands-On Learning First

Every example, tutorial, and exercise must include working code. Readers should be able to run, modify, and experiment with examples immediately. No theoretical-only sections without accompanying implementation guides.

**Rules:**
- All code examples must be executable and tested in the book's build pipeline
- Each concept introduces a practical exercise before diving into theory
- Runnable projects included for major chapters
- Clear setup instructions provided for all examples

### II. Progressive Complexity

Content is organized from absolute beginner to intermediate, with clear scaffolding between levels. Readers should never encounter unexplained concepts; prerequisites are always explicit.

**Rules:**
- Each section builds on prior knowledge without gaps
- Advanced topics appear in separate "deep dive" sections clearly marked
- Glossary terms explained on first use
- Difficulty indicators on exercises (🔰 beginner, 🚀 intermediate)

### III. Documentation-First

All content lives in Docusaurus markdown before any other format. Docusaurus is the single source of truth for the book.

**Rules:**
- Content organized in `docs/` directory following Docusaurus conventions
- Sidebar and navigation configuration version-controlled
- All code examples stored in `examples/` with references in markdown
- Search functionality tested in each release

### IV. Clear Intent & Accessibility

Content is written for diverse learners with varying backgrounds. Every explanation uses concrete examples before abstract definitions. Terminology is consistent throughout.

**Rules:**
- One main concept per section (max 3-5 subsections)
- Visual diagrams included for complex concepts
- Code comments explain "why" not "what"
- External links and dependencies are minimized and documented

### V. Code Quality & Testing

Code in the book must be production-ready (or clearly marked as "pedagogical"). Examples demonstrate best practices, not shortcuts.

**Rules:**
- All executable examples follow project code style
- Example code includes error handling
- Tests included for non-trivial examples
- Dependencies pinned to known-good versions

### VI. Versioning & Maintenance

The book tracks semantic versioning. Changes to code examples or dependencies require documentation and may trigger version bumps.

**Rules:**
- MAJOR: Framework/library version changes, significant restructuring
- MINOR: New chapters/sections, new examples, clarifications
- PATCH: Typos, small clarifications, dependency patches
- Changelog maintained for each version

## Technology & Documentation Standards

### Docusaurus Configuration
- Version: Latest stable Docusaurus v3.x
- Language: JavaScript/TypeScript for examples and tooling
- Theme: Standard Docusaurus theme with custom branding
- Search: Algolia or built-in (depending on deployment)

### Example Code Organization
- Root: `examples/` directory with subfolders per chapter
- Format: Runnable scripts, notebooks, or project directories
- README: Each example has clear setup and run instructions
- Testing: Unit tests provided for non-trivial examples

### Documentation Structure
- `docs/intro.md` — Quick start and audience
- `docs/fundamentals/` — Core concepts (chapters 1-3)
- `docs/applications/` — Practical projects (chapters 4-6)
- `docs/advanced/` — Deep dives and edge cases
- `docs/troubleshooting.md` — Common issues and solutions
- `docs/glossary.md` — All key terms defined

## Development Workflow

### Content Creation
- Write content in markdown (Docusaurus native format)
- Include code examples inline or via file references
- Commit examples with documentation changes
- Test all examples locally before committing

### Review & Quality Gates
- All PRs must pass:
  - Linting (Prettier, ESLint for code blocks)
  - Example code execution tests
  - Link validation (no broken internal/external references)
  - Docusaurus build succeeds without warnings

### Release Process
- Merge to `main` triggers automated build and deployment
- Version bump documented in `CHANGELOG.md`
- GitHub Releases notes include what changed in examples/docs
- Pinned example dependencies tracked in separate lock file

## Governance

This constitution supersedes all other practices and is the source of truth for editorial and technical decisions on the book project.

**Amendment Process:**
- Significant changes (new sections, principle additions) require unanimous team agreement
- Documentation changes (typos, link updates) follow standard PR process
- All amendments documented in version control with rationale

**Compliance & Review:**
- Every PR must explicitly verify compliance with at least three principles
- Code reviews must check for hand-on-ness and progressivity
- Monthly review of outdated examples and broken links

**Version**: 1.0.0 | **Ratified**: 2025-12-09 | **Last Amended**: 2025-12-09
