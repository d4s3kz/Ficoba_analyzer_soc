# FICOBA SOC Analyzer

Secure Python tool for SOC-style analysis of FICOBA access logs.

## Context

This project was developed in an educational cybersecurity context.
The goal is to analyze FICOBA-style logs and detect suspicious behaviors after a possible credential compromise.

## Features

The tool detects:

- external or invalid IP addresses
- off-hours access
- MFA anomalies (`MFA_FAIL`, `MFA_BYPASS`)
- suspicious `MFA_FAIL -> MFA_BYPASS` pattern
- abnormal query volume per session
- data export activity
- burst activity in short time windows
- multiple IPs used by the same user
- concurrent sessions for the same user

## Expected log format

```text
[TIMESTAMP] USER | ROLE | IP | APP | ACTION | RESOURCE | QUERY_COUNT | STATUS | MFA | SESSION_ID
```

Example:

```text
2026-01-31T22:14:25Z | m.bernard | agent_interministeriel | 185.193.44.21 | API_FICOBA | SEARCH | PERSONNE | 500 | SUCCESS | - | SID100207
```

## Usage

Run the analyzer on a log file:

```bash
python ficoba_analyzer.py -l access_ficoba.log
```

Generate a text report:

```bash
python ficoba_analyzer.py -l access_ficoba.log -o report.txt
```

Generate a JSON report:

```bash
python ficoba_analyzer.py -l access_ficoba.log -j -o report.json
```

## Secure development points

This tool includes:

- input validation
- safe parsing of malformed lines
- exception handling
- no unexpected crash on invalid log entries
- explicit exit codes
- robust report generation

## Academic context

Developed by **Adel Salah Eddine KHALFAOUI**  
Module: **Développement sécurisé**  
Promo: **2025-CSC2**  
EFREI Paris - 2025/2026
