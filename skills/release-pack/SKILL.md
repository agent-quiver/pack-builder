---
name: release-pack
description: Use when a Quiver pack is ready for a new version that agents should receive. Bumps the pack version, writes the changelog entry, checks the pack with the tag, and creates the release tag that Quiver serves.
---

# Release a pack

A release is a tag `vX.Y.Z` on the default branch. Quiver serves the newest release that passes its check and keeps
serving every version it recorded; a tag is never moved or deleted.

## 1. Choose the version

Compare with the last release tag (`git describe --tags --abbrev=0`):

- **major:** an artifact removed or renamed, or a breaking change to one;
- **minor:** an artifact added, or changed compatibly;
- **patch:** fixes only.

## 2. Update the files

- `quiver-pack.yaml`: `version: X.Y.Z`.
- `CHANGELOG.md`: a new top entry `## X.Y.Z (YYYY-MM-DD)`, dated today, listing what changed for the reader.
- `README.md`: the artifact table's versions match the artifacts' `quiver.yaml`.

Commit these as one change (`chore(release): X.Y.Z`) through the forge's normal review.

## 3. Check with the tag

```bash
uvx --from git+https://github.com/agent-quiver/quiver-check@<commit> quiver-check . --tag vX.Y.Z
```

It confirms the tag equals the version and the changelog entry is dated. Fix every finding before tagging.

## 4. Protect release tags (once per repository)

- **GitHub:** a tag ruleset on `refs/tags/v*` with "Restrict updates" and "Restrict deletions" (Settings →
  Rules → Rulesets). A private repository on GitHub Free has no rulesets; Quiver then serves its tags as they are
  and keeps the first copy of each version.
- **GitLab:** Settings → Repository → Protected tags, `v*`, allowed to create: Maintainers.

## 5. Tag and push

```bash
git tag -a vX.Y.Z -m "<pack title> X.Y.Z"
git push origin vX.Y.Z
```

The forge's check runs on the tag. When it passes, Quiver picks the release up on the next call (a first call may
answer that the pack is being prepared; retry after a few seconds).

## 6. Verify

Ask the agent connected to the pack to run `whoami`: it shows the pack version and commit. Tell the person the
version is live and what changed.
