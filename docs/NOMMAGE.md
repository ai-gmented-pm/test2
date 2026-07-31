<!-- Généré par Amorce (brique : nommage). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Conventions de nommage

_Document de référence dérivé du preset de stack Ruby et aucune entité n'étant déclarée dans le profil, tout est décliné sur l'entité d'exemple **article**. Il se lit une fois et s'applique sans rediscuter : tout ce qui est écrit ici est déjà tranché._

## 1. CSS / UI

Convention CSS : **BEM** (`bloc__element--modifier`), déclinée par entité du projet.

Lecture : le **bloc** est le composant (`article-card`), l'**élément** en est une partie (`article-card__title`, double underscore), le **modificateur** en est une variante (`article-card--featured`, double tiret). Une classe = un rôle, pas de style posé sur des balises nues.

Chaque entité du projet a le **même jeu de blocs** : `card`, `form`, `list`, `item`, `badge`. Ne créez pas un sixième bloc pour une entité sans le créer pour les autres — et si un bloc ne sert pas pour une entité, ne l'écrivez simplement pas.

### Entité article

| Bloc | Éléments | Modificateurs |
| --- | --- | --- |
| `.article-card` | `.article-card__title`, `.article-card__image`, `.article-card__meta`, `.article-card__actions` | `.article-card--featured`, `.article-card--compact` |
| `.article-form` | `.article-form__field`, `.article-form__label`, `.article-form__error`, `.article-form__submit` | `.article-form--invalid`, `.article-form--loading` |
| `.article-list` | `.article-list__item`, `.article-list__empty-state`, `.article-list__pagination` | `.article-list--loading` |
| `.article-item` | `.article-item__label`, `.article-item__value`, `.article-item__action` | `.article-item--selected`, `.article-item--disabled` |
| `.article-badge` | `.article-badge__dot`, `.article-badge__label` | `.article-badge--draft`, `.article-badge--published`, `.article-badge--archived` |

## 2. Code (Ruby)

**Entité article**

| Aspect | Règle | Exemple sur `article` |
| --- | --- | --- |
| Fichiers | `snake_case.rb`, un fichier = une classe, rangé par rôle | `app/models/article.rb`, `app/controllers/articles_controller.rb` |
| Classes / modules | `CamelCase` — modèle au singulier, contrôleur au pluriel | `Article`, `ArticlesController`, `ArticlePolicy` |
| Méthodes | `snake_case` ; `?` pour un prédicat, `!` pour ce qui modifie ou lève | `article.published?`, `article.publish!`, `Article.recentes` |
| Variables | `snake_case`, pluriel pour une collection | `article`, `articles`, `articles_count` |
| Constantes | `SCREAMING_SNAKE_CASE`, dans la classe concernée | `Article::STATUTS`, `Article::PAR_PAGE` |
| Booléens | adjectif ou participe, jamais de préfixe `is_` | colonne `published` → `article.published?` |
| Vues et partiels | dossier au pluriel, partiel préfixé d'un underscore | `app/views/articles/index.html.erb`, `app/views/articles/_article.html.erb` |

## 3. Base de données

**Entité article**

| Aspect | Règle | Exemple sur `article` |
| --- | --- | --- |
| Tables | `snake_case` au **pluriel** | `articles` |
| Colonnes | `snake_case`, jamais préfixées du nom de la table | `title`, `published_at` |
| Clés étrangères | `<entite_au_singulier>_id`, portée par la table liée, avec contrainte en base | `add_reference :autres, :article, foreign_key: true` → colonne `article_id` |
| Index | nom généré par Rails, un index sur chaque clé étrangère | `index_autres_on_article_id` |
| Timestamps | `created_at` / `updated_at` sur toutes les tables | `t.timestamps` |
| Booléens | adjectif, `null: false` + valeur par défaut explicite | `t.boolean :published, null: false, default: false` |
| Tables de jointure | les deux tables au pluriel, par ordre alphabétique | `articles_autres` |

## 4. Routes et URLs

Les URL sont au pluriel, en minuscules, sans underscore et sans verbe : l'action est portée par le verbe HTTP, pas par le chemin.

**Entité article**

- Ressource REST : `resources :articles` → `/articles`, `/articles/:id`
- Formulaires : `/articles/new`, `/articles/:id/edit`
- Helpers de chemin : `articles_path`, `article_path(article)`, `new_article_path`
- Ressource imbriquée : une seule entité déclarée : pas de ressource imbriquée pour l'instant — on n'imbrique jamais au-delà d'un niveau.

## 5. Tests (RSpec)

Framework du preset : **RSpec** — la suite se lance avec `bundle exec rspec`. Un test mal nommé est un test que personne ne relit.

**Entité article**

| Aspect | Convention sur `article` |
| --- | --- |
| Fichiers | `spec/models/article_spec.rb`, `spec/requests/articles_spec.rb`, `spec/system/articles_spec.rb` — le chemin reflète celui du code testé |
| describe racine | la classe testée (`RSpec.describe Article do`) ; pour un test système, le parcours (`RSpec.describe "Parcours article" do`) |
| describe imbriqué | `describe "#publish!"` pour une méthode d'instance, `describe ".recentes"` pour une méthode de classe |
| it | une phrase de comportement, pas un nom de méthode : `it "refuse un article sans titre"` |
| context | toujours commencé par « quand » ou « avec » : `context "quand le article est publié"`  |

## 6. Conventions transverses

- Tables et routes au **pluriel** : `articles, /articles`.
- Variables (Ruby) : snake_case (`ma_variable`).
- Un nom dit ce que c'est, pas comment c'est codé : `recettes_publiees`, pas `arr_tmp2`.
- Pas d'abréviation maison : on écrit le mot en entier, sauf `id`, `url`, `api`.
- Le français reste dans l'interface et la documentation ; le code, lui, est en anglais — un seul mot par concept, jamais deux traductions du même terme.
- Une entité porte le même mot partout : table, classe, composant, route, branche et scope de commit. Si le mot change quelque part, c'est un bug de nommage.

> Aucune entité n'est renseignée dans le profil : l'entité **article** utilisée dans tout ce document est un exemple fictif. Ajoutez les entités du projet dans le dashboard Amorce puis régénérez cette brique pour obtenir la déclinaison réelle — blocs CSS, classes, tables, routes et tests seront alors nommés d'après votre domaine.
