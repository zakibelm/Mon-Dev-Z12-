# PROJECT_HANDOFF — état au 25 novembre 2026

**Statut : GO M0 terminé côté documents — NO-GO production.**

## Fait

- Dépôt public `zakibelm/Mon-Dev-Z12-` : cahier v1.1, README, 9 livrables M0.
- Claudex Loop copié dans `vendor/claudex-loop/` (SHA `53cddc4`, MIT).
- Assistant Frontend lié en sous-module `vendor/assistant-frontend` (SHA `728aaf9`, dépôt privé).

## Bloquants et alternatives

| Problème | Action | Bénéfice |
|---|---|---|
| Conformité d'usage des abonnements non vérifiée (`BLOCKED_SUBSCRIPTION_COMPLIANCE`) | M1 : lire les conditions Claude Pro/Max et ChatGPT Plus, tester un usage CLI sur le VPS | Décision documentée avant tout investissement dans le Studio |
| Codex non authentifié : pas de revue indépendante | Connecter Codex sur le VPS puis lancer la revue du plan (voir `PLAN-REVIEW-LOG.md`) | Plan contesté par un second modèle |
| Sous-module privé inaccessible sans jeton | Fournir une clé de déploiement ou un jeton en lecture seule sur le VPS ; ou rendre ce dépôt privé et copier le code | Clone complet reproductible |
| `PLAN_DIRECTEUR.md`, `ADDENDUM_V1.1.md`, `docs/reviews/` absents | Les ajouter à `docs/` | Documentation de référence complète |

## Prochaine action

M1 : installer et authentifier les deux CLI sur le VPS, puis exécuter une boucle Claudex Loop réelle sur un petit brief.

## Rappel du cahier

Aucune implémentation prématurée, aucun déploiement sans autorisation. Les prochaines décisions se fondent sur les résultats réels de M1.
