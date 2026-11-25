# SECURITY — modèle de menaces (C02)

Format imposé : Problème → Action → Bénéfice.

| # | Problème | Action | Bénéfice |
|---|---|---|---|
| S1 | Une application générée malveillante pourrait lire les identifiants des CLI | Env. 2 (CLI) séparé de l'env. 3 (sandbox) : utilisateur système distinct, aucun montage partagé | Aucun identifiant récupérable depuis une sandbox |
| S2 | La preview s'exécute sur la même origine que le Studio et pourrait voler la session | Preview servie depuis une origine distincte (sous-domaine dédié), cookies du Studio non transmis | Le script d'une preview ne lit pas la session du Studio |
| S3 | Injection de commandes via la description d'application ou les noms de fichiers | L'API ne construit jamais de commande shell par concaténation ; arguments validés, liste blanche de commandes | Aucune exécution arbitraire depuis l'interface |
| S4 | Le Studio atteint directement les terminaux | Interdit : le Studio parle seulement à l'API ; l'API enfile des tâches ; seul l'exécuteur appelle les CLI | Surface d'attaque réduite à l'API |
| S5 | Le dépôt public expose le code privé d'Assistant Frontend | Sous-module, jamais de copie ; aucun fichier de `.claude/settings.local.json` ni jeton versionné | Code privé inaccessible depuis ce dépôt |
| S6 | Consommation hors abonnement (clé API, facturation supplémentaire) | Aucune clé API stockée ; appel non exécuté si un risque de facturation est détecté (cahier §6) | Zéro facturation non autorisée |
| S7 | Scripts tiers (skills, `npx`) exécutés pendant un build | Exécution en env. 3 uniquement, réseau restreint, versions figées (`package-lock.json`, `skills-lock.json`) | Une dépendance compromise reste confinée |
| S8 | Épuisement des ressources du VPS par une sandbox | Limites CPU, mémoire, durée, espace disque par sandbox | Le VPS reste disponible pour les autres projets |
| S9 | Action sensible sans trace | Journal des actions sensibles (connexion, changement de rôle, approbation, export) | Traçabilité et reprise après incident |

## Vérifications obligatoires avant production

- Tests d'isolation négatifs réels (une sandbox hostile ne lit aucun identifiant, n'atteint aucun autre projet, ne contrôle pas le VPS).
- Aucun secret dans l'historique Git de ce dépôt (balayage fait à M0 sur Assistant-frontend- : aucun motif de secret détecté dans les fichiers versionnés ; à refaire en CI).
