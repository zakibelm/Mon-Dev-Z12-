# DECISIONS — journal des décisions

Format : décision, justification, statut. Les décisions A1–A5 et C01–C12 du cahier ne sont pas rejouées ici.

| # | Décision | Justification | Statut |
|---|---|---|---|
| D1 | Claudex Loop copié dans `vendor/claudex-loop/` au SHA `53cddc4` | Public, MIT, auditable ici, relevé exact | Acté |
| D2 | Assistant Frontend lié en **sous-module** (SHA `728aaf9`), non copié | Dépôt privé ; ce dépôt est public. Copier le code l'exposerait | Acté. Réversible : si ce dépôt devient privé, copie possible sur demande |
| D3 | Cahier dans `docs/CAHIER_DES_CHARGES.md` | Chemin référencé par le cahier lui-même | Acté |
| D4 | Pas de modification des sources vendorisées | Garder la traçabilité au SHA ; toute extension vit hors de `vendor/` | Acté |
| D5 | Écart réel identifié : aucun second modèle ne conteste les directions frontend | Dans l'Assistant Frontend, seul l'humain valide ; le cahier (C01) exige un audit décisionnel avant développement | À résoudre en M3 |
| D6 | Stack du Studio et de l'API | Point ouvert du cahier ; décision après audit réel des deux dépôts | **Ouvert** : décider en M1 par test, pas par préférence |
| D7 | Conformité d'usage des abonnements (Claude Pro/Max et ChatGPT Plus pilotés depuis une interface web sur VPS) | Non vérifiée : la documentation de Claudex Loop décrit l'usage des CLI en connexion officielle, mais ne couvre pas un usage via une interface tierce | **Ouvert** : `BLOCKED_SUBSCRIPTION_COMPLIANCE` tant que non vérifié (M1) |
