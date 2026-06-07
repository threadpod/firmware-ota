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

## Issues STOP & autorisations
Par défaut, une issue contenant une section **STOP** s'arrête à l'**ouverture de la PR** : NE PAS merger, NE PAS clore l'issue, NE PAS déployer, NE PAS créer/modifier de **ressource d'organisation** (webhook, ruleset, secret, team, repo, bucket lock).

Ces gestes sont **réservés à Nicolas** — **SAUF** si le prompt de lancement (ou un message explicite de Nicolas) autorise nommément à aller au-delà (ex. « merge et clôture », « déploie », « fais tout ce que tu peux à ma place »). L'autorisation explicite **lève le STOP pour les gestes nommés**.

En cas de doute sur l'étendue de l'autorisation : **s'arrêter et demander**, ne jamais présumer.

Cette règle **prime sur** la « Définition de Terminé » ci-dessus : sur une issue STOP, la clôture automatique (merge, suppression de branche, fermeture d'issue, déploiement, ressources d'org) n'a lieu **qu'avec** une autorisation explicite ; sinon, s'arrêter à la PR.

## Spécifique firmware-ota
- Repo PUBLIC (distribution OTA + GitHub Pages).
- Binaires firmware volumineux → GitHub Releases, pas dans le repo.
- Public : ne jamais committer de clés, secrets ou information sensible.
