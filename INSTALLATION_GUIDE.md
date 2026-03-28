# KISHKANU Installation & Setup Guide

**Quantum Antibiotic Resistance Enzyme Scanner v0.1.1**

This guide covers installation on Windows, macOS, and Linux.

---

## System Requirements

| Component | Requirement | Status |
|---|---|---|
| Python | 3.8 or higher | ✅ Required |
| OS | Windows, macOS, Linux | ✅ Compatible |
| RAM | 256 MB minimum | ✅ Very light |
| Disk Space | ~50 MB | ✅ Minimal |
| Dependencies | None (stdlib only) | ✅ Perfect |

---

## Installation Steps

### Step 1: Verify Python Installation

**Windows (Command Prompt):**
```cmd
python --version
```

**macOS / Linux (Terminal):**
```bash
python3 --version
```

**Expected output:**
```
Python 3.8.0
```
or higher.

If Python is not installed, download from https://www.python.org/downloads/

---

### Step 2: Download KISHKANU

**Option A: Clone from GitHub (recommended)**

```bash
git clone https://github.com/sectio-aurea-q/kishkanu.git
cd kishkanu
```

**Option B: Download ZIP**

1. Visit https://github.com/sectio-aurea-q/kishkanu
2. Click "Code" → "Download ZIP"
3. Extract the ZIP file
4. Open Terminal/Command Prompt in the extracted folder

**Option C: Download Single File**

If you only want the executable (not the full repo):

```bash
# Download just the Python script
curl -O https://raw.githubusercontent.com/sectio-aurea-q/kishkanu/main/kishkanu_v0.1.1.py
```

---

### Step 3: Verify Installation

```bash
# Check file exists
ls -la kishkanu_v0.1.1.py

# OR on Windows:
dir kishkanu_v0.1.1.py
```

---

## Running KISHKANU

### Basic Run (Default Settings)

**Windows:**
```cmd
python kishkanu_v0.1.1.py
```

**macOS / Linux:**
```bash
python3 kishkanu_v0.1.1.py
```

This will:
1. Scan 9 antibiotic resistance enzymes
2. Classify them as quantum-critical
3. Export results to current directory
4. Display summary statistics

**Output files created:**
- `KISHKANU_FULL_REPORT.json` — Complete structured results
- `KISHKANU_RESULTS.csv` — Spreadsheet-compatible format

---

### Custom Output Directory

```bash
python3 kishkanu_v0.1.1.py --output ./results/
```

This creates a `results/` folder and saves output there.

---

### Enable Debug Logging

```bash
python3 kishkanu_v0.1.1.py --verbose
```

Shows detailed processing logs for troubleshooting.

---

### Get Help

```bash
python3 kishkanu_v0.1.1.py --help
```

---

## Using KISHKANU as a Python Module

You can import KISHKANU into your own Python scripts:

```python
#!/usr/bin/env python3

from kishkanu_v0.1.1 import run_analysis, built_in_resistance_enzymes

# Run analysis
result = run_analysis(output_dir='./my_results', verbose=True)

# Access results
stats = result['statistics']
scores = result['scores']

# Print summary
print(f"Quantum-critical enzymes: {stats['quantum_critical_count']}")
print(f"Total scanned: {stats['total_scanned']}")
print(f"Average Lindblad score: {stats['avg_lindblad_score']:.3f}")

# Iterate through results
for score in scores:
    print(f"\n{score.enzyme_name}")
    print(f"  Quantum-critical: {score.quantum_critical}")
    print(f"  Tunneling probability: {score.tunneling_probability:.1%}")
    print(f"  Catalytic multiplier: {score.catalytic_efficiency_multiplier:.2f}x")
```

Save as `analyze.py` and run:
```bash
python3 analyze.py
```

---

## Understanding the Output

### Console Output Example

```
2026-03-28 19:09:31 - KISHKANU - INFO - KISHKANU v0.1.1
2026-03-28 19:09:31 - KISHKANU - INFO - Scanning 9 antibiotic resistance enzymes...
2026-03-28 19:09:31 - KISHKANU - INFO - ⚡ TEM-1 Beta-Lactamase: Lindblad=0.351, Tunneling=61.5%, Multiplier=9.92x
...
2026-03-28 19:09:31 - KISHKANU - INFO - Total enzymes scanned: 9
2026-03-28 19:09:31 - KISHKANU - INFO - Quantum-critical resistance: 9 (100.0%)
2026-03-28 19:09:31 - KISHKANU - INFO - Average Lindblad Score: 0.390
2026-03-28 19:09:31 - KISHKANU - INFO - Average Tunneling Probability: 0.633
```

**What it means:**
- ⚡ = Quantum-critical enzyme (tunneling-dependent)
- Lindblad Score = 0.0 (classical) to 1.0 (fully quantum)
- Tunneling % = Estimated quantum contribution to catalytic rate
- Multiplier = How much faster the enzyme works due to tunneling

### JSON Output (KISHKANU_FULL_REPORT.json)

```json
{
  "title": "KISHKANU v0.1.1 - Quantum Antibiotic Resistance Enzyme Scanner",
  "timestamp": "2026-03-28T19:09:31.123456",
  "summary": {
    "total_enzymes_scanned": 9,
    "quantum_critical_count": 9,
    "quantum_critical_percentage": 100.0,
    "avg_lindblad_score": 0.390,
    "avg_tunneling_probability": 0.633,
    "avg_catalytic_multiplier": 10.07
  },
  "results": [
    {
      "pdb_id": "1BTL",
      "enzyme_name": "TEM-1 Beta-Lactamase",
      "resistance_class": "Beta-Lactamase",
      "quantum_critical": true,
      "lindblad_score": 0.351,
      "tunneling_probability": 0.615,
      "catalytic_efficiency_multiplier": 9.92,
      "confidence": 0.400,
      "structural_features": [
        "Catalytic_Serine_Proton_Transfer",
        "Oxyanion_Hole_Hydrogen_Bond"
      ],
      "biological_implications": "QUANTUM-CRITICAL: ..."
    }
  ]
}
```

### CSV Output (KISHKANU_RESULTS.csv)

```csv
PDB_ID,Enzyme_Name,Resistance_Class,Quantum_Critical,Lindblad_Score,Tunneling_Probability,Catalytic_Multiplier,Confidence
1BTL,TEM-1 Beta-Lactamase,Beta-Lactamase,True,0.351,0.615,9.92,0.400
1BLH,BLIP-bound TEM-1 Beta-Lactamase,Beta-Lactamase,True,0.351,0.615,9.92,0.400
...
```

Open this in Excel, LibreOffice, or Google Sheets for analysis.

---

## Troubleshooting

### Problem: "Python command not found"

**Solution:**
- **Windows:** Use `python` (not `python3`)
- **macOS/Linux:** Use `python3` (not `python`)
- Verify Python installation: `python3 --version`

### Problem: "Permission denied"

**On macOS/Linux:**
```bash
chmod +x kishkanu_v0.1.1.py
./kishkanu_v0.1.1.py
```

### Problem: "ModuleNotFoundError"

KISHKANU uses only Python standard library (no external packages needed).

If you get module errors:
1. Verify Python version: `python3 --version` (must be 3.8+)
2. Reinstall Python from https://www.python.org/downloads/

### Problem: Output files not created

Check file permissions:
- Windows: Run Command Prompt as Administrator
- macOS/Linux: Check folder write permissions (`ls -la`)

---

## Advanced Usage

### Process Multiple Enzyme Files

Create a Python script `batch_analyze.py`:

```python
#!/usr/bin/env python3

from kishkanu_v0.1.1 import run_analysis
import os

output_dirs = ['batch_1', 'batch_2', 'batch_3']

for output_dir in output_dirs:
    os.makedirs(output_dir, exist_ok=True)
    result = run_analysis(output_dir=output_dir)
    print(f"Completed {output_dir}: {result['statistics']['quantum_critical_count']} quantum-critical enzymes")
```

```bash
python3 batch_analyze.py
```

### Integration with Shell Scripts

**Linux/macOS:**
```bash
#!/bin/bash

echo "Running KISHKANU..."
python3 kishkanu_v0.1.1.py --output ./results/

# Process results
if [ -f ./results/KISHKANU_RESULTS.csv ]; then
    echo "Analysis complete!"
    head -5 ./results/KISHKANU_RESULTS.csv
fi
```

Save as `run_kishkanu.sh`:
```bash
chmod +x run_kishkanu.sh
./run_kishkanu.sh
```

---

## System-Specific Notes

### Windows-Specific

1. **File paths:** Use backslashes `\` or forward slashes `/`
   ```cmd
   python kishkanu_v0.1.1.py --output C:\Users\YourName\results\
   ```

2. **PowerShell:** If using PowerShell instead of Command Prompt:
   ```powershell
   python .\kishkanu_v0.1.1.py
   ```

3. **Unicode output:** If you see garbled characters, set encoding:
   ```cmd
   chcp 65001
   python kishkanu_v0.1.1.py
   ```

### macOS-Specific

1. **Homebrew Python:** Ensure Homebrew Python is used, not system Python
   ```bash
   which python3  # Should output /usr/local/bin/python3
   ```

2. **M1/M2 Macs:** Native ARM support, no compatibility issues

### Linux-Specific

1. **Package manager Python:** Update if using system Python
   ```bash
   sudo apt install python3.11  # Debian/Ubuntu
   sudo yum install python3.11  # RedHat/CentOS
   ```

2. **Virtual environments (optional):**
   ```bash
   python3 -m venv kishkanu_env
   source kishkanu_env/bin/activate
   python3 kishkanu_v0.1.1.py
   ```

---

## Performance

**Typical Execution Times:**

- Scan 9 enzymes: < 1 second
- Export JSON: < 100 ms
- Export CSV: < 50 ms
- **Total runtime: ~1 second**

KISHKANU is extremely fast. No optimization needed for typical use.

---

## Support & Contact

**Issues or Questions?**

- 📧 Email: meg.depth@proton.me
- 🐙 GitHub Issues: https://github.com/sectio-aurea-q/kishkanu/issues
- 📖 Documentation: See README.md and KISHKANU-QUELLEN.md

---

## Next Steps

1. ✅ **Install KISHKANU** (this guide)
2. 📊 **Run the analysis** (`python3 kishkanu_v0.1.1.py`)
3. 📈 **Review results** (check JSON/CSV files)
4. 🔬 **Validate findings** (compare with your enzyme databases)
5. 🌍 **Share with peers** (contact prof.marx@ruhr-uni-bochum.de, etc.)

---

**KISHKANU** — Installation complete. Ready to analyze quantum antibiotic resistance.

March 2026.
