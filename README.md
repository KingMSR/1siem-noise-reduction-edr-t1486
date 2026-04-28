# 1siem-noise-reduction-edr-t1486
siem-noise-reduction-edr-t1486
# SIEM Noise Reduction - edr T1486 Case Study

## 🔴 Problem Statement
High volume of ransomware-related alerts (MITRE T1486) from  EDR caused ~500+ P3 offenses in siem, leading to alert fatigue and unnecessary Tier-3 escalations.

## 🎯 Objective
- Reduce false positives
- Improve detection fidelity
- Prevent unnecessary auto-escalation

## 🧱 Environment
- SIEM: QRadar
- EDR: Tanium
- FIM: Trend Micro

## 🔍 Root Cause
- Volume-based detection without validation
- No process-level correlation
- Auto escalation enabled (AE)

## 🛠️ Solution
- Removed Auto Escalation (AE)
- Added correlation with:
  - Suspicious processes (PowerShell, vssadmin)
  - Behavior monitoring
- Introduced exclusions (backup, patching)

## 📉 Outcome
- ~90% reduction in Tier-3 alerts
- Improved analyst efficiency
- Better signal-to-noise ratio

## 📌 Key Learning
Detection without validation = noise  
Correlation + context = fidelity

## 🔍 Sample AQL Queries

### 1. Mass File Modification Detection
```sql
SELECT sourceip, COUNT(*) AS event_count
FROM events
WHERE QIDNAME(qid) ILIKE '%file modified%'
GROUP BY sourceip
HAVING event_count > 100
LAST 5 MINUTES


2. Suspicious PowerShell Execution
SELECT *
FROM events
WHERE UTF8(payload) ILIKE '%powershell%'
AND UTF8(payload) ILIKE '%-enc%'
LAST 24 HOURS

3. Shadow Copy Deletion Detection

SELECT *
FROM events
WHERE UTF8(payload) ILIKE '%vssadmin delete shadows%'
LAST 24 HOURS

---

# 🔴 IMPORTANT (don’t break formatting)

When pasting:

- Use triple backticks:

sql / aql
These queries were used to validate and correlate SIEM signals with endpoint behavior.
