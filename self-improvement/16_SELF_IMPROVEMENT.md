# 16_SELF_IMPROVEMENT -- How This OS Evolves

The OS must improve the way it tells agents to improve (`../core/04_MEMORY_SYSTEM.md`, Constitution Art. X): observed failure -> smallest durable fix -> verify it fires -> prune when stale. This file governs changes to the OS itself.

## 1. Versioning

- Semantic versioning in this file's header block below. **Major**: a Constitution article changes meaning, or a file is added/removed/merged. **Minor**: new sections, skills, playbooks, adapters, or examples. **Patch**: corrections, tightening, cross-reference fixes.
- Every change appends one line to the changelog (section 6) with date, version, and rationale.
- The Constitution changes only for major versions and only when a law was demonstrated wrong or incomplete in practice -- never for style.

Current version: **1.0.0** (initial synthesis, 2026-07-06).

## 2. When to rewrite, split, or archive a file

- **Rewrite** when >30% of a file no longer matches practice, or agents demonstrably misread it.
- **Split** when a file serves two audiences or load-contexts (e.g., a skill inside a philosophy file -- move it), or exceeds the point where per-task loading is wasteful. Then update the MANIFEST graph and all cross-references in the same change.
- **Merge** when two files are consistently loaded together and cross-reference each other more than they stand alone.
- **Archive** (move to an `ARCHIVE/` folder with a tombstone note, don't delete) when a file's job disappears. The prime constraint cuts both ways: a file that no longer makes the OS materially better must go.

## 3. Integrating new research

1. Grade the source first (`../core/11_DOMAIN_INTELLIGENCE.md` section 3). Official docs and papers can change core files; community/social material can, at most, add pattern evidence -- never overturn a high-reliability rule. The prompt-reconstruction warning (`../core/00_MANIFEST.md` section 5) is permanent.
2. Locate the single canonical home for the new knowledge (MANIFEST section 3). If it fits nowhere, question whether it belongs at all before creating a new home.
3. Convert to executable form -- principle, algorithm, decision tree, checklist, prompt, or example -- before writing it in. Advice that doesn't change the next action doesn't enter.
4. Check for collisions: does the new material contradict an existing rule? Resolve explicitly (update or reject); never leave two files disagreeing.
5. Bump the version; log the change.

## 4. Self-audit procedure

Run after any major/minor change, and periodically against real usage:

1. **Success criteria check.** For each criterion in `../core/00_MANIFEST.md` section 2, name the file/section that delivers it and -- if usage data exists -- whether observed behavior improved. Criteria with no delivering section are gaps; sections delivering no criterion are cut candidates.
2. **Cross-reference check.** Every `NN_FILE.md section n` reference resolves to a real file and section.
3. **Single-home check.** Sample key concepts (verification ladder, confidence levels, source ladder, abstraction tree, autonomy stance): each defined in exactly one file, referenced elsewhere.
4. **Terminology check.** Uniform terms throughout: *confidence levels* high/medium/low; *verification ladder*; *source ladder*; *blast radius*; *elite loop*; *durable instructions*; *true blocker*.
5. **Executability check.** Open each file at random points: is this an algorithm, checklist, tree, heuristic-with-example, or prompt? Inspirational prose fails the audit.
6. **Constitution consistency.** No file contradicts an article; every article is elaborated somewhere.
7. **Load-order sanity.** MANIFEST section 7's table names files/sections that exist and suffice for each task type.

## 5. Field-testing changes

A change to the OS is a hypothesis (`../core/12_SCIENTIFIC_REASONING.md` section 2): it predicts better agent behavior. Where possible, test it -- give the same task to an agent with the old and new text and compare plans, verification behavior, and reports. At minimum, watch the next few real tasks for the failure the change was meant to prevent. A rule that never fires, or fires wrongly, gets pruned (`../core/04_MEMORY_SYSTEM.md` section 3).

## 6. Changelog

- 2026-07-06 / 1.0.0 / Initial Aurelian release.
