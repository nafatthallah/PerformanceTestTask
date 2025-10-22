# 🧪 Stress Test on Dummy JSON APIs

This project performs a **stress test using Apache JMeter and Taurus (bzt)** to measure API performance, identify bottlenecks, and automatically generate a **JMeter HTML dashboard** after execution.

---

## 📋 Overview

The Taurus configuration (`auto_stopper.yml`) runs a **ramp-up test** on the JMeter script
`Stress Testing on Dummy Json APIs Test Plan.jmx`.
It automatically stops the test when SLA limits are breached — for example, if p95 latency exceeds 1200 ms or the success rate drops below 98%.

After execution, Taurus generates:

* **Raw results** (`.jtl`, `.csv`)
* **Summary metrics** (`final-stats.txt`)
* **An interactive JMeter HTML report**

---

## ⚙️ Prerequisites

Before running, install the following:

### 1. **Python 3.8+**

Download from [python.org/downloads](https://www.python.org/downloads/)

### 2. **Taurus (bzt)**

```bash
pip install bzt
```

Verify installation:

```bash
bzt --version
```

### 3. **Apache JMeter 5.6.3**

Download and extract from:
[https://jmeter.apache.org/download_jmeter.cgi](https://jmeter.apache.org/download_jmeter.cgi)

Then note the **JMeter path**, for example:

```
D:/nadaf/Downloads/apache-jmeter-5.6.3/apache-jmeter-5.6.3/bin/jmeter.bat
```

Ensure this path matches the one in `auto_stopper.yml`.

---

## ▶️ Running the Test

From the command line (PowerShell or terminal):

```bash
py -m bzt auto_stopper.yml```

Taurus will:

1. Start JMeter with the provided `.jmx` file.
2. Stream live results in the console.
3. Stop the test automatically once the SLA is breached.
4. Generate all output files under a timestamped folder.

---

## 📁 Output Structure

After each run, Taurus creates a unique folder under `artifacts-dir`, as defined in the YAML:

```yaml
settings:
  artifacts-dir: "D:/perf/artifacts/%Y-%m-%d_%H-%M-%S"
```

Example generated path:

```
D:/perf/artifacts/2025-10-22_19-50-29/
```

Inside you’ll find:

```
│
├── jmeter-bzt.properties
├── kpi.jtl                     # Raw JMeter results (Taurus generated)
├── output/output.csv           # Simple Data Writer results
├── final-stats.txt             # Test summary
└── jmeter-dashboard/           # 📊 HTML report folder
    └── index.html              # Open this in your browser
```

Open:

```
D:/perf/artifacts/<timestamp>/jmeter-dashboard/index.html
```

to view the **interactive HTML performance report**.

---

## 📈 SLA & Pass/Fail Criteria

Configured in `auto_stopper.yml`:

| Metric       | Condition | Duration | Action              |
| ------------ | --------- | -------- | ------------------- |
| p95 Latency  | > 1200 ms | 30 s     | Stop test as failed |
| Failures     | > 2%      | 60 s     | Stop test as failed |
| Throughput   | < 20/s    | 60 s     | Stop test as failed |
| Success Rate | < 98%     | 60 s     | Stop test as failed |

---

## 🧱 Manual HTML Report Generation (Optional)

If you want to **manually generate or re-generate** the JMeter HTML report after Taurus finishes:

### 🪟 Windows Command Prompt / PowerShell

```bat
rem Copy the name of artifacts in the latest Taurus artifacts folder
Like this D:\perf\artifacts\2025-10-22_19-50-29


rem Create a new, empty dashboard folder
mkdir D:\perf\artifacts\2025-10-22_19-50-29\jmeter-dashboard"

rem Generate the JMeter HTML report from Taurus results (kpi.jtl)
"D:\nadaf\Downloads\apache-jmeter-5.6.3\apache-jmeter-5.6.3\bin\jmeter.bat" ^
  -Jjmeter.save.saveservice.assertion_results_failure_message=false ^
  -g D:\perf\artifacts\2025-10-22_19-50-29\kpi.jtl" ^
  -o D:\perf\artifacts\2025-10-22_19-50-29\jmeter-dashboard"
```

### 📊 Output

After execution, open:

```
D:\perf\artifacts\2025-10-22_19-50-29\jmeter-dashboard\index.html
```

Example:

```
D:\perf\artifacts\2025-10-22_19-50-29\jmeter-dashboard\index.html
```

This regenerates the HTML dashboard from the raw JMeter results.

---

## 🏁 Summary

This setup provides a **reproducible, automated stress-testing framework** that:

* Ramps load until SLA failure.
* Captures p99 latency and error spikes.
* Identifies performance bottlenecks.
* Generates a JMeter HTML performance report — either automatically or manually.
