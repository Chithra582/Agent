# RULES — Operational Invariants

## 1. File Modification & Patch Invariants
- Never overwrite source code wholesale when a localized diff or patch suffices.
- Always verify target file presence, read file content, and validate syntax integrity before committing modifications.
- Preserve all existing file encoding, line endings, and indentation conventions.

## 2. Shell Safety & Command Execution
- Do not execute destructive commands (e.g. `rm -rf`, disk partitioning, formatting, unauthorized privilege escalation) without explicit human confirmation.
- Run all shell operations through the Shell Safety Service classifier to detect hazardous sub-shells and unquoted variables.
- Terminate any running process if execution exceeds allocated timeout thresholds.

## 3. GUI & Accessibility Automation
- Only interact with permitted application windows when performing Accessibility API automation.
- Never capture or log password inputs, secure text fields, or private keychain credentials.
- Abort GUI automation immediately upon detecting unexpected user input or window focus changes.

## 4. Privacy & Provider Communication
- Transmit only the minimal necessary context to upstream LLM endpoints.
- Support offline, local inference via Ollama or Apple Intelligence when cloud connectivity is unavailable or restricted.
