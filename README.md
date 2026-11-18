# Pack builder

[![Add to Agent Quiver](https://quiver.l13v.net/brand/add-to-agent-quiver.svg)](https://quiver.l13v.net/quiver?add=github.com/agent-quiver/pack-builder)

`agent-quiver/pack-builder` is an open [Quiver pack](https://github.com/agent-quiver/pack-standard): the pack for
making packs.

Most people already wrote rules for their AI tools: a `CLAUDE.md`, an `AGENTS.md`, Cursor rules, ChatGPT custom
instructions. This pack helps an agent turn those into a versioned pack that every AI tool can use, then start,
grow and release it to the pack standard.

## Use it

- **Through Quiver:** connect your AI tool to the pack and say "turn my CLAUDE.md into a pack" or "start a pack for
  our review rules".
- **As files:** clone it, or add it to a repository as a git submodule at a release tag. `skills/` follows the Agent
  Skills layout.
- **Your agent does the git work:** it creates, changes, forks and releases packs with your own GitHub or GitLab
  access, on your word (`packs.agent-access`). Quiver only reads the releases.
- **Change it:** open a pull request. A release is a tag `vX.Y.Z`; see `CHANGELOG.md`.

## Artifacts

| kind | id | version | when to use |
|---|---|---|---|
| skills | `new-pack` | 1.0.0 | Starting a new Quiver pack: pick its theme and readers, create the repository from the template, fill the manifest. |
| skills | `import-instructions` | 1.0.0 | Someone already has CLAUDE.md, AGENTS.md, Cursor rules or custom instructions: turn them into skills and rulebooks of a pack. |
| skills | `add-artifact` | 1.0.0 | Adding or changing one skill, rulebook, workflow, tool contract or agent profile in a pack, to the standard. |
| skills | `improve-artifact` | 1.0.0 | The person says an artifact is wrong or should change: fix it in its pack through a merge request, on their word, and serve the new version. |
| skills | `fork-pack` | 1.0.1 | The person wants their own version of a pack: fork it with their git access, make it theirs, release it, and serve the fork in their quiver. |
| skills | `release-pack` | 1.0.0 | A pack is ready for a new version: bump, changelog, check with the tag, then the protected release tag Quiver serves. |
| resources | `packs.agent-access` | 1.0.0 | What can my agent do with packs? Create, change, retire, fork and release them with my own git access; the skill and access for each. |
| resources | `standards.quiver-pack` | 1.1.1 | Creating or changing a Quiver pack repository: layout, quiver-pack.yaml, release tags and the check gate. |

## Licence

Text in this pack is licensed under CC-BY-4.0 (`LICENSE`).
