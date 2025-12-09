---
sidebar_position: 2
---

# Getting Started 🚀

Set up your environment in 5-10 minutes to run Physical AI examples.

## Choose Your Path

### Path A: Read Online (0 minutes setup)
No installation needed! Read lessons directly on this site.

**What you get**: Lesson content, example code, checkpoint descriptions
**What you don't get**: Ability to run code yourself

👉 **Start reading**: [Lesson 1.1](fundamentals/lesson-01-what-is-physical-ai.md)

---

### Path B: Run Simulator (5 minutes setup)
Run Python code on your computer with simulated sensors.

**What you get**: Working code + simulator sensors + checkpoint exercises
**What you don't get**: Real sensor values (but data is realistic!)
**Cost**: $0
**Hardware**: None needed

👉 **Jump to**: [Setup for Simulator](#setup-for-simulator)

---

### Path C: Run with Real Hardware (30 minutes setup)
Run code on Raspberry Pi with actual sensors.

**What you get**: Real sensor data + complete project experience
**What you don't get**: Portability (requires Pi + sensors)
**Cost**: ~$30 for sensors
**Hardware**: Raspberry Pi 4 + sensors

👉 **Jump to**: [Setup for Real Hardware](#setup-for-real-hardware)

---

## Setup for Simulator

### Step 1: Install Python

**macOS:**
```bash
brew install python3.11
python3 --version  # Should show Python 3.11.x
```

**Windows:**
1. Download Python from https://www.python.org/downloads/
2. Run installer, check "Add Python to PATH"
3. Open Command Prompt, type: `python --version`

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install python3.11 python3.11-venv python3-pip
python3.11 --version
```

### Step 2: Clone/Download the Book Repository

```bash
git clone https://github.com/physical-ai-book/physical-ai-book.git
cd physical-ai-book
```

Or download as ZIP and extract.

### Step 3: Install Dependencies

```bash
cd examples/chapter-01
pip install -r requirements.txt
```

**On Linux, ignore errors about RPi.GPIO** — it's not available outside Raspberry Pi.

### Step 4: Verify Installation

```bash
python -m pytest --version  # Should show pytest 7.4.0
```

### Step 5: Run First Example

```bash
python lesson-01-hello-sensors/basic_read.py
```

**Expected output:**
```
Temperature (Celsius): 22.5
Temperature (Fahrenheit): 72.5
Sensor status: ✓ OK
```

✅ **Success!** You're ready to run examples.

---

## Setup for Real Hardware

### Hardware Shopping List

| Item | Cost | Where to Buy |
|------|------|--------------|
| Raspberry Pi 4 Model B (4GB) | ~$15 | Adafruit, Amazon, RS Components |
| DHT22 Temperature/Humidity Sensor | ~$5 | Adafruit, Amazon |
| PIR Motion Sensor | ~$5 | Adafruit, Amazon |
| Jumper wires (M-to-M) | ~$2 | Any electronics supplier |
| Breadboard | ~$2 | Any electronics supplier |
| Micro USB Power Supply (5V 3A) | ~$3 | Included with Pi or buy separately |
| **Total** | **~$30** | Various |

### Step 1: Set Up Raspberry Pi

1. **Download Raspberry Pi OS**:
   - Go to https://www.raspberrypi.com/software/
   - Download Raspberry Pi Imager

2. **Write OS to SD Card**:
   - Insert 32GB+ SD card
   - Open Imager, select Raspberry Pi OS (Lite or Desktop)
   - Write to card (takes 5-10 minutes)

3. **Boot Pi**:
   - Insert SD card into Pi
   - Connect USB power
   - Wait 1-2 minutes for first boot

4. **Connect via SSH or Desktop**:
   - If using Lite: SSH from terminal
   - If using Desktop: Connect monitor/keyboard

### Step 2: Install Python & Dependencies

```bash
sudo apt update
sudo apt install python3.11 python3.11-venv python3-pip git

# Enable GPIO interface (required for sensors)
sudo raspi-config
# → Interface Options → GPIO → Enable
# → Reboot when prompted
```

### Step 3: Clone Repository

```bash
cd ~
git clone https://github.com/physical-ai-book/physical-ai-book.git
cd physical-ai-book/examples/chapter-01
```

### Step 4: Install Book Dependencies

```bash
pip install -r requirements.txt
```

### Step 5: Wire Sensors (See Lesson 1.3 for Details)

Before running on hardware, wire your sensors:
- **DHT22**: Data to GPIO pin 4 (see diagram)
- **PIR**: Signal to GPIO pin 17 (see diagram)
- **GND & 5V**: As shown in hardware_setup_guide.md

### Step 6: Test Hardware Connection

```bash
python lesson-03-smart-room/smart_room_monitor.py
```

---

## Troubleshooting Setup

### "python: command not found"

**macOS**:
```bash
python3 --version  # Use python3 instead of python
# Add alias: echo 'alias python=python3' >> ~/.zshrc
```

**Windows**:
- Make sure Python was added to PATH during installation
- Try restarting terminal/PowerShell

**Linux**:
```bash
python3 --version  # Use python3 instead of python
```

### "pip: command not found"

```bash
python -m pip install -r requirements.txt
# Instead of: pip install -r requirements.txt
```

### ModuleNotFoundError: No module named 'RPi'

This is expected on non-Pi systems. The code will use simulators automatically.

On actual Raspberry Pi:
```bash
sudo apt install python3-rpi.gpio
```

### Permission Denied (Raspberry Pi GPIO)

When running on actual Pi hardware:
```bash
sudo python lesson-03-smart-room/smart_room_monitor.py
# OR add user to gpio group:
sudo usermod -a -G gpio $USER
# Log out and log back in
```

### ImportError: urllib3, requests, etc.

```bash
pip install --upgrade pip setuptools wheel
pip install -r requirements.txt --force-reinstall
```

---

## Verify Everything Works

### Test Simulator Mode

```bash
# From examples/chapter-01/
pytest lesson-01-hello-sensors/ -v
```

**Expected**: All tests pass ✅

### Test Hardware Mode (if on Pi)

```bash
python lesson-03-smart-room/smart_room_monitor.py
```

**Expected**: Real sensor values displayed

### Test Docusaurus Site

```bash
cd ../..  # Back to repo root
npm install
npm start
```

Opens at http://localhost:3000

---

## IDE Recommendations

### VS Code (Free, Recommended)
1. Download from https://code.visualstudio.com/
2. Install Python extension by Microsoft
3. Open project folder
4. Select Python interpreter (click "Python X.X.X" at bottom)

### PyCharm Community (Free)
1. Download from https://www.jetbrains.com/pycharm/
2. Open project folder
3. Configure project interpreter (Settings → Python Interpreter)

### Thonny (Simple, Great for Beginners)
1. Download from https://thonny.org/
2. Great for running Python scripts step-by-step

---

## Next Steps

### Ready to Start Learning?

1. **Path B (Simulator)**:
   - ✅ Setup complete
   - 👉 Go to [Lesson 1.1](fundamentals/lesson-01-what-is-physical-ai.md)

2. **Path C (Hardware)**:
   - ✅ Hardware wired and Python ready
   - 📖 Read Lesson 1.3 hardware setup guide
   - 👉 Run: `python lesson-03-smart-room/smart_room_monitor.py`

3. **Stuck?**
   - Check [Troubleshooting](troubleshooting.md)
   - Search [GitHub Issues](https://github.com/physical-ai-book/physical-ai-book/issues)
   - Ask in [Discussions](https://github.com/physical-ai-book/physical-ai-book/discussions)

---

**Total setup time**: 5-30 minutes (depending on path)
**Ready?** Let's go! 🚀
