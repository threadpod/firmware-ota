# ThreadPod OTA

Distribution des mises à jour firmware signées de ThreadPod OS. Un seul
binaire par classe de carte mère `tpc` (0.1, 0.2, 1.0), quelle que soit la
carte fille du module.

## Comment ça marche

Chaque module embarque un client OTA qui interroge le manifest de sa classe
de carte mère et de son channel actif, servi par GitHub Pages (branche
`gh-pages`) :

```
https://ota.threadpod.net/tpc/<rev>/<channel>.json
```

Exemples :
- `https://ota.threadpod.net/tpc/0.1/latest.json`
- `https://ota.threadpod.net/tpc/1.0/latest.json`

Si une version plus récente est disponible **et** que le module est dans la
fenêtre de rollout, il télécharge le binaire depuis la GitHub Release
correspondante (`tpc-<rev>-nightly` pour `latest`), vérifie SHA-256 puis **signature ECDSA P-256** avant
commutation de partition.

## Channels

| Channel | Usage |
| --- | --- |
| `stable` | Production. Aucune stable `tpc` n'est publiée à ce jour : `tpc/<rev>/stable.json` répond 404. |
| `latest` | Nightlies, release rolling `tpc-<rev>-nightly` (prerelease). |

## Format du manifest

```json
{
  "module":          "tpc",
  "hw_rev":          "0.2",
  "idf_major":       6,
  "channel":         "latest",
  "version":         "1.7.1798-202610251541",
  "build":           1798,
  "url":             "https://github.com/threadpod/firmware-ota/releases/download/tpc-0.2-nightly/tpc-0.2-idf6-ota.bin",
  "size":            2985408,
  "sha256":          "ae950cbf…",
  "sig_ecdsa_p256":  "66f7c4f5…",
  "min_version":     "1.0.0",
  "rollout_percent": 100,
  "notes":           "0a61dc3",
  "full_url":        "https://github.com/threadpod/firmware-ota/releases/download/tpc-0.2-nightly/tpc-0.2-idf6-full.bin"
}
```

## Signature & transparence

Les binaires sont signés par la clé privée détenue par ThreadPod SAS.
La **clé publique** correspondante est publiée ici pour vérification
indépendante : [`pubkey.pem`](pubkey.pem).

Empreinte SHA-256 de la clé publique (à comparer avec celle embarquée
dans le firmware) : voir [`pubkey.sha256`](pubkey.sha256).

## Sécurité

- Ce repo est **public** par conception : les binaires distribués sont
  destinés à être exécutés sur les modules ; la signature garantit
  l'authenticité.
- Flash Encryption + Secure Boot V2 sont activés sur les modules de
  production (eFuses), ce qui empêche un binaire légitime de tourner sur
  un module tiers.
- Une brèche de la clé privée nécessiterait une rotation coordonnée avec
  une version intermédiaire du firmware embarquant la nouvelle clé.

## Canary rollout

Le champ `rollout_percent` permet un déploiement progressif :

- Chaque module calcule un bucket stable (FNV-1a de son MAC WiFi, modulo 100).
- Seuls les modules dont le bucket est < `rollout_percent` installent.
- Procédure typique : 10 % → 50 % → 100 % sur 48 h.

## Licence

Les binaires sont sous licence ThreadPod. La clé publique et les manifests
sont sous CC-BY-SA 4.0.
