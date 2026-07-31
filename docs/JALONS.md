<!-- Généré par Amorce (briques : jalons, priorisation). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Jalons

Jalons rétro-planifiés depuis la date de démo (2026-08-07) pour un format « Bootcamp 2 semaines » de 10 jours.

> ⚠️ **Planning compressé — décision d'équipe requise.** La démo est dans 7 jour(s) alors que le format en prévoit 10. Le rétro-planning ci-dessous est mécaniquement écrasé (certains jalons peuvent tomber dans le passé). Rien n'est tranché ici à votre place : l'équipe doit choisir entre couper du scope (recommandé) ou redistribuer les jalons sur le temps réellement disponible, puis ajuster les dates ci-dessous.

| Jalon | Date | Objectif |
| --- | --- | --- |
| **J1** | 2026-07-29 | Setup + squelette déployé *(repo, CI, une page en ligne)* |
| **J3** | 2026-07-31 | Premier flux déployé *(un premier parcours utilisateur complet, en ligne)* |
| **J5** | 2026-08-02 | Revue de mi-parcours *(point scope : ce qui reste tient-il dans le temps restant ?)* |
| **J8** | 2026-08-05 | Feature freeze *(plus aucune fonctionnalité nouvelle — uniquement bugs et finitions)* |
| **J9** | 2026-08-06 | Répétition de la démo *(dérouler la démo en conditions réelles, chronométrée)* |
| **J10** | 2026-08-07 | Démo |

## Comment lire ces jalons

- **Squelette déployé** : l'app est en ligne dès le début, même vide — déployer n'est plus jamais un risque de dernière minute.
- **Feature freeze** : à partir de ce jalon, on n'ajoute plus rien de nouveau ; on corrige, on peaufine, on prépare la démo.
- **Un jalon glisse ?** On coupe du scope, on ne décale pas la démo — voir la section Priorisation ci-dessous.

## Priorisation

**Méthode : matrice valeur / effort (2×2).** Chaque story est placée sur deux axes : valeur apportée (au projet, à la démo) et effort pour la livrer.

| | Effort faible | Effort fort |
| --- | --- | --- |
| **Valeur forte** | ✅ P1 — à faire d'abord | 🤔 P2 — découper avant d'attaquer |
| **Valeur faible** | 🎁 P3 — bouche-trou de fin | ❌ On ne fait pas |

Le placement se fait en équipe, à la louche et en quelques secondes par story : c'est un outil de conversation, pas une science.

### Charte de scope-cut

- **Qui coupe** : personne ne coupe seul — la décision suit la charte de décision de l'équipe (voir `CHARTE.md`).
- **Quand** : à chaque jalon qui glisse (voir les jalons ci-dessus). Un jalon raté déclenche une coupe de scope, jamais un décalage de la démo.
- **Comment** : on rétrograde des stories (P1 → P3), on ne les supprime pas — le backlog garde la trace de ce qui a été coupé.
