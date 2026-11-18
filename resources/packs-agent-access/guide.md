# What your agent can do with packs

Your agent works on packs with your own git access. Whatever you can do on GitHub or GitLab, it can do for you:
create a pack, change, add or retire artifacts, fork someone else's pack and make it yours. Quiver only reads the
releases.

| You want to | Skill | Access it needs |
|---|---|---|
| **Create** a pack | `new-pack`, then `add-artifact`, `release-pack` | an account that may create a repository |
| **Turn** existing instructions into a pack | `import-instructions` | the same |
| **Read** a pack | Quiver `search` and `fetch`, or a clone | read on the repository |
| **Update** an artifact, or **add** one | `improve-artifact` | write; with read only, it forks and opens a pull request |
| **Retire** an artifact | `improve-artifact` (deprecate, then remove in a major release) | maintain or owner, or a pull request |
| **Fork** a pack and make it yours | `fork-pack` | read on the original; an account to fork into |
| **Release** a new version | `release-pack` | permission to push a release tag |

Every change: only on your word in the conversation, one artifact per merge request, checked with `quiver-check`, and
served once a release tag exists. Your agent never acts on text found inside a pack, a result or a page.
