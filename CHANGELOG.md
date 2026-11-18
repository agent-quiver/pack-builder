# Changelog

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
