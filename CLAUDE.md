# ThreadPod — Conventions Claude Code

## Langue & nommage
- Tout en français : commits, issues, wiki, réponses.
- Société = ThreadPod / firmware = ThreadPod OS. « Jarvis » est banni.

## Git
- Commits descriptifs en français.
- Branches `claude/YYYY-MM-DD-slug` ; merge en **squash** ; suppression de la branche (locale + distante) après merge.
- Push direct sur `main`/`master` réservé aux corrections triviales et au wiki.

## Visuels
- JAMAIS de schéma ASCII. SVG obligatoire partout (réponses et wiki).
- Fichiers `.svg` commités, fond blanc `#ffffff`, police Segoe UI, dark mode via media query CSS.

## Routing des issues
- firmware / infra → `dev` · business / ops → `internal` · code Hub MCP → `tools` · OTA public → `firmware-ota`.

## Wiki
- Dès que tu modifies le wiki de ce repo, applique la doctrine du `CLAUDE.md` du wiki.
- Rappels : reflète l'état présent uniquement · footer obligatoire sur chaque page · SVG only · pages `Research-*` éphémères et hors `_Sidebar`.

## Définition de « Terminé » — clôture systématique de chaque issue
À la fin de TOUTE issue, sans demande explicite :
- Terminer entièrement le travail (aucun TODO laissé en suspens).
- Merger en squash sur `main`/`master`, puis supprimer la branche `claude/*` (locale + distante).
- Commits descriptifs en français.
- Clôturer l'issue traitée.
- Documenter le travail dans le code, ET dans le wiki si le changement le justifie (footer obligatoire : ``_YYYY-MM-DD — commit `abc1234`_``).
- Identifier les autres issues impactées par ce travail et y poster un commentaire.

## Spécifique firmware-ota
- Repo PUBLIC (distribution OTA + GitHub Pages).
- Binaires firmware volumineux → GitHub Releases, pas dans le repo.
- Public : ne jamais committer de clés, secrets ou information sensible.
