---
name: import-instructions
description: Use when someone already has agent instructions (CLAUDE.md, AGENTS.md, .cursor/rules, .github/copilot-instructions.md, custom GPT or project instructions, prompt files) and wants them as a Quiver pack, so every AI tool they use gets the same rules.
---

# Turn existing agent instructions into a pack

Most people already wrote rules for their AI tools, scattered across files and chat settings. This skill moves
them into one pack without losing anything and without inventing rules.

## 1. Collect the sources

Ask where the instructions live, then read them all before writing anything:

- Repository files: `CLAUDE.md`, `AGENTS.md`, `.cursor/rules/*.mdc`, `.cursorrules`,
  `.github/copilot-instructions.md`, `.windsurfrules`, `.claude/skills/*/SKILL.md`, `.claude/commands/*.md`.
- Pasted text: ChatGPT custom instructions, project instructions, a custom GPT's instructions, saved prompts.

Do not read secrets, `.env` files or credentials. If a source contains a token, a password, a private hostname or
a client's name, leave that line out and tell the person.

## 2. Sort every instruction

Put each instruction in exactly one bucket and show the person the sorted list:

| Bucket | What it is | Becomes |
|---|---|---|
| Rule | Always true for the work ("use conventional commits", "never edit generated files") | a line in a **rulebook** (resource) |
| Procedure | Steps for a recurring task ("to release: bump, changelog, tag") | a **skill** |
| Project fact | True only for one repository (paths, commands, ports, names) | stays in that repository's `CLAUDE.md` / `AGENTS.md`, not in the pack |
| Persona | Tone or role ("answer briefly", "act as a senior reviewer") | an **agent profile**, or a short rule |
| Stale or conflicting | Contradicts another instruction, or the person no longer wants it | ask; drop or fix before import |

Project facts are the most common mistake: a pack is shared, so it must hold what is true across projects.

## 3. Group into artifacts

- One rulebook per area (git, testing, writing, security, code review), named `standards.<area>`.
- One skill per recurring task, named by its verb (`release`, `review-pr`, `write-changelog`).
- Merge duplicates from different tools into one wording. Where two tools disagreed, ask which wins.
- If the result has unrelated audiences (a team's rules and a person's own habits), propose two packs.

## 4. Write them

Create each artifact with `/add-artifact`. Keep the person's own wording where it is clear; rewrite only for
clarity, never to add rules they did not have. Record the source of each artifact in its `quiver.yaml`
`description` (for example "from the team's AGENTS.md and Cursor rules").

## 5. Replace the old copies

After the first release, offer to shrink the old files to what is project-specific, plus one line pointing at
the pack (its address or submodule path). Do this only with the person's go-ahead; never delete their files
silently.

## 6. Report

List: artifacts created (kind, id, card); instructions left in the repository as project facts; instructions
dropped and why. Then continue with `/release-pack`.
