## ✅ Law #1: Ownership & License Preamble

Every XML/patch file must begin with the following comment block, placed **above** the file header:

```xml
<!--
  Demonata Gaming Metadata Format ©2025
  Licensed for use under terms in LICENSE.md.
-->
```

This preamble asserts authorship and links to your licensing terms. Do not omit it.

## ✅ Law #2: Every Section Needs an `@group`

**Why?**

* It gives every section a name, a role, and a home.
* It makes parsing, sorting, and indexing predictable.
* It eliminates ambiguity when cross-referencing or generating docs.
* It works even if the section stands alone — today’s island might be tomorrow’s hub.

So yes: **if it’s a section, it gets a `@group`**. No exceptions.

---

## ✅ Law #3: `@group` = *What*, `@xref`/`@ref` = *Where/How*

Here’s the functional breakdown:

| Tag      | Purpose                                           | Analogy                                         | Required?       |
| -------- | ------------------------------------------------- | ----------------------------------------------- | --------------- |
| `@group` | What is this section *about*?                     | “This drawer holds screwdrivers.”               | ✅ Always        |
| `@desc`  | What does it *do*?                                | “These screwdrivers are used for X.”            | ✅ Always        |
| `@xref`  | What *other file(s)* does it relate to?           | “This screwdriver fits a bolt in that machine.” | ❌ If applicable |
| `@ref`   | What *other section in this file* does it tie to? | “This section depends on that section’s value.” | ❌ If applicable |

> **In short:**
> `@group` tells us the **category of change**.
> `@xref` and `@ref` tell us **how that change interacts** with the rest of the system.

---

## 🧠 Think of It Like Building a Mod Encyclopedia:

Every section becomes an article:

* `@group` = the article title
* `@desc` = the article summary
* `@xref`/`@ref` = internal hyperlinks to other articles

Even if nobody links *to* that article yet, it still needs a name and purpose.

---

## 🧪 Practical Benefit

When every section has a `@group`, it enables:

* **Changelog diffing by system** (e.g., “Show me all changes in ZombieBehaviorBalance”)
* **Patch scoping** (e.g., “Did this release touch BiomeDecorLoot?”)
* **File reorganization** (e.g., safely moving a section into its own file later without losing identity)

---

## 🚨 If You Don’t Use `@group` Consistently:

You’ll eventually:

* Have to retroactively fill them in during changelog creation.
* Lose the ability to generate accurate dependency graphs.
* Confuse future-you when tracing interactions across files.

**So yes. You’re not just assuming correctly — you’re building a goddamn framework.**
