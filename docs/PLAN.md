# PLAN — lots après M0

Le `PLAN_DIRECTEUR.md` cité par le cahier (lots M0–M8) n'est pas dans ce dépôt ; ce plan reprend le découpage minimal nécessaire au cahier v1.1 et devra être réconcilié avec lui s'il est retrouvé.

| Lot | Objet | Sortie vérifiable |
|---|---|---|
| **M0** (fait, documentaire) | Sources intégrées, inventaire, architecture minimale, risques | Les 9 documents de `docs/` |
| **M1** Qualification réelle | Installer et authentifier Claude Code et Codex sur le VPS ; vérifier la conformité d'usage des abonnements ; inventorier les connecteurs atteignables ; exécuter une boucle Claudex Loop réelle ; mesurer ce que les CLI exposent (quotas, modèles) | Rapport de qualification ; levée ou maintien de `BLOCKED_SUBSCRIPTION_COMPLIANCE` |
| **M2** Socle sécurisé | API, authentification, trois environnements, sandbox, preview isolée, persistance, checkpoint | Tests d'isolation négatifs réussis ; checkpoint restauré |
| **M3** Collaboration | Sélecteur de 4 modes de rôles, double audit câblé, classification EVV, plafonds de cycles | Deux configurations de rôles testées ; audit décisionnel démontré sur une proposition frontend |
| **M4** Studio | Fil à trois, rôles colorés + libellé, preview/Code, menu, contrôles | Parcours complet depuis une tablette |
| **M5** Assistant Frontend | Les trois parcours (bibliothèque, demande directe, carte blanche) via le mécanisme contradictoire | Trois parcours fonctionnels |
| **M6** Benchmark | Quatre configurations A–D (`BENCHMARK.md`) | Résultats chiffrés, décision sur la valeur des cycles supplémentaires |
| **M7** Livraison | Export du code, suivi des phases, reprise multi-appareils | Export exploitable ; reprise après coupure |
| **M8** Vercel (facultatif) | Séparer le Studio seulement si un bénéfice est démontré (C06) | Mesure avant/après |

## Condition de passage en production

Tous les critères du §7 du cahier (C11), dont zéro défaut critique non résolu et zéro facturation non autorisée. Tant que M1 n'a pas eu lieu : **NO-GO production**.
