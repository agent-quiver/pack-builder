---
name: new-pack
description: Use when someone wants to start a new Quiver pack, to share agent skills and rules with a team or the public. Creates the repository from the pack template, sets the manifest, adds the first artifacts and gets the check green before the first release.
---

# Start a new pack

A pack is one forge repository (GitHub or GitLab). Whoever can read the repository can use the pack; nothing
else grants access. Decide that first.

## 1. Decide the pack's boundary

Ask the person, in one message:

- **What is it for?** One theme an agent can recognise from a single line (the card), for example "rules for
  writing commit messages and changelogs". Several unrelated themes are several packs.
- **Who may read it?** Everyone (public repository), a team (private repository with that team as readers), or
  only them. Artifacts with different readers go in different packs.
- **Where does it live?** The forge namespace (user or organisation) and the repository name, `pack-<theme>` by
  convention.

## 2. Create the repository

- **GitHub:** create it from the template `agent-quiver/pack-template` ("Use this template", or
  `gh repo create <owner>/<name> --template agent-quiver/pack-template --private` or `--public`). The template
  carries the check workflow.
- **GitLab:** create an empty project, copy the template's files, and include the GitLab CI component from
  `agent-quiver/quiver-check` (its README names the include and the pinned commit).

Make it private first if unsure; making it public later is one setting.

## 3. Fill the manifest

Edit `quiver-pack.yaml`:

- `id`: `<namespace>/<repository>`, lower case, exactly the repository path.
- `version`: `0.1.0` until the first artifacts settle, then `1.0.0`.
- `title`; `card`: one line, at most 40 tokens (160 characters), saying when an agent should use the pack;
  `description`: what it holds and for whom.
- `maintainers`, `license` (`CC-BY-4.0` for text is a good default for a shared pack), `tags`.
- `requires`: connectors the artifacts need, never a grant. Leave `[]` if none.

## 4. Add the artifacts

- Remove `skills/hello/`.
- If the person already has agent instructions (a `CLAUDE.md`, `AGENTS.md`, Cursor rules, prompt files), use
  `/import-instructions` to turn them into artifacts.
- Otherwise write each artifact with `/add-artifact`. Start with two or three that the person uses every week;
  a small pack that works beats a large one nobody reads.

## 5. README and CHANGELOG

- `README.md`: what the pack is for, how to use it (as files, as a git submodule at a release tag, or through
  Quiver), and a table of the artifacts: kind, id, version, card.
- `CHANGELOG.md`: an `## X.Y.Z (YYYY-MM-DD)` entry per release.

## 6. Check, then release

Run the checker locally (Python 3.11+ and uv):

```bash
uvx --from git+https://github.com/agent-quiver/quiver-check@<commit> quiver-check .
```

Fix every finding, push, and let the forge's check pass. Then release with `/release-pack`.

## 7. Tell the person how to use it

- In an AI tool through Quiver: the pack address `https://aqi-wos.l13v.net/p/<forge host>/<id>/mcp`.
- For a public pack listed for everyone: a pull request on `agent-quiver/catalog` (one small file).
