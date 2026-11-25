# Cahier des charges — claudex-fullstack-platform

**Version :** 1.1 (v1 + addendum C01–C12 intégré)
**Date :** 25 novembre 2026
**Statut :** GO M0 — NO-GO production tant que la qualification réelle n'est pas terminée

## 0. Documents et précédence

- `docs/PLAN_DIRECTEUR.md` : référence technique et opérationnelle (architecture, lots M0–M8, contrats, prompt maître).
- Ce cahier : alignement fonctionnel. En cas de contradiction, ce cahier v1.1 prévaut sur le plan directeur pour le fonctionnel et le déploiement initial.
- `docs/ADDENDUM_V1.1.md` : texte source des corrections C01–C12 (détail et critères d'acceptation).
- `docs/reviews/` : évaluations indépendantes (8,7/10 sur la v1).

Contradictions résolues :

| Sujet | Plan directeur / v1 | Résolution v1.1 |
|---|---|---|
| Déploiement initial | Studio sur Vercel, moteur sur VPS | MVP tout sur le VPS ; Vercel après qualification (C06) |
| Moment de l'audit | Fin de phase seulement | Double audit : décisionnel avant, exécution après (C01) |
| Benchmark | 3 configurations | 4 configurations : Claude seul, Codex seul, Claudex sans AF, Claudex avec AF (C12) |
| Rôles | Deux configurations fixes | 4 modes dont automatique, par défaut (C04) |
| Identification des rôles | Couleur seule | Couleur + libellé explicite (C10) |

## 1. Objectif

Outil personnel de développement full-stack, alternative à Lovable, accessible depuis un navigateur (tablette comprise). Zaki décrit une application ; Claude et Codex la construisent en alternant exécuteur et auditeur, avec l'expertise d'Assistant Frontend. Une seule interface remplace le va-et-vient manuel entre Claude et ChatGPT. Aucune clé API.

## 2. Décisions d'alignement

| # | Décision |
|---|---|
| A1 | Abonnements uniquement : Claude Pro/Max via Claude Code, ChatGPT Plus via Codex CLI. Aucune clé API, aucun basculement payant automatique, aucun contournement. Usage autorisé à vérifier avant toute intégration définitive (`BLOCKED_SUBSCRIPTION_COMPLIANCE` sinon). |
| A2 | Approche classique : dépôt GitHub + moteur + interface web. Pas de dépendance à « Install as app » (Mac/Windows seulement). |
| A3 | MVP : tout sur le VPS (Studio, API, Claudex, CLI, Assistant Frontend, sandboxes, preview, persistance) derrière un reverse proxy sécurisé. Évolution : Studio sur Vercel, le reste sur le VPS, seulement si la séparation apporte un bénéfice démontré. |
| A4 | Accessible partout par navigateur. |
| A5 | Connecteurs : ne pas reconstruire. Inventorier et tester ce que Claude Code et Codex atteignent réellement depuis le VPS (GitHub, Drive, Supabase, Vercel, MCP). Registre : connecteur, fournisseur compatible, état, permissions, capacités, restrictions, résultat du test réel. Les connecteurs des versions web ne sont pas supposés disponibles dans les CLI. |

## 3. Collaboration Claude–Codex

### 3.1 Double audit (C01)

- **Audit décisionnel, avant exécution :** besoin, architecture, propositions d'Assistant Frontend, directions artistiques, composants et skills importants, modèle de données, contrats API, choix technologiques, sécurité. Issue : retenir, améliorer, remplacer ou rejeter, avec justification documentée.
- **Audit d'exécution, après réalisation :** planification, frontend, backend, intégration, tests, livraison. Pas d'audit sur les opérations mineures ou répétitives.
- **Critère :** une proposition d'Assistant Frontend est contestée et améliorée avant le début du développement.

### 3.2 Attribution des rôles (C04)

Sélecteur dans le Studio :

1. **Automatique, par défaut** (nature de la tâche, compétences, disponibilité, benchmarks, quotas ; aucun modèle supposé supérieur sans preuve) ;
2. Claude exécute / Codex audite ;
3. Codex exécute / Claude audite ;
4. Alternance par phase.

Règles : aucun modèle ne valide son propre travail ; changement de rôle visible dans le fil et journalisé ; approbation liée à la version exacte inspectée ; un seul exécuteur écrit dans un workspace à la fois.

### 3.3 Assistant Frontend (C05)

Réutilisation réelle de ses capacités (orchestrateur, skills, outils, directions artistiques, templates, composants, design systems, animations, méthodes de refonte), sans le réduire à des prompts. Les trois parcours restent disponibles et passent par le même mécanisme contradictoire :

1. Bibliothèque guidée ;
2. Demande directe ;
3. Expert frontend / carte blanche.

### 3.4 EVV proportionné (C09)

- **Critique (bloque la conformité) :** faille de sécurité critique, secrets exposés, perte de données, fonctionnalité essentielle inutilisable, échec critique de build, violation de permissions.
- **Significatif :** présenté avec conséquences et recommandation ; Zaki corrige ou accepte un compromis documenté (jamais si une règle de sécurité est violée).
- **Mineur :** présenté sans bloquer la livraison.
- **Débats :** 3 cycles max (décision normale), 5 (structurante), arrêt anticipé si solution satisfaisante ; seuils configurables, qualifiés par tests. Désaccord persistant → Zaki, avec alternatives, risques et recommandation. L'accord des deux modèles n'est jamais une preuve de fonctionnement.

## 4. Interface (Studio)

1. Fil unique à trois : Zaki, exécuteur, auditeur. Zaki intervient quand il veut.
2. Rôles : fond de bulle selon le rôle (exécuteur bleu nuit, auditeur ambre/brun sombre) + libellé explicite (« Claude · exécuteur ») ; nom du modèle discret. Les couleurs suivent le rôle lors des inversions.
3. Lisibilité : fonds sombres et doux, texte clair, contraste WCAG AA, jamais clair sur clair.
4. Épuré : par défaut, proposition retenue, objections importantes, corrections, décisions, progression réelle, résultats de vérification ; détails techniques à la demande. Jamais de raisonnements internes privés ni d'échanges simulés.
5. Preview en sandbox, agrandissable ; sélecteur mobile / tablette / bureau ; bascule Preview / Code (fichiers, changements récents).
6. Menu : historique des sessions avec reprise ; connecteurs ; paramètres des modèles ; configuration des rôles ; bibliothèque frontend facultative ; sidebar rétractable.
7. Contrôles : suspendre, reprendre, annuler ; restauration de checkpoint ; export du code ; suivi des phases.
8. Suivi des abonnements (si les données sont réellement exposées par les CLI, sinon « inconnu ») : état de connexion Claude et Codex, modèles, disponibilité, quotas, nombre de cycles d'audit, durée, motif d'interruption.

## 5. Sécurité (C02)

- Le Studio ne parle jamais directement aux terminaux, CLI ou identifiants : il passe par une API sécurisée (authentification du propriétaire, HTTPS, sessions, permissions, validation, journal des actions sensibles, limites de ressources, protection contre l'injection de commandes).
- Trois environnements séparés : (1) orchestration Claudex ; (2) environnement authentifié des CLI Claude et Codex ; (3) sandboxes des applications générées.
- Une application générée n'accède jamais aux identifiants des CLI, aux secrets du VPS, aux autres projets ni à l'hôte. La preview est isolée de l'origine web du Studio.
- **Critère :** une application générée malveillante ne récupère aucun identifiant, n'atteint aucun autre projet, ne contrôle pas le VPS.

## 6. Quotas, interruptions, persistance

| Situation | Action |
|---|---|
| Quota Claude ou Codex atteint | Sauvegarder et suspendre les tâches concernées |
| Authentification expirée | Demander une reconnexion |
| CLI indisponible | Workflow en attente |
| VPS interrompu | Reprise au dernier checkpoint valide |
| Audit indisponible | Livrable non déclaré validé |
| Usage non autorisé | Blocage signalé, sans contournement |
| Risque de facturation supplémentaire | Appel non exécuté |

Le fil n'est pas la seule mémoire (C08) : cahier, contexte, décisions, propositions, audits, historique des rôles, versions Git, tests, artefacts, état des tâches, approbations, dernier checkpoint valide sont persistés. Reprise possible après fermeture du navigateur, changement d'appareil, redémarrage du VPS, interruption des CLI, épuisement des quotas — après vérification de l'état réel, sans rejouer une action externe incertaine.

## 7. Critères d'acceptation (C11)

Deux dépôts accessibles et versionnés ; deux CLI réellement authentifiées ; usage des abonnements autorisé et vérifié ; deux configurations de rôles testées ; audit décisionnel démontré sur une proposition frontend ; audit d'exécution démontré sur un livrable réel ; trois parcours frontend fonctionnels ; API et base de données réelles ; preview exécutable ; tests critiques réussis ; zéro défaut critique non résolu ; tests d'isolation négatifs réussis ; checkpoint réellement restauré ; export exploitable ; zéro facturation non autorisée. Les tests simulés servent au développement, jamais de preuve d'intégration.

## 8. Benchmark (C12)

Configurations : **A** Claude Code seul ; **B** Codex seul ; **C** Claudex sans Assistant Frontend ; **D** Claudex avec Assistant Frontend. Mêmes briefs et critères ; seuils fixés avant les essais. Objectif : établir si le mécanisme contradictoire justifie les cycles supplémentaires.

## 9. Lancement de M0

**Étapes :** accès aux deux dépôts, SHA exacts, licences, inventaire des capacités réelles, interfaces et dépendances, conditions d'usage des abonnements, mécanismes de collaboration réellement présents dans Claudex, capacités réutilisables d'Assistant Frontend, architecture d'intégration minimale, risques, documents, revue contradictoire indépendante si les outils le permettent.

**Livrables :** `SOURCE_MANIFEST.md`, `INTEGRATION_MAP.md`, `ARCHITECTURE.md`, `PLAN.md`, `DECISIONS.md`, `SECURITY.md`, `PLAN-REVIEW-LOG.md`, `BENCHMARK.md`, `PROJECT_HANDOFF.md`.

**Blocages :** `BLOCKED_SOURCE_ACCESS` (source inaccessible), `BLOCKED_SUBSCRIPTION_COMPLIANCE` (usage non autorisé). Aucune substitution, aucune implémentation prématurée, aucun push distant ni déploiement sans autorisation. Le cahier n'est plus révisé sur papier : les prochaines décisions se fondent sur les résultats réels de M0.

## 10. Points encore ouverts

- Accès réel à Assistant-frontend- (M0).
- Authentification de Codex avec ChatGPT Plus sur le VPS, et conformité d'usage (M0–M1).
- Stack définitive du Studio (après audit des deux dépôts).
