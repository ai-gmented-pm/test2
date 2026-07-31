<!-- Généré par Amorce (briques : conventions_git, revue_code). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Conventions Git

_Workflow par branches de feature, calibré pour un bootcamp de 2 semaines._

## Branches
- Une branche par tâche : `<type>/<entite>-<action>` — le type dit la nature du travail, l'entité dit sur quelle partie du projet il porte, l'action dit ce qui change.
- Jamais de push direct sur `main` — `main` doit rester déployable à tout moment.
- Pull Request obligatoire avant tout merge — c'est là que la revue de code se joue (voir la section revue).

### Nommage des branches
Une branche porte le nom de ce qu'elle change, pas celui de la personne qui la pousse.

Schéma imposé : `<type>/<entite>-<action>` — types autorisés : `feat`, `fix`, `chore`, `docs`, `refactor`, `test`.

Ces exemples sont des **gabarits** : le profil du projet ne déclare aucune entité, `<entite>` est donc un trou à remplir, pas un vrai scope.

| Branche | Ce qu'on y fait |
| --- | --- |
| `feat/<entite>-liste` | afficher la liste des <entite> |
| `feat/<entite>-creation` | créer un <entite> depuis le formulaire |
| `fix/<entite>-validation` | corriger la validation du formulaire <entite> |
| `refactor/<entite>-extraction` | extraire la logique <entite> dupliquée |

## Messages de commit
- Format Conventional Commits : `<type>(<scope>): <sujet>` — un format lisible par tous et par l'outillage.
- Types autorisés : `feat`, `fix`, `chore`, `docs`, `refactor`, `test` — choisir le type qui décrit l'intention du commit.
- Sujet : 72 caractères maximum, à l'infinitif, en minuscule, sans point final — au-delà, `git log --oneline` devient illisible et le commit fait probablement deux choses.

### Scopes autorisés
Le scope répond à « quelle partie du projet ce commit touche-t-il ? ». La liste ci-dessous est **dérivée des entités déclarées dans le profil du projet**, plus les scopes transverses qui n'appartiennent à aucune entité.

| Scope | Couvre |
| --- | --- |
| `<entite>` | tout ce qui touche l'entité <entite> : modèle, écrans, routes, tests |
| `ci` | workflow GitHub Actions, scripts de build, déploiement |
| `docs` | README, CONTRIBUTING, docs/ |
| `deps` | ajout ou montée de version d'une dépendance |
| `ui` | styles et composants partagés, sans entité précise |

Un commit qui n'entre dans aucun de ces scopes est presque toujours un commit fourre-tout : découpez-le. Un nouveau scope se décide en équipe et s'ajoute d'abord aux entités du profil, pas dans un coin du CONTRIBUTING.

### Exemples de messages (gabarits)
Ces exemples sont des **gabarits** : le profil du projet ne déclare aucune entité, `<entite>` est donc un trou à remplir, pas un vrai scope.

Lecture : le message dit ce que le commit **fait**, pas ce que vous avez touché. « corrige le bug » n'apprend rien ; « corrige la validation du formulaire » situe le problème et sa zone.

- `feat(<entite>): afficher la liste des <entite>`
- `feat(<entite>): créer un <entite> depuis le formulaire`
- `fix(<entite>): corriger la validation du formulaire <entite>`
- `refactor(<entite>): extraire la logique <entite> dupliquée`

> ⚠️ **Aucune entité n'est déclarée dans le profil du projet.** Les scopes de commit et
> les noms de branches ci-dessus sont donc des gabarits (`<entite>`), pas les
> vôtres. Ajoutez les entités du domaine (les objets que votre app manipule) dans le
> dashboard Amorce, puis régénérez cette brique : la liste des scopes autorisés et les
> exemples de branches et de commits seront alors ceux de votre projet.

# Revue de code

_Mode retenu : revue par Pull Request._

## Le circuit
- Toute PR est relue par **au moins 1 reviewer** avant merge — quatre yeux voient plus qu'une paire, surtout sous pression.
- Délai de réponse attendu : **sous 4h ouvrées** — une PR qui attend bloque son auteur et fait diverger `main`.
- On ne merge pas sans approbation — un « demande de changements » se traite avant tout nouveau sujet.

## Ce qu'Amorce configure sur le repo GitHub

Ces réglages sont appliqués automatiquement à chaque synchronisation depuis le tableau de bord — inutile de les repasser à la main.

- Visibilité du repo : **public**.
- Suppression automatique de la branche après merge : **activée**.
- Merge autorisé : **squash uniquement** (une story = un commit sur `main`).
- Branche `main` **protégée** : 1 approbation minimum, pas de push direct sur `main`.
- Passage de la CI en check obligatoire : **non activé par défaut** — exiger un check qui n'a jamais tourné bloquerait toutes les PR. Une fois la CI vue verte une première fois, activez-le dans *Settings → Branches → main → Require status checks* en cochant `lint` et `ci`.

## Adapter le mode
- Équipe de 2 ? Le pairing remplace avantageusement la PR : passez le mode sur « pairing » dans Amorce.
- Le mode se rediscute en rétro si les PR s'accumulent ou si la revue devient un goulot.
