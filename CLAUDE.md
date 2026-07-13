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
- **Référencer une issue = toujours `repo#numéro`** (`internal#278`, `dev#341`), jamais `#278` seul : les numéros sont propres à chaque repo et se chevauchent (un `#278` existe sur `dev` ET sur `internal`). S'applique partout — commits, issues, PR, wiki, commentaires — et pour lancer Claude Code : `claude "issue internal#278"`.

## Wiki
- Dès que tu modifies le wiki de ce repo, applique la doctrine du `CLAUDE.md` du wiki.
- Rappels : reflète l'état présent uniquement · footer obligatoire sur chaque page · SVG only · pages `Research-*` éphémères et hors `_Sidebar`.
- **Wiki plat** : tout fichier (factures, PDF, SVG, PNG, JPG) **à la racine**, référencé par **nom nu** (`![alt](fichier.svg)`, `[PDF](fichier.pdf)`). **Jamais de sous-dossier** — un wiki GitHub est plat, un lien `dossier/x.pdf` est interprété comme une page wiki inexistante → 404 (cf. internal#278).

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

La PR s'ouvre **ready for review**, jamais en draft : le STOP tient au non-merge (réservé à Nicolas), pas à l'état draft — une PR draft n'est pas mergeable (405) et force un contournement fermer/recréer (internal#354).

Ces gestes sont **réservés à Nicolas** — **SAUF** si le prompt de lancement (ou un message explicite de Nicolas) autorise nommément à aller au-delà (ex. « merge et clôture », « déploie », « fais tout ce que tu peux à ma place »). L'autorisation explicite **lève le STOP pour les gestes nommés**.

En cas de doute sur l'étendue de l'autorisation : **s'arrêter et demander**, ne jamais présumer.

Cette règle **prime sur** la « Définition de Terminé » ci-dessus : sur une issue STOP, la clôture automatique (merge, suppression de branche, fermeture d'issue, déploiement, ressources d'org) n'a lieu **qu'avec** une autorisation explicite ; sinon, s'arrêter à la PR.

**Choix multiples sans recommandation** : face à plusieurs options viables (A/B/C…) sans recommandation claire, NE PAS trancher seul — **STOP**, présenter les options avec leurs trade-offs, et attendre le choix de Nicolas. S'il existe une recommandation explicite, l'appliquer et continuer sans demander. (Garde-fou important en mode `auto`, qui pousse sinon à poursuivre sans poser de question.)

## Spécifique firmware-ota
- Repo PUBLIC (distribution OTA + GitHub Pages).
- Binaires firmware volumineux → GitHub Releases, pas dans le repo.
- Public : ne jamais committer de clés, secrets ou information sensible.
