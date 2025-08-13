# 📚 Metadata Standards for 7 Days to Die Modding
_Designed for DemonataCore Mod Suite_

---

## 📌 Purpose

This document defines the structured metadata conventions used across all XML patch files for mods developed under the **Demonata Gaming** umbrella. It integrates best practices for documentation, organization, long-term maintainability, and automation of patch notes and changelogs.

The goal is threefold:

1. Help you (and future you) remember what the hell you did.
2. Automate changelogs and internal documentation generation.
3. Deliver a studio-grade modding experience.

---

## 🧠 Core Metadata Tags

| Tag       | Purpose                                      | Scope                | Required | Description |
|-----------|----------------------------------------------|----------------------|----------|-------------|
| `@group`  | Functional system the section belongs to     | Per section block    | ✅ Yes   | Used for doc grouping, changelogs, modularity |
| `@desc`   | Describes what the section does              | Per section block    | ✅ Yes   | Player-facing effect summary |
| `@notes`  | Adds developer context or clarifications     | Per section block    | ⚠️ Recommended | Dev notes, balance details, engine quirks |
| `@xref`   | Cross-links to another file/section          | Cross-file reference | 🔄 Optional | Shows system dependencies across files |
| `@ref`    | Internal link to another section in same file| Intra-file reference | 🔁 Optional | Aids logic chaining or dependencies within a file |

---

## 🔧 Tag Details & Examples

### `@group`
Classifies the section's **mechanical purpose**, not just its data type.

```xml
@group BiomeMineGoreExpansion
```

Shared across files when part of a multi-file system. Used for changelogs, filtering, internal organization.

---

### `@desc`
Concise summary of gameplay impact. Avoid implementation specifics.

```xml
@desc Adds explosive mine decorations to all biomes and increases gore block count in the Wasteland.
```

Appears in public patch notes and summaries.

---

### `@notes`
Internal modder guidance: edge cases, interactions, limitations, or balance rationale.

```xml
@notes
- Gore blocks here cause infection via blocks.xml effects.
- Decorative mines do NOT explode—see traps.xml for active variants.
```

---

### `@xref`
Used for pointing to other files this one relies on.

```xml
@xref blocks.xml → SECTION: GORE BLOCK INFECTION
```

Never points outside the current modlet suite. Helps map cross-file dependencies.

---

### `@ref`
Used for **intra-file references**.

```xml
@ref SECTION: PLAYER DAMAGE SYSTEM BASELINE
```

Ensures traceability between linked XML logic.

---

## 🧱 Metadata Header Format (Top of File)

> **New requirement:** Add the ownership/license preamble comment block at the very top of each file, above the metadata header example shown below.

```xml
<!--
  Demonata Gaming Metadata Format ©2025
  Licensed for use under terms in LICENSE.md.
-->
```


Every large XML file begins with a metadata block:

```xml
<!--
  Demonata Gaming Metadata Format ©2025
  Licensed for use under terms in LICENSE.md.
-->
<!--
  ==================================================
  Entity Tweaks - Forest Zombies
  @version     1.0.2
  @date        2025-08-04
  @author      Demonata Gaming
  @group       EntityBalance_Forest
  @description
    Adjusts spawn frequencies and toughness of common
    zombies in the Pine Forest biome.
  @xref        spawning.xml → SECTION: PINE FOREST SPAWN RULES
  @notes
    - Related buffs in buffs.xml (infection rates).
    - Difficulty tuned for veteran players starting new games.
  ==================================================
-->
```

### ✅ Required fields:

- Ownership & License preamble comment block (at the very top of every file)


- `@version`
- `@date`
- `@author`
- `@group`
- `@description`

### Optional:

- `@notes` (recommended)
- `@xref` (for major file-wide dependencies)

---

## 🧩 Section Header Format (Within Files)

Use this to separate major blocks of logic:

```xml
<!-- ===============================
     SECTION: PLAYER DAMAGE SYSTEM
     ===============================
     @group     CombatBalance
     @desc      Base damage model for ranged and melee.
     @notes     Balances around headshot-only rules and zombie reach changes.
     @xref      buffs.xml → SECTION: DAMAGE MODIFIER STAGES
-->
```

### Rules:

- Always use **ALL CAPS** for `SECTION:` titles.
- Each section **must** have its own `@group` and `@desc`.
- Use `@notes` when behavior isn’t obvious.
- Use `@xref` only for mechanical or systemic ties.

---

## 🎨 Capitalization Rules

| Element       | Format     |
|---------------|------------|
| File header   | Title Case |
| Section title | ALL CAPS   |
| `@xref/@ref`  | Must match **exactly** the section name with `SECTION:` or `MAIN:` prefix |

---

## 🧑‍💻 Best Practices Recap

- Use a file-level metadata block at the top of every XML patch.
- Use `SECTION:` blocks any time logic changes within a file.
- Use `@xref` and `@ref` to create a navigable dependency map.
- Ensure every `@xref` points to a real header with exact naming.
- Document gameplay impacts first—implementation notes second.

---

## 🚧 Optional Automation Usage

These tags support:

- Internal changelog bundling via tag grouping
- Patch note generation from `@desc`
- Cross-system tracing through `@xref`/`@ref`
- Git-friendly structure for collaborative workflows

---

## 🧬 Final Thoughts

Structured XML is the backbone of scalable modding. Whether you’re solo or working with a team, these standards will keep your files readable, debuggable, and future-proof.

You can mod like a wild man—or you can mod like a studio. This is how we mod like a studio.
