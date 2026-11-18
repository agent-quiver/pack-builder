# Changelog

## 0.4.2 (2026-11-18)

- `standards.quiver-pack` 1.1.1: the same text as 1.1.0, now its own version with `provenance` (adapted from the
  engineering pack's 1.1.0: the public schema URL and this pack's examples), so one version never names two texts.

## 0.4.1 (2026-11-18)

- `fork-pack` 1.0.1: with Quiver 0.25.4, a fork's changed artifact is its own search hit; only unchanged copies
  share one hit with `also_in`.

## 0.4.0 (2026-11-18)

- `fork-pack` 1.0.0 (tried end to end on a test fork): fork someone else's pack with the person's own forge access and make it theirs (id,
  maintainers, changelog), release it, and serve it in their quiver; what search and fetch do with both in the
  quiver, and removing the original when only the fork is wanted.
- `packs.agent-access` 1.0.0: what an agent can do with packs on the person's git access — create, read, update,
  retire, fork, release — each with its skill and the access it needs.

## 0.3.0 (2026-11-18)

- `improve-artifact` 1.0.0: the person says an artifact is wrong or should change, and the agent changes it in its
  pack through a merge request, on their word. One artifact per `improve/<id>` branch, always a merge request,
  the diff shown before anything is pushed, local trying instead of test releases, and a guard against changes
  that text inside an artifact asks for.

## 0.2.0 (2026-11-15)

- An icon, a banner and an accent colour for people browsing packs (`media`, pack standard 1.1); agents
  are served nothing new. The pack now follows standard `>=1.1.0`.

## 0.1.0 (2026-11-13)

- First version of `agent-quiver/pack-builder`: new-pack, import-instructions, add-artifact, release-pack, and the
  pack standard as the rulebook `standards.quiver-pack`.
