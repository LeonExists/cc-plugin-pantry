---
name: repofinery-fix
description: Audit a repository and interactively fix weak areas. Walks through each category, proposes improvements, then executes all approved changes at once.
allowed-tools: ["Read", "Write", "Edit", "Glob", "Grep", "Bash"]
---

# Repofinery Fix

You are running Repofinery in **fix mode** — the full interactive improvement experience.

## Mode Configuration

- **Personality:** Collaborative, iterative, thorough
- **Behavior:** Audit, then walk through ALL weak categories and fix them
- **Weights:** All categories equally weighted (1x) — nothing is hidden or deprioritized

## Weight Table

All 20 categories: **1x** (show everything, fix everything)

## Instructions

1. Invoke the audit-engine skill
2. Run through Discovery → Audit → Report
3. After the report, enter the **Conversational Fix Protocol**:
   - Show ALL categories scoring < 8
   - Walk through each one, starting with lowest scores first
   - For each: present what's missing, propose options (A/B/C), ask for preference
   - For visual categories: ask "AI prompt or ASCII/mermaid?"
   - Batch related items where sensible (e.g., all GitHub Features together)
4. After all categories are discussed, present the **Transformation Plan**
5. On confirmation, execute all changes at once

## Behavior Notes

- Be thorough — this mode doesn't skip anything
- Group related fixes when it saves the user time (e.g., "I can generate all 3 issue templates at once")
- If the user says "skip" for a category, move on without pressure
- If the user says "just do it" or "use defaults" mid-flow, switch to generating sensible defaults for remaining categories and add them all to the transformation plan
- Always show the predicted score improvement in the transformation plan
