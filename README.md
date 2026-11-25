# Mon-Dev-Z12-

Projet **claudex-fullstack-platform** — outil personnel de développement full-stack (alternative à Lovable) où Claude et Codex alternent exécuteur et auditeur, avec l'expertise d'Assistant Frontend.

**Statut :** GO M0 — NO-GO production tant que la qualification réelle (M1) n'est pas terminée.

## Contenu

| Chemin | Rôle |
|---|---|
| `docs/CAHIER_DES_CHARGES.md` | Cahier des charges v1.1 |
| `docs/SOURCE_MANIFEST.md` | Sources, SHA exacts, licences |
| `docs/INTEGRATION_MAP.md` | Capacités réutilisables et écarts |
| `docs/ARCHITECTURE.md`, `SECURITY.md`, `PLAN.md`, `DECISIONS.md`, `BENCHMARK.md` | Livrables M0 |
| `docs/PLAN-REVIEW-LOG.md`, `PROJECT_HANDOFF.md` | Revue et passation |
| `vendor/claudex-loop/` | [Claudex Loop](https://github.com/chaseai-yt/claudex-loop) (MIT), copie au SHA `53cddc4` |
| `vendor/assistant-frontend` | Sous-module vers [Assistant-frontend-](https://github.com/zakibelm/Assistant-frontend-) (privé), SHA `728aaf9` |

## Cloner

```bash
git clone --recurse-submodules https://github.com/zakibelm/Mon-Dev-Z12-.git
```

Le sous-module exige un accès GitHub au dépôt privé Assistant-frontend-.
