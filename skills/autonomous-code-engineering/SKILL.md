---
name: "autonomous-code-engineering"
description: "Autonomous code modification, test-driven validation, unified diff patching, and build orchestration."
---

# Autonomous Code Engineering Skill

## Overview
This skill guides the agent through inspecting codebases, isolating bugs, formulating surgical unified diffs, running native build pipelines, and verifying test suites.

## Step-by-Step Execution Workflow
1. **Analyze Project Context**: Scan project structure, build definitions (`Package.swift`, `project.pbxproj`, `Cargo.toml`), and existing test suites.
2. **Formulate Minimal Patch**: Construct surgical unified diffs rather than wholesale file replacements.
3. **Execute Build Verification**: Run test suites and verify compilation status.
4. **Handle Failures**: Parse compiler diagnostics, pinpoint error line numbers, and iteratively refine the patch.
