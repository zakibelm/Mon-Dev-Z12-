# SOURCE_MANIFEST — sources intégrées (M0)

Date de relevé : 25 novembre 2026.

| | Claudex Loop | Assistant Frontend |
|---|---|---|
| Dépôt | https://github.com/chaseai-yt/claudex-loop | https://github.com/zakibelm/Assistant-frontend- |
| Visibilité | public | **privé** |
| Branche relevée | `main` | `ccr-9b5832cc-g65xj5` (branche par défaut du dépôt) |
| SHA exact | `53cddc42e39346fb8c6d5d612281a3b1add14e66` (2026-10-14) | `728aaf9d24378f5aebba3f81c523dd41f01657c1` (2026-11-21) |
| Licence | MIT (© 2026 Chase AI) | Dépôt sans fichier LICENSE propre ; `LICENCES.md` liste les licences des skills (voir ci-dessous) |
| Mode d'intégration | **Copie** dans `vendor/claudex-loop/` (sans historique git) | **Sous-module** `vendor/assistant-frontend` épinglé au SHA ci-dessus |
| Pourquoi ce mode | Public + MIT : copie autorisée, auditable dans ce dépôt | Dépôt privé, ce dépôt est public : copier les fichiers exposerait le code. Le sous-module n'expose que l'URL et le SHA |

## Licences à respecter (Assistant Frontend, d'après son `LICENCES.md`)

| Skill | Licence | Obligation |
|---|---|---|
| Hallmark, Motion design, Web Interface Guidelines | MIT | Garder copyright et licence |
| Impeccable, frontend-design | Apache 2.0 | Garder `LICENSE`/`NOTICE.md`, signaler les modifications |
| Unslop | CC BY 4.0 | Créditer Damir Sokolovsky (@heydamir) avec lien vers https://github.com/heydamir/unslop |
| Photos de Hallmark | Variable (CC0, CC BY, CC BY-SA…) | Créditer chaque photo utilisée |

**Action ouverte :** le dépôt Assistant-frontend- n'a pas de licence propre sur son code (outils, agents `expert-frontend`, skill `refonte`). Tant que c'est ton code personnel, aucun blocage ; à trancher si le projet est un jour distribué.

## Reproduire l'état exact

```bash
git clone --recurse-submodules https://github.com/zakibelm/Mon-Dev-Z12-.git
# ou, après un clone simple :
git submodule update --init   # exige un accès GitHub au dépôt privé (jeton ou clé de déploiement)
```

## Mettre à jour une source (jamais automatiquement)

1. Relever le nouveau SHA, lire le diff.
2. Audit décisionnel (cahier §3.1) avant de changer l'épinglage.
3. Mettre ce manifeste à jour dans le même commit.
