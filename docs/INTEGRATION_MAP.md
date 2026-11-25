# INTEGRATION_MAP — ce qui existe, ce qui manque

Inventaire fondé sur la lecture réelle des deux dépôts (SHA dans `SOURCE_MANIFEST.md`). « Existe » = présent dans le code ; rien n'a encore été exécuté de bout en bout (qualification réelle = M1).

## Capacités réutilisables

| Source | Capacité réelle | Réutilisation dans le Studio |
|---|---|---|
| Claudex Loop | Boucle : reconnaissance → exigences → `PLAN.md` → revue du plan par l'autre fournisseur → build → inspection finale par l'autre fournisseur | Moteur du double audit (C01) |
| Claudex Loop | `scripts/runner.py` (Python 3.10+, sans paquet pip) : exécute **un tour de CLI** ; l'hôte arbitre, journalise et borne les tours | Brique d'appel des CLI Claude et Codex derrière l'API |
| Claudex Loop | `builder=claude\|codex`, l'inspecteur est toujours l'autre fournisseur | Modes 2 et 3 du sélecteur de rôles (C04) |
| Claudex Loop | Verdicts `APPROVED` / `REVISE` / `BLOCKED`, budget de tours, `PLAN-REVIEW-LOG.md` (modèles demandés et observés, aucun repli silencieux) | Journal d'audit et plafonds de cycles (C09) |
| Claudex Loop | Revue en lecture seule (Claude : `Read,Glob,Grep` seulement, mode sûr compatible abonnement) | Base de la politique de permissions de l'auditeur |
| Claudex Loop | `claudex-route` : recommandation de modèle/rôle | Point de départ du mode Automatique (C04) |
| Assistant Frontend | Agent `expert-frontend` + 4 agents `impeccable-*` (relecteur, documentaire, producteur d'assets, applicateur) | Expertise frontend (C05) |
| Assistant Frontend | 8 skills : refonte, impeccable, hallmark, unslop, motion-design, motion-site, frontend-design, web-design-guidelines | Parcours « bibliothèque guidée » et « carte blanche » |
| Assistant Frontend | Deux points de validation (directions, puis variantes) + `approbations/` liées à une variante précise | Contrat d'approbation « liée à la version exacte » (C04) |
| Assistant Frontend | Contrôles mesurés : `logique`, `captures`, `lighthouse`, `accessibilite` (WCAG 2.2), `interactions`, `seuils`, `preuve`, `silhouettes`, `mouvement`, `ci` | Résultats de vérification affichés dans le fil ; critères des défauts critiques (C09) |
| Assistant Frontend | Séparation solution / travaux (`travaux/<nom>` par refonte) | Un projet généré = une branche ; export et checkpoint |

## Écarts : ce qui n'existe dans aucun des deux dépôts

| Besoin du cahier | État | Où ça se construit |
|---|---|---|
| Studio web (fil à trois, rôles colorés + libellé, preview, Code, menu) | À construire | M3–M4 |
| API sécurisée, authentification propriétaire, journal des actions sensibles | À construire | M2 |
| Sandboxes isolées + preview sur origine séparée | À construire | M2 |
| Mode de rôles **Automatique** et **alternance par phase** | À construire (Claudex Loop ne fournit que les deux modes fixes) | M3 |
| **Audit décisionnel d'une proposition frontend par Codex** | Écart réel : dans l'Assistant Frontend, c'est l'humain qui valide ; aucun second modèle ne conteste les directions | M3, via une revue Claudex Loop appliquée à `directions.html` avant le point de validation 1 |
| Classification EVV critique / significatif / mineur | À construire (Assistant Frontend a des seuils chiffrés, pas cette taxonomie) | M3 |
| Persistance, checkpoints restaurables, reprise après coupure (C08) | À construire | M2 |
| Suivi d'abonnement et de quotas | À vérifier : dépend de ce que les CLI exposent réellement | M1 |
| Registre de connecteurs testés (A5) | À construire après inventaire réel depuis le VPS | M1 |

## Points de contact techniques

- Claudex Loop : Python 3.10+, Claude Code et Codex installés et connectés (login officiel de chaque CLI, aucune clé API).
- Assistant Frontend : Node 22 (`.nvmrc`), Playwright/Chromium, `axe-core 4.14.1`, `lighthouse 13.6.0`, `playwright 1.65.1`.
- Les deux s'exécutent dans l'environnement n°2 (CLI authentifiées) ou n°3 (sandbox) défini dans `ARCHITECTURE.md`.
