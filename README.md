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
