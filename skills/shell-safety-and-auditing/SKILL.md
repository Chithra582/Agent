---
name: "shell-safety-and-auditing"
description: "Pre-execution command safety risk classification, parameter sanitization, and audit logging."
---

# Shell Safety and Auditing Skill

## Overview
Ensures all terminal operations executed by the autonomous agent adhere to strict security constraints, preventing accidental data loss or unauthorized modifications.

## Safety Check Sequence
1. **Syntax & AST Analysis**: Parse command strings to detect hazardous recursion, redirection to system files, or unquoted variables.
2. **Risk Classification**: Classify commands into Low (read-only), Medium (local writes), and High (system-level/root modifications).
3. **Confirmation Gating**: Escalate High-risk commands for explicit human confirmation.
4. **Audit Logging**: Persist execution timestamps, stdout, stderr, and exit codes to the local activity log.
