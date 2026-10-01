---
name: "accessibility-gui-automation"
description: "Safe interaction with desktop applications using accessibility element trees and synthetic UI events."
---

# Accessibility GUI Automation Skill

## Overview
Provides guidelines for navigating desktop application hierarchies, selecting accessibility UI elements, and dispatching synthetic clicks and keystrokes safely.

## Operational Guidelines
1. **Identify Target Window**: Query the Accessibility subsystem for frontmost applications matching target bundle IDs.
2. **Query Element Tree**: Search for accessible nodes using roles, titles, and identifiers.
3. **Safety Verification**: Ensure the target element is visible and interactive before dispatching events.
4. **Human Interruption**: Cease automated interactions immediately upon receiving manual user input.
