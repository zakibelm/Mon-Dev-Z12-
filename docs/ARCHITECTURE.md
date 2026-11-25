# ARCHITECTURE — intégration minimale (M0, hypothèse à qualifier en M1)

Statut : **proposition**. La stack définitive du Studio reste un point ouvert du cahier (§10) ; ce document fixe uniquement la découpe et les frontières de sécurité, pas le framework.

## Vue d'ensemble (MVP : tout sur le VPS, cahier A3)

```
Navigateur (tablette, téléphone, bureau)
        │ HTTPS
        ▼
 Reverse proxy ──► Studio (interface web)               [env. 1 : orchestration]
        │
        └──────► API Claudex (authentification propriétaire, sessions,
                 permissions, journal, limites, file de tâches, persistance)
                        │  file locale (jamais d'accès terminal depuis le Studio)
                        ▼
        Exécuteur de CLI : Claude Code, Codex via runner.py   [env. 2 : identifiants CLI]
                        │  écrit dans un workspace par projet (un seul exécuteur à la fois)
                        ▼
        Sandbox d'application générée + preview               [env. 3 : sans secrets]
        (origine web distincte du Studio, ex. sous-domaine dédié)
```

## Les trois environnements (C02)

| Environnement | Contient | Ne doit jamais |
|---|---|---|
| 1. Orchestration | Studio, API, base de données, journal | Lire les identifiants des CLI |
| 2. CLI authentifiées | Sessions de connexion Claude et Codex, `runner.py`, agents | Être monté dans une sandbox ou exposé au Studio |
| 3. Sandboxes | Code généré, `npm run ci` de l'Assistant Frontend, preview | Joindre l'hôte, d'autres projets, les secrets du VPS, les identifiants CLI |

Mise en œuvre proposée : trois utilisateurs système distincts + conteneurs sans privilèges pour l'env. 3, sans réseau interne et avec limites CPU/mémoire/durée. À valider par les tests d'isolation négatifs (C11).

## Flux d'une tâche

1. Zaki décrit l'application dans le Studio → l'API crée la tâche et persiste le cahier du projet.
2. **Audit décisionnel** : revue du plan (et des directions frontend) par le fournisseur non exécuteur, via Claudex Loop. Issue : retenir / améliorer / remplacer / rejeter, avec justification.
3. **Exécution** par l'exécuteur choisi (mode de rôles) ; commits par passe sur une branche de projet.
4. **Vérification** en sandbox : tests du projet et contrôles de l'Assistant Frontend (`ci`, `seuils`, `accessibilite`).
5. **Audit d'exécution** par l'autre fournisseur ; défauts classés critique / significatif / mineur (C09).
6. Checkpoint à chaque étape validée ; livraison = branche Git + export.

## Règles transverses

- Un seul exécuteur écrit dans un workspace à la fois ; aucun modèle ne valide son propre travail.
- Approbation liée au SHA exact inspecté (même principe que `approbations/` de l'Assistant Frontend).
- Quota atteint, authentification expirée ou audit indisponible → états du tableau §6 du cahier ; jamais de repli vers une API payante.
- Interfaces entre blocs derrière une couche d'abstraction (fournisseur de modèle, exécuteur de sandbox, stockage), pour rester interchangeables.

## À trancher en M1 (voir `DECISIONS.md`)

Langage/framework du Studio et de l'API, moteur de base de données, technologie de sandbox, mécanisme de checkpoint.
