<!-- Généré par Amorce (brique : board). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Board de suivi

Board complet en 5 colonnes : chaque colonne a une règle d'entrée explicite, adossée à la DoR et à la DoD de l'équipe.

## Colonnes et règles de passage

| Colonne | Une carte y entre quand... |
| --- | --- |
| **Backlog** | toute idée ou story, même brute — rien n'y est engagé |
| **Ready** | la story remplit la Definition of Ready (voir `DOR_DOD.md`) |
| **En cours** | une personne est assignée et a réellement commencé (une seule carte par personne) |
| **En revue** | une Pull Request est ouverte et attend une relecture |
| **Fait** | la story remplit la Definition of Done (voir `DOR_DOD.md`) |

## Limite WIP (travail en cours)

Limite sur la colonne **En cours** : 1 carte par personne (pour une équipe de N membres : N cartes maximum dans « En cours »).

Pourquoi : plus il y a de cartes en cours en même temps, moins il y a de cartes terminées. Si tout le monde a déjà sa carte, on aide à finir une carte existante avant d'en tirer une nouvelle.

## Labels

| Label | Signification |
| --- | --- |
| `P1` | Indispensable pour la démo / la livraison — se fait en premier |
| `P2` | Important, mais la démo survit sans |
| `P3` | Si (et seulement si) il reste du temps |

## Le board est créé automatiquement

À la synchronisation, Amorce crée un board **GitHub Projects** lié au repo et y installe exactement ces colonnes : Backlog / Ready / En cours / En revue / Fait. L'écran « Statut de synchronisation » indique s'il a été créé, et sinon pourquoi.

Il reste trois choses à faire de votre côté :

1. Ouvrir le project (onglet **Projects** du repo) et l'épingler.
2. Activer les workflows intégrés du project : *Item added to project* → **Backlog**, *Pull request merged / Item closed* → **Fait**.
3. L'ouvrir à chaque standup — un board qu'on ne regarde pas ne sert à rien.

### Si le board n'a pas été créé

4. Cause la plus fréquente : le `GITHUB_TOKEN` d'Amorce n'a pas la permission **Projects: write** (scope `project` sur un token classique). Ajoutez-la et relancez la synchro.
5. Repli manuel : **Projects** → **New project** → modèle **Board**, puis renommez les colonnes pour obtenir Backlog / Ready / En cours / En revue / Fait et liez le project au repo.
