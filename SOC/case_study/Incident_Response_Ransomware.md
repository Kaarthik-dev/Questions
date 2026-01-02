# 🔐 Ransomware Alert — SOC L2 / L3 Incident Case Study

## 🧩 Incident Context
- Environment: Mid-size enterprise
- OS: Windows
- Security Stack: EDR + SIEM + Firewall
- Scenario: Suspected ransomware activity on a user endpoint

---

## ⏰ Incident Timeline (SOC Real-World Flow)

### 🕒 09:42 — Initial Detection (T0)
- 🚨 EDR alert triggered for **mass file modification**
- 🗑️ Shadow copies deleted via:
vssadmin delete shadows
- Severity automatically classified as **High**

---

### 🕒 09:45 — SOC Triage (T+3 min)
- 🔍 Analyst validation confirms:
- Rapid file extension changes (`.locked`, `.crypt`)
- Process chain:
  - `powershell.exe → cmd.exe → unknown binary`
- SIEM shows spike in file write events

---

### 🕒 09:49 — Scope Assessment (T+7 min)
- 🌐 Network logs reveal:
- SMB connections from infected host
- Attempts to access **2 internal servers**
- ⚠️ No alerts from servers yet  
- **Potential lateral movement identified**

---

### 🕒 09:52 — Escalation (T+10 min)
- 🚨 Escalated to IR Lead
- Incident officially declared:
**Confirmed Ransomware**

---

### 🕒 09:54 — Containment (T+12 min)
- 🔒 Endpoint isolated via EDR
- 🚫 SMB traffic temporarily blocked at firewall
- 👤 User account disabled to prevent misuse

---

### 🕒 10:02 — Threat Identification (T+20 min)
- 🧬 File hash matched in Threat Intelligence
- Ransomware family identified:
**LockBit variant**
- 🌍 C2 domains and IPs extracted

---

### 🕒 10:12 — Eradication Phase (T+30 min)
- 🔎 IOC sweep across environment
- ✅ No additional infected endpoints found
- Persistence mechanisms identified:
- Scheduled Task
- Registry Run Key

---

### 🕒 10:45 — Recovery (T+1 hr)
- ♻️ Endpoint wiped and reimaged
- 💾 Files restored from **offline backup**
- 🔓 Network access restored in controlled manner

---

### 🕒 +24 Hours — Post-Incident Review
- ✅ No reinfection observed
- 📊 Monitoring level increased
- 🟢 Incident formally closed

---

## 📁 Logs & Telemetry Used (REAL SOC VIEW)

### 🖥️ Endpoint / EDR Logs (Most Critical)
- Process execution tree
- File modification velocity
- Shadow copy deletion
- Registry modifications
- Scheduled task creation

---

### 📊 SIEM Logs
- Correlation alerts
- File integrity monitoring
- Time-based behavior patterns  
- Used to confirm **mass encryption**

---

### 🪟 Windows Event Logs
- **Security**
- Event ID 4688 (process creation)
- **System**
- Service creation events
- **Application**
- Crashes caused by encrypted files

---

### 🌐 Network Logs
- Firewall logs (SMB, RDP)
- DNS logs (C2 resolution attempts)
- Proxy logs (malicious domain access)

---

### 💾 Backup & Storage Logs
- Backup success/failure status
- Last known clean restore point
- Backup integrity validation

---

## 🧠 SOC Decision Points (Interview-Critical)

### ❓ Decision 1: Ransomware or Noisy Malware?
**Decision:** ✅ Ransomware confirmed  
**Reasoning:**
- Mass encryption behavior
- Shadow copy deletion
- Known ransomware TTP alignment

---

### ❓ Decision 2: Immediate Isolation?
**Decision:** ✅ YES  
**Why:**
- Encryption propagates rapidly
- Evidence can still be preserved
- Single-host isolation < org-wide impact

---

### ❓ Decision 3: Shut Down the System?
**Decision:** ❌ NO (initially)  
**Why:**
- Memory artifacts would be lost
- C2 communication still observable
- Persistence not yet identified

---

### ❓ Decision 4: Block C2 Domains/IPs?
**Decision:** ✅ YES  
**Why:**
- Prevent key exchange
- Stop command updates
- Block further payload delivery

---

### ❓ Decision 5: Restore or Pay Ransom?
**Decision:** ✅ Restore from backups  
**Why:**
- Offline backups intact
- Ransom payment not guaranteed
- Legal and compliance risks

---

### ❓ Decision 6: Notify Stakeholders?
**Decision:** ✅ YES  
**Trigger Conditions:**
- Confirmed ransomware
- Potential data exposure
- Regulatory obligations

---

## 🧾 Executive Incident Summary

- **Attack Type:** Ransomware (LockBit variant)
- **Initial Vector:** Phishing email attachment
- **Impact Scope:** Single endpoint
- **Data Loss:** None
- **Downtime:** ~2 hours
- **Root Cause:** User executed malicious attachment

---

## 🛡️ Preventive & Hardening Actions

- 📧 Strengthened email filtering
- 🧩 Macro execution restrictions
- 🛡️ EDR policy hardening
- 🎓 User security awareness training

---

## 🎯 SOC Takeaway
> Fast isolation and disciplined decision-making  
> prevented lateral spread and business disruption.
