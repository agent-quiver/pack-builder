---
name: add-artifact
description: Use when adding or changing one artifact in a Quiver pack (a skill, a rulebook or other resource, a workflow, a tool contract or an agent profile). Covers the directory, the quiver.yaml manifest, SKILL.md frontmatter, budgets, skill references and the version bump.
---

# Add or change an artifact

## 1. Pick the kind and the id

| Kind | Directory | Entrypoint | Use for |
|---|---|---|---|
| `skill` | `skills/<id>/` | `SKILL.md` | a procedure an agent follows |
| `resource` | `resources/<id>/` | a rules or reference file, e.g. `rules.md` | rules or reference material |
| `workflow` | `workflows/<id>/` | the entrypoint file | several skills in a fixed order |
| `tool` | `tools/<id>/` | a tool contract | a tool's interface; never code Quiver runs |
| `agent_profile` | `agent_profiles/<id>/` | `<id>.md` | a role or persona |

The id is short and lower case: a verb for a skill (`release`), `standards.<area>` for a rulebook. The directory
name is the id with dots replaced by hyphens (`standards.git` lives in `resources/standards-git/`). Ids are unique
in the pack.

## 2. Write the entrypoint

For a skill, `SKILL.md` starts with the standard Agent Skills frontmatter and nothing else:

```markdown
---
name: <directory name>
description: Use when <the situation>. <What it produces.>
---
```

- The description says **when** to use the skill; agents choose by it.
- The main document stays within 2,000 tokens (8,000 characters). Every step and every MUST stays in it; long
  explanation and templates move to files under the artifact's directory (`reference/`), linked relatively.
- Write imperative steps. Say what to ask the person, what to produce, and where it goes.
- To name another skill of this pack, write it as its own code span, `/<name>`. A skill of another pack is named
  in prose with its pack id. Links stay inside the artifact's directory.

## 3. Write `quiver.yaml`

```yaml
id: <id>
kind: skill                 # or resource, workflow, tool, agent_profile
version: 0.1.0
title: <Title>
description: <one or two sentences: what it does and where it comes from>
card: '<one line, at most 40 tokens: when to use it and its key precondition>'
discovery:
  queries:                  # 2–5 ways an agent would ask for this; indexed for search, never shown
  - <query>
tags: [<area>]
owner: <namespace>          # transitional field (standard §7)
lifecycle:
  status: published
audience: [public]          # transitional field; the repository's access decides
execution:
  mode: content
entrypoint: rules.md        # resources and others; skills use SKILL.md
```

- `requires` lists connectors or capabilities the artifact needs. It is never a grant.
- No secrets, private hostnames or client names anywhere in a shared pack.

## 4. Version it

- New artifact: `0.1.0` while it settles, `1.0.0` when people rely on it.
- Change to an existing one: wording → patch; new guidance → minor; removed steps, changed contract or new
  requirements → major. A released version is never edited in place.
- The pack's own version moves too at the next release (see `/release-pack`).

## 5. Update the README and check

Add or update the artifact's row in the README table (kind, id, version, card), then run `quiver-check .` and fix
every finding.
