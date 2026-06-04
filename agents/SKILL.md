---
name: master-writing-collection
description: Skill for the 大师写作合集 craft-module library. Use when the user needs structured writing guidance — inspiration, plot, character, scene, pacing, revision, line polish, or workshop feedback. Prefer the smallest useful intervention and load only the relevant module.
---

# 大师写作合集 — Agent Skill

## Overview

This skill provides access to a library of practical writing modules organized by writing phase. It does not load all modules at once. Instead, it routes the request through a vector table to find the specific module(s) needed.

## Start Here

1. Read [skill-vector-table.md](skill-vector-table.md) to tag the request by level, intent, and load strategy.
2. If the vector table points to this skill, read [references/request-router.md](references/request-router.md) for mode selection.
3. Load only the module(s) listed under the matching task category. Do not load unrelated modules.
4. For web-oriented prompt templates, refer to `../web-copy/`.

## Workspace Placement

This release is designed to live directly inside the user's writing workspace after unzip.

- Keep `agents/`, `modules/`, and `web-copy/` as sibling directories.
- Preserve relative paths if the release is copied into another writing project.
- For API wrappers without automatic skill discovery, start from this file, then load only the routing files and matched modules.

## Module Locations

All paths are relative to this skill file.

| Phase | Modules |
| --- | --- |
| Prewriting (写作前) | `../modules/01-prewriting/` |
| Drafting (写作中) | `../modules/02-drafting/` |
| Revision (写作后) | `../modules/03-revision/` |
| Router (uncertain) | `../modules/00-router.md` |

## Default Stance

- If the request is line polish: modify the text directly, do not load modules unless clarity is needed.
- If the request is local rewrite: rewrite the passage, keep facts and POV stable.
- If the request is scene diagnosis: diagnose first, then decide whether to rewrite.
- If the request is structure or plot help: give beats, options, or causal chains.
- If the request is inspiration: give seeds and directions, not finished prose.

## Minimum Load Principle

Load what you need, nothing more. If `微调润色` solves the problem, do not load `构思与结构` modules. Only escalate when the current mode cannot solve the problem cleanly.

## Relations

- `../modules/` — method documentation and actionable guidance for each writing task.
- `../web-copy/` — prompt templates for web-based AI tools (DeepSeek, Kimi, etc.).
- `../INDEX.md` — complete module index.

## Copyright

This skill is part of the 大师写作合集 open-source library. It contains no copyrighted book content — only original synthesized writing guidance.
