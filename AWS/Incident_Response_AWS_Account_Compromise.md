# 🚨 AWS Account Compromise – Incident Response Case Study

## 🧩 Incident Overview
- Suspicious AWS activity detected involving IAM credentials
- Indicators pointed toward **unauthorized access**
- Incident handled by SOC following IR lifecycle

---

## ⏰ Timeline of Events (UTC)

### ⏱️ 02:14 — Threat Detection
- 🛡️ GuardDuty flagged abnormal IAM behavior  
- Alert type suggested **credential misuse**

### ⏱️ 02:16 — Persistence Attempt
- 🔑 CloudTrail recorded **new access key creation**
- Action not aligned with normal admin workflow

### ⏱️ 02:18 — Reconnaissance Activity
- 🌍 `ListBuckets` API call from foreign IP
- Confirmed account enumeration phase

### ⏱️ 02:21 — Privilege Escalation
- ⚠️ `AdministratorAccess` policy attached
- High-risk action → Incident threshold crossed

### ⏱️ 02:24 — SOC Escalation
- 🚨 Alert reclassified as **Security Incident**
- Incident commander assigned

### ⏱️ 02:27 — Containment
- 🔒 IAM user disabled
- 🔑 All access keys revoked

---

## 📁 Log Sources Correlated

### 📜 CloudTrail
- Tracked IAM API calls and source IPs
- Verified **time, region, and user agent anomalies**

### 🛡️ Amazon GuardDuty
- Detected behavior matching known attack patterns
- Provided confidence for escalation

### 🌐 VPC Flow Logs
- Observed outbound traffic to non-approved regions
- No matching legitimate workload activity

### 🔍 IAM Access Advisor
- Identified **sudden use of high-privilege permissions**
- Confirmed deviation from baseline behavior

---

## 🧠 SOC Decision Analysis

### ❓ Compromise or Legitimate Admin?
- ❌ No change request or maintenance window
- ❌ IP geolocation mismatch
- ❌ New access key + admin policy = red flag

**➡️ Conclusion:** Account compromised

---

### ❓ Immediate Disable or Wait?
- ⏳ Waiting increases blast radius
- ⚠️ Admin privileges already granted

**➡️ Decision:** Immediate containment

---

### ❓ Production Impact Assessment
- 🔍 IAM user not bound to EC2 / Lambda
- ✅ No service interruption observed

**➡️ Safe to disable without downtime**

---

## 🔐 Containment & Remediation

- 🚫 Disabled compromised IAM user
- 🔑 Revoked and rotated credentials
- 📊 Reviewed historical CloudTrail logs
- 🛡️ Tightened IAM policies

---

## 📘 Lessons Learned

- 🔐 Enforce MFA for all IAM users
- 🔄 Avoid long-lived access keys
- 🧑‍🚀 Prefer IAM roles over users
- 🚨 Monitor privilege escalation aggressively

---

## 🎯 SOC Analyst Takeaway
> Fast detection + fast decisions prevented data exposure  
> **Logs don’t stop attacks — analysts do.**
