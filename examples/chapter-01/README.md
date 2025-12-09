# Chapter 1: Physical AI Fundamentals - Examples

This directory contains all runnable code examples for Chapter 1 lessons.

## Quick Start

### Prerequisites

- Python 3.9 or higher
- pip (Python package manager)

### Installation

1. **Install dependencies:**
```bash
cd examples/chapter-01
pip install -r requirements.txt
```

2. **Choose your path:**

#### Option A: Simulator (No Hardware Required)
If you don't have hardware yet, all examples work with built-in simulators:

```bash
# Lesson 1.1
python lesson-01-hello-sensors/basic_read.py

# Lesson 1.2
python lesson-02-multi-sensor/data_logger.py

# Lesson 1.3
python lesson-03-smart-room/smart_room_monitor.py
```

#### Option B: Real Hardware (Raspberry Pi)
If you have a Raspberry Pi with sensors, see the hardware setup guide in `lesson-03-smart-room/hardware_setup_guide.md`

## Directory Structure

```
chapter-01/
├── README.md                          # This file
├── requirements.txt                   # Python dependencies (pinned versions)
├── conftest.py                        # pytest configuration
├── lesson-01-hello-sensors/
│   ├── sensor_simulator.py           # Mock temperature sensor
│   ├── basic_read.py                 # Main lesson code
│   └── test_basic_read.py            # pytest test cases
├── lesson-02-multi-sensor/
│   ├── multi_sensor_simulator.py     # Mock 3-sensor environment
│   ├── data_logger.py                # Main lesson code
│   └── test_data_logger.py           # pytest test cases
└── lesson-03-smart-room/
    ├── smart_room_monitor.py         # Main project code
    ├── config.json                   # Learner-editable configuration
    ├── test_smart_room_monitor.py    # pytest test cases
    └── hardware_setup_guide.md       # Raspberry Pi setup instructions
```

## Running Examples

### Lesson 1.1: Basic Sensor Reading

```bash
python lesson-01-hello-sensors/basic_read.py
```

**Expected Output:**
```
Connected to temperature sensor
Current temperature: 22.5°C
```

**What It Does:**
- Reads temperature from a simulated sensor
- Displays the value in a readable format

**Checkpoint Exercise:**
Modify `basic_read.py` to convert Celsius to Fahrenheit

### Lesson 1.2: Multi-Sensor Data Logging

```bash
python lesson-02-multi-sensor/data_logger.py
```

**Expected Output:**
```
Data logging started (10 readings)
Sample output saved to readings.csv
Readings completed successfully
```

**What It Does:**
- Reads 3 sensors (temperature, humidity, motion) simultaneously
- Logs readings to CSV file with timestamps
- Handles sensor read errors gracefully

**Checkpoint Exercise:**
Add a light intensity sensor to the data logger

### Lesson 1.3: Smart Room Monitor Project

```bash
python lesson-03-smart-room/smart_room_monitor.py
```

**Expected Output:**
```
Starting Smart Room Monitor...
Configuration loaded from config.json
[12:30:45] Reading sensors...
[12:30:45] Temperature: 26°C, Motion: Detected
[12:30:45] DECISION: Fan ON (temperature exceeded threshold)
[12:30:55] No motion detected, lights will dim in 9:59...
[12:31:05] DECISION: Lights DIMMED (no motion for 10+ minutes)
```

**What It Does:**
- Monitors room conditions with integrated sensor logic
- Makes decisions based on temperature and motion thresholds
- Logs all decisions with reasoning

**Checkpoint Exercise:**
Extend the system to include humidity sensor and implement "comfort zone" logic

## Running Tests

### Run all tests for Chapter 1:

```bash
pytest -v
```

### Run tests for a specific lesson:

```bash
pytest lesson-01-hello-sensors/test_basic_read.py -v
pytest lesson-02-multi-sensor/test_data_logger.py -v
pytest lesson-03-smart-room/test_smart_room_monitor.py -v
```

### View test coverage:

```bash
pytest --cov=. --cov-report=html
open htmlcov/index.html
```

## Expected Output Examples

### Lesson 1.1 Output

```
$ python lesson-01-hello-sensors/basic_read.py
Temperature (Celsius): 22.5
Temperature (Fahrenheit): 72.5
Sensor status: ✓ OK
```

### Lesson 1.2 Output (readings.csv)

```
timestamp,temperature,humidity,motion
2025-12-09 12:30:45,22.5,55.3,1
2025-12-09 12:30:46,22.6,55.2,1
2025-12-09 12:30:47,22.5,55.4,0
```

### Lesson 1.3 Output

```
[12:30:45] Temperature: 25°C, Motion: YES → Fan OFF (below threshold)
[12:30:55] Temperature: 26°C, Motion: YES → Fan ON (exceeded threshold)
[12:30:57] Motion: NO (timer started)
[12:40:57] Motion: NO (10+ minutes) → Lights DIMMED
```

## Troubleshooting

### "ModuleNotFoundError: No module named 'RPi'"

**This is expected!** The examples use mocks for simulator mode. This error only appears if you try to run real hardware code without a Raspberry Pi.

**Solution**: Stick with simulator mode or follow the hardware setup guide.

### Tests fail with import errors

**Solution**: Make sure you installed requirements.txt:
```bash
pip install -r requirements.txt
```

### Examples run but produce unexpected output

**Solution**: Check that you're in the correct directory:
```bash
cd examples/chapter-01
python lesson-01-hello-sensors/basic_read.py
```

### Port already in use (if using real hardware)

**Solution**: Close other Python processes using GPIO pins:
```bash
ps aux | grep python
kill <process_id>
```

## Simulator vs. Hardware

| Aspect | Simulator | Hardware |
|--------|-----------|----------|
| Cost | $0 | ~$30 |
| Setup time | 1 minute | 30 minutes |
| Realistic data | Yes (mocked) | Yes (actual sensors) |
| Learning value | High | Very High |
| Availability | Anytime | Requires Pi + sensors |

**Recommendation**: Start with simulator, then transition to hardware for Lesson 1.3.

## Dependencies

All dependencies pinned to known-good versions for reproducibility:

```
pytest==7.4.0           # Testing framework
pytest-cov==4.1.0       # Coverage reporting
```

If you need to update dependencies (e.g., for security patches), see `requirements.txt` comments.

## Further Exploration

### Modify the examples:
- Change sensor thresholds in `config.json` (Lesson 1.3)
- Add new decision rules in `smart_room_monitor.py`
- Create custom sensor simulators

### Extend the project:
- Add humidity threshold logic
- Implement fan speed control (not just on/off)
- Add data visualization
- Log to a cloud database

### Real hardware next:
- Follow `lesson-03-smart-room/hardware_setup_guide.md`
- Connect real sensors to Raspberry Pi
- Test examples on actual hardware

## Questions?

See the troubleshooting guide in `../../docs/troubleshooting.md` or check GitHub Issues.

---

**Total time to complete all examples**: 2-3 hours
