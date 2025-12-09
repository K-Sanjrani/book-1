# Physical AI Book 📚🤖

A beginner-to-intermediate guide to Physical AI with hands-on learning. Build sensor-based systems, understand hardware-software interaction, and develop real-world IoT projects.

## Quick Start

### Prerequisites

- **Node.js**: v18.0.0 or higher
- **npm**: v9.0.0 or higher (comes with Node.js)
- **Python**: v3.9 or higher (for running code examples)

### Installation

1. Clone this repository:
```bash
git clone https://github.com/physical-ai-book/physical-ai-book.git
cd physical-ai-book
```

2. Install Node dependencies:
```bash
npm install
```

3. Install Python dependencies (optional, for running examples):
```bash
pip install -r examples/chapter-01/requirements.txt
```

### Running Locally

**Start the development server:**
```bash
npm start
```

The site will open at `http://localhost:3000`

**Build for production:**
```bash
npm run build
```

**Run Python examples:**
```bash
npm run test-examples
```

## 📖 Chapters & Lessons

### Chapter 1: Physical AI Fundamentals ✓ (v1.0.0)

- **Lesson 1.1**: What is Physical AI?
  - Duration: ~30 minutes
  - Hardware: Simulator (no hardware required)
  - Topics: Physical AI definition, real-world applications, hardware-software model

- **Lesson 1.2**: Understanding Sensors
  - Duration: ~45 minutes
  - Hardware: Simulator (no hardware required)
  - Topics: Sensor types, analog vs. digital signals, data collection

- **Lesson 1.3**: Building Your First Physical AI Project
  - Duration: ~60 minutes
  - Hardware: Raspberry Pi + DHT22 + PIR motion sensor (~$30)
  - Topics: System integration, decision logic, real-world deployment

**Estimated Total Time**: ~2-3 hours for complete chapter

### Future Chapters (Planned)

- Chapter 2: Home Automation Project (v2.0)
- Chapter 3: Real-World IoT Systems (v2.1)

## 🚀 Features

- ✅ **Hands-On Learning**: Every lesson includes working code examples
- ✅ **Progressive Complexity**: Clear scaffolding from beginner to intermediate
- ✅ **Simulator Support**: Start learning without hardware investment
- ✅ **Real Hardware Guide**: Complete setup instructions for Raspberry Pi projects
- ✅ **Interactive Checkpoints**: Exercises at end of each lesson
- ✅ **Complete Solutions**: Reference solutions + grading rubric for instructors
- ✅ **Offline Capable**: Download and work without internet

## 📚 Documentation

- **Getting Started**: [docs/getting-started.md](docs/getting-started.md)
- **Glossary**: [docs/glossary.md](docs/glossary.md)
- **Troubleshooting**: [docs/troubleshooting.md](docs/troubleshooting.md)
- **Instructor Guide**: See checkpoint solutions in examples/

## 🛠️ Development

### Project Structure

```
physical-ai-book/
├── docs/                    # Docusaurus markdown content
│   ├── intro.md
│   ├── getting-started.md
│   ├── fundamentals/        # Chapter 1
│   ├── glossary.md
│   └── troubleshooting.md
├── examples/                # Runnable Python code
│   └── chapter-01/
│       ├── lesson-01-hello-sensors/
│       ├── lesson-02-multi-sensor/
│       └── lesson-03-smart-room/
├── .github/workflows/       # CI/CD pipelines
├── docusaurus.config.js     # Main config
├── sidebars.js              # Navigation structure
├── package.json             # Node dependencies
└── README.md                # This file
```

### Code Quality Standards

All code examples follow:
- **PEP 8** style guidelines
- **Error handling** for production readiness
- **80%+ test coverage** with pytest
- **Pinned dependencies** for reproducibility

### Running Tests

**Docusaurus build:**
```bash
npm run build
```

**Lint markdown:**
```bash
npm run lint
```

**Format code:**
```bash
npm run format
```

**Test Python examples:**
```bash
npm run test-examples
```

## 📋 Maintenance

### Quarterly Updates

Every 3 months we:
- Update dependency versions
- Test all examples against latest libraries
- Publish patch/minor releases as needed
- Update documentation

### Breaking Changes

For any breaking changes:
- Update affected examples within 1 week
- Publish fix release
- Add migration guide to troubleshooting

See [CHANGELOG.md](CHANGELOG.md) for complete version history.

## 🤝 Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Make your changes
4. Run tests (`npm run build && npm run test-examples`)
5. Commit with clear messages (`git commit -am 'Add new feature'`)
6. Push to your fork (`git push origin feature/your-feature`)
7. Create a Pull Request

### Contributing Guidelines

- Add tests for new examples
- Update documentation for new content
- Follow code quality standards (PEP 8, error handling)
- Update CHANGELOG.md with your changes
- Ensure CI/CD pipeline passes

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙋 Support

- **Documentation**: Read the lessons and troubleshooting guide
- **Issues**: Report bugs on [GitHub Issues](https://github.com/physical-ai-book/physical-ai-book/issues)
- **Discussions**: Join our community on [GitHub Discussions](https://github.com/physical-ai-book/physical-ai-book/discussions)

## 🎯 Learning Objectives

By completing this book, you will:

- [ ] Understand what Physical AI is and why it matters
- [ ] Know common sensor types and how to read their data
- [ ] Write Python scripts to interact with hardware
- [ ] Design and implement a simple monitoring system
- [ ] Test hardware code with simulators and real devices
- [ ] Deploy your projects to Raspberry Pi
- [ ] Apply decision logic to automate real-world systems

## 📞 Contact

**Project Lead**: Physical AI Book Team
**Email**: hello@physical-ai-book.example.com
**Twitter**: [@PhysicalAIBook](https://twitter.com/physicalaibook)

---

**Made with ❤️ for learners everywhere**
