<!-- Généré par Amorce (brique : boilerplate). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Démarrer

Stack du projet : **rails monolithe** (Ruby). Le squelette de l'application est créé par le générateur du framework — Amorce ne le double pas. Ce document donne la commande exacte, l'arborescence attendue et les premiers fichiers à créer.

## Créer le projet

```bash
rails new . --database=postgresql --css=bootstrap
bundle install
bin/rails db:setup
bin/dev
```

Lancez la commande de création **dans le repo cloné** : les fichiers livrés par Amorce (`docs/`, `.gitignore`, `.editorconfig`) cohabitent avec ce que le générateur écrit. Vérifiez le `.gitignore` après coup — fusionnez plutôt que d'écraser.

## Arborescence

```
app/
├── assets/
│   ├── images/                 images du projet (logo, illustrations)
│   └── stylesheets/            un fichier par entité : articles.css
├── controllers/                articles_controller.rb
├── models/                     article.rb
├── javascript/                 contrôleurs Stimulus
└── views/
    ├── layouts/
    │   ├── application.html.erb   layout généré par Rails
    │   └── _meta.html.erb         partial fourni par Amorce (à rendre dans le <head>)
    └── articles/       index / show / _form / _article
config/routes.rb                resources :articles
db/                             migrations et seeds
spec/                           tests (RSpec)
public/                         servi tel quel : favicon.svg, og-image.png
```

L'entité **article** ci-dessus est un exemple : aucune entité n'est déclarée dans le profil du projet. Déclarez-les puis régénérez cette brique pour obtenir l'arborescence réelle.

## Ce qu'Amorce livre déjà

- `app/views/layouts/_meta.html.erb` — partial à rendre dans le `<head>` du layout : `<%= render "layouts/meta" %>`
- `.gitignore` — socle commun + entrées Ruby
- `.editorconfig` — indentation commune à tous les éditeurs

## Premiers fichiers à créer

- [ ] Lancer la commande de création ci-dessus et committer le squelette généré
- [ ] Brancher le squelette fourni par Amorce (`app/views/layouts/_meta.html.erb`)
- [ ] Renseigner le nom du projet dans la brique « Boilerplate » du dashboard Amorce
- [ ] Déposer l'image de partage `og-image.png` (1200×630) dans le dossier public
- [ ] Entité `article` : modèle, route `/articles`, vue liste, vue détail, styles
- [ ] Déclarer les entités du projet dans le profil puis régénérer cette brique
- [ ] Vérifier que `bin/dev` démarre chez tout le monde
