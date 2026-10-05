# INTRUSION DETECTION USING LOG HASHING

**Unified Enterprise Cryptographic Log Integrity Monitoring & SOC Forensics Platform**  
*Single Application Architecture for B.Tech CyberSecurity Project Demonstration*

---

## 1. Executive Summary
**INTRUSION DETECTION USING LOG HASHING** is an enterprise-grade cybersecurity web platform developed as a **single, unified, cohesive Single-Page Application (SPA)**. 

Unlike conventional multi-page demonstrations, this system operates entirely from a single entry point (`index.html`), maintaining persistent client-side application state across all functional views: **Home**, **Dashboard**, **Log Files**, **Integrity Monitor**, **Security Alerts**, **Test Lab**, **Log Analysis**, and **How It Works**.

---

## 2. Visual Design & Theme System
Designed to replicate an authentic enterprise **Security Operations Center (SOC)**:
- **Background**: Clean, crisp white & subtle slate (`#f8fafc`, `#ffffff`)
- **Typography**: Inter & JetBrains Mono with zero default raw browser elements
- **Accents**: Deep Navy (`#0f172a`) and Enterprise Blue (`#1d4ed8`)
- **Containers**: Professional cards with subtle borders, soft shadows, rounded corners, and status badges
- **Controls**: Custom file dropzone, interactive log terminal viewer, confirmation modals, toast alerts, and real-time activity timelines.

---

## 3. Unified Application Architecture (SPA)

The application provides a single persistent navigation header with client-side view switching without full-page reloads:

```text
ONE UNIFIED APPLICATION (index.html)
├── 01. HOME            (Hero, core capabilities, cryptographic pipeline diagram)
├── 02. DASHBOARD       (Statistics, live monitored target, system health, recent activity)
├── 03. LOG FILES       (Drag-and-drop upload, log repository table, read-only terminal viewer)
├── 04. INTEGRITY       (Deterministic SHA-256 workbench, baseline comparison, tamper banners)
├── 05. ALERTS          (Incident alert center, detailed modal inspections, recommendations)
├── 06. TEST LAB        (Automated attack vectors: Test 01 to Test 05, real-time detection latencies)
├── 07. ANALYSIS        (Heuristic rule engine, search filters by keyword/user/IP/status)
└── 08. HOW IT WORKS    (7-stage lifecycle methodology, architecture flowcharts, avalanche effect)
```

### Shared Application State
All views share a single reactive state:
- When a baseline is anchored in **LOG FILES**, it is immediately updated in **INTEGRITY MONITOR**, **DASHBOARD**, **ANALYSIS**, and **ALERTS**.
- Tampering simulated in **TEST LAB** instantly reflects on the **DASHBOARD** counters and dispatches alerts to the **SECURITY ALERT CENTER**.

---

## 4. Cryptographic Hashing Implementation
The application employs true, deterministic **SHA-256 (FIPS PUB 180-4 standard)**:

```python
import hashlib

def calculate_hash(file_path):
    sha256 = hashlib.sha256()
    with open(file_path, "rb") as file:
        while chunk := file.read(4096):
            sha256.update(chunk)
    return sha256.hexdigest().upper()
```

- **Collision Resistance**: $2^{128}$ operations required to find two identical digests.
- **The Avalanche Effect**: Modifying even 1 bit of an entry flips over 50% of the 256 output bits.
- **Wording Standard**: Hash mismatches are designated as `POSSIBLE LOG TAMPERING DETECTED`, adhering to strict digital forensic reporting guidelines.

---

## 5. Security Test Lab & Attack Simulation

The dedicated **Security Test Lab** allows examiners to test 5 distinct threat vectors:
1. **TEST 01: Original Log Verification** — Proves bitwise match against pristine baseline.
2. **TEST 02: Single-Line Modification** — Altering an IP address in authentication records.
3. **TEST 03: Multiple-Line Modification** — Renaming users and modifying privilege flags.
4. **TEST 04: Log Entry Deletion** — Simulating an adversary wiping their breach timestamps.
5. **TEST 05: Log Entry Addition** — Simulating covert backdoor command injection.

---

## 6. Project Directory Structure
```text
intrusion-log-hashing/
├── app.py                     # Unified Flask backend & cryptographic REST API
├── requirements.txt           # Python dependencies (Flask >= 3.0.0)
├── README.md                  # System documentation
├── test_system.py             # Automated unit verification test suite
│
├── templates/
│   └── index.html             # Single entry point for all 8 SPA views & modals
│
├── static/
│   ├── css/
│   │   └── style.css          # Enterprise Blue/White design system
│   └── js/
│       └── app.js             # Shared state manager, client router, and API driver
│
├── logs/
│   ├── sample_auth.log        # SSH & sudo authentication events
│   ├── sample_system.log      # Kernel & system maintenance logs
│   ├── sample_security.log    # WAF, port scans, & privilege elevation alerts
│   └── sample_webserver.log   # HTTP access & injection probe logs
│
└── data/
    ├── baselines.json         # Authoritative reference SHA-256 digests
    └── state.json             # Persisted SOC incident state & activity timeline
```

---

## 7. How to Run the Application

### Prerequisites
- Python 3.8+ installed.

### Step 1: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 2: Launch Application Server
```bash
python app.py
```

### Step 3: Access Unified Platform
Open your browser and navigate to:
```text
http://127.0.0.1:5000
```

---

## 8. Demonstration Procedure for Examination

1. **Access Single Entry Point**: Open `http://127.0.0.1:5000`. The complete platform loads with persistent enterprise navigation.
2. **Explore Navigation**: Click through **HOME**, **DASHBOARD**, **LOG FILES**, **INTEGRITY**, **ALERTS**, **TEST LAB**, **ANALYSIS**, and **HOW IT WORKS** to observe seamless client-side view switching.
3. **Upload or Select Log**: In **LOG FILES**, drag-and-drop a custom `.log`, `.txt`, or `.csv` file, or select `sample_auth.log`.
4. **Anchor Baseline**: Click **CREATE BASELINE**. A modal appears explaining cryptographic anchoring. Confirm creation.
5. **Verify Clean Log**: Navigate to **INTEGRITY MONITOR** &rarr; click **VERIFY LOG INTEGRITY**. Observe the banner display:  
   `✓ LOG INTEGRITY VERIFIED — The current log matches the trusted baseline.`
6. **Execute Test Lab Attack**: Go to **TEST LAB** &rarr; click **RUN ALL 5 TESTS**. Observe sub-millisecond detection latencies for single-line, multi-line, deletion, and addition attacks.
7. **Simulate Tampering**: Click **SIMULATE LOG TAMPERING**. Observe the original entry change from `failure` to `succeeded`, triggering an immediate SHA-256 divergence.
8. **Inspect Dispatched Alert**: Switch to **ALERTS** &rarr; click **VIEW** on `ALT-001` to inspect baseline vs. tampered hash values and SOC remediation steps.
9. **Heuristic Filter Search**: Switch to **ANALYSIS** &rarr; filter events by keyword, username (`admin`), IP (`192.168.1.105`), or status (`SUSPICIOUS`).
10. **Generate Forensic Report**: In **LOG FILES**, click **GENERATE SECURITY REPORT** to download an audit file.

---

## 9. Baseline Protection Architecture & Security Limitations

In production Security Operations Centers (SOCs) and digital forensics environments, protecting the baseline reference database is critical to the integrity of the detection pipeline.

### Limitations of Local JSON Storage
In this microproject implementation, baseline SHA-256 digests are stored locally within `data/baselines.json`.
- **The Threat Model**: If an adversary obtains root/administrator write access to the host machine, they could theoretically tamper with the target log file *and simultaneously overwrite `baselines.json`* with the newly computed hash. This would evade detection during simple verification.

### Enterprise Baseline Protection Strategies
To harden baseline storage against tampering in real-world deployments:
1. **Operating System File Permissions (Access Control Lists / ACLs)**:
   - Restrict write access to `baselines.json` so that only a dedicated, privileged security daemon user can update the baseline.
   - Set the baseline repository as read-only (`chmod 444` on Linux or `icacls filename /deny Everyone:(W)` on Windows) after initial enrollment.
2. **Write-Once-Read-Many (WORM) Storage & Remote Centralized Vaults**:
   - Transmit calculated baseline hashes to a separate, isolated logging server (e.g., SIEM, syslog-ng over TLS, or AWS S3 Object Lock in Compliance Mode) where records cannot be overwritten or deleted even by root.
3. **Hardware Security Modules (HSM) & Digital Signatures**:
   - Cryptographically sign each baseline hash using a private key held in an HSM or TPM chip. Verification tests both the log file hash and the digital signature of the baseline record.
4. **Append-Only Merkle Tree Log Architecture**:
   - Construct a Merkle tree of sequential log events, where each entry commits to all prior logs, making retroactive modification cryptographically unfeasible without invalidating the root head.

---

## 10. Automated Periodic Verification & Missing File Detection

- **60-Second Background Verifier**: A daemon thread continuously checks all monitored logs every 60 seconds, comparing live disk digests against `baselines.json`. Discrepancies immediately dispatch SOC incidents without requiring user interaction.
- **Missing File Tracking**: Monitored files are cataloged independently in `data/monitored.json`. If a monitored log is deleted or moved, the platform retains its baseline and flags the file as `MISSING` (`FILE_NOT_FOUND`), preventing attackers from covering their tracks through file deletion.
