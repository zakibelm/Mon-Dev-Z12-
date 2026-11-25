# BENCHMARK — protocole (C12)

Objectif : établir si le mécanisme contradictoire justifie les cycles supplémentaires.

## Configurations

| | Configuration | Exécuteur | Audit |
|---|---|---|---|
| A | Claude Code seul | Claude | Aucun |
| B | Codex seul | Codex | Aucun |
| C | Claudex sans Assistant Frontend | Claude ou Codex | Autre fournisseur (Claudex Loop) |
| D | Claudex avec Assistant Frontend | Claude ou Codex | Autre fournisseur + expertise et contrôles de l'Assistant Frontend |

## Briefs (mêmes pour A–D)

1. Application CRUD avec base de données et authentification.
2. Tableau de bord avec données réelles et graphiques.
3. Refonte d'une interface existante (le brief d'exemple `demo` de l'Assistant Frontend peut servir de base).

## Mesures

Build réussi, tests critiques réussis, défauts critiques/significatifs/mineurs (grille C09), notes Lighthouse et violations WCAG 2.2 (outils de l'Assistant Frontend), nombre de cycles d'audit, durée, consommation de quota (si exposée), interventions humaines.

## Seuils

**À fixer par Zaki avant le premier essai** (exigence du cahier). Proposition de départ, non figée : D doit réduire les défauts significatifs d'au moins un tiers par rapport à A et B pour justifier une durée plus longue ; sinon, privilégier A ou B pour ce type de tâche.

## Règles

Mêmes briefs, mêmes critères, même évaluateur ; résultats bruts conservés ; les tests simulés ne comptent pas.
