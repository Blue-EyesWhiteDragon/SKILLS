---
alias: useSkill
accepts-parameters: true
usage: /useSkill --<parameter>
name: Use Skill Flow
author: Blue-EyesWhiteDragon
description: >
        A list of tools that the agent has at their disposal.
version: 1.0.0
topic: tools
date-format: YYYY-MM-DD
last-updated: 2026-05-08
---

# Flow: useSkill

## Instructions

Use the follow table to identify the skill the user wishes the agent to use.

Example:
`/useSkill --compression` -> Select Compression Skill from table -> Read Skill file associated with the entry.
`/useSkill --mastering` -> Select Mastering Skill from table -> Read Skill file associated with mastering.

| Skill       | Skill-File                                      | Relevant Tools |
|:------------|:------------------------------------------------|:---------------|
| Compression | [Compression Skill](../../COMPRESSION.SKILL.md) | None           |
