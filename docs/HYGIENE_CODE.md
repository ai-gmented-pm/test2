<!-- Généré par Amorce (brique : hygiene_code). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Hygiène de code

_Cinq règles du quotidien qui gardent le code lisible par toute l'équipe, du premier au dernier jour._

## Commentaires : le pourquoi, pas le quoi

Un commentaire explique une décision ou une contrainte ; un commentaire qui paraphrase le code est du bruit à supprimer.

Avant :

```ruby
# on ajoute 1 au score
score += 1
```

Après :

```ruby
# le règlement du concours plafonne le score à 100
score = [ score, 100 ].min
```

## Nommage intentionnel

Les noms disent l'intention, sans abréviations : `days_since_signup` plutôt que `d`.

Avant :

```ruby
d = (Date.today - u.s_on).to_i
```

Après :

```ruby
days_since_signup = (Date.today - user.signed_up_on).to_i
```

## Fonctions courtes, une responsabilité

Une fonction fait une chose ; si vous dites « et » en la décrivant, découpez-la.

Avant :

```ruby
def process(input)
  # 60 lignes : parse, valide, sauvegarde ET notifie
end
```

Après :

```ruby
def process(input)
  data = parse(input)
  validate!(data)
  save(data)
end
```

## Pas de code mort commité

Ni code commenté « au cas où », ni fonction inutilisée : on supprime, l'historique Git garde tout.

Avant :

```ruby
# def old_score_algo
#   ...
# end  # gardé au cas où
```

Après :

```ruby
# (supprimé : `git log` s'en souvient si besoin)
```

## TODO datés et nominatifs

Tout `TODO` porte un nom et une date ; un TODO anonyme ne sera jamais fait.

Avant :

```ruby
# TODO: améliorer plus tard
```

Après :

```ruby
# TODO(claire, 2026-02-10) : gérer le panier vide avant la démo
```

## Ces règles sont vérifiées automatiquement

Elles ne vivent pas que dans ce document : elles sont traduites en
configuration exécutable dans `.rubocop.yml`, à la racine du repo.

- **À chaque push et à chaque Pull Request**, le job `lint` du workflow
  `.github/workflows/ci.yml` exécute `bundle exec rubocop`. S'il trouve un
  écart, **la CI passe au rouge** — le contrôle bloque, il n'alerte pas
  seulement.
- **Sur les Pull Requests**, le job `revue_bot` fait tourner
  [reviewdog](https://github.com/reviewdog/reviewdog) avec
  `reporter: github-pr-review` : chaque écart devient un **commentaire de
  revue posé sur la ligne concernée**, comme le ferait un relecteur
  humain. Il ne bloque pas de son côté (`fail_level: none`) : il montre,
  le job `lint` sanctionne.
- En local, avant de pousser : `bundle exec rubocop`.

### Ajuster ou désactiver le bot

- **Assouplir une règle** : décochez-la dans Amorce (brique « Hygiène de
  code »). Elle disparaît de ce document *et* de `.rubocop.yml` au
  prochain push — les deux ne peuvent pas diverger.
- **Ne plus recevoir de commentaires sur les PR** : supprimez le job
  `revue_bot` de `.github/workflows/ci.yml`. Le job `lint` continue de
  bloquer.
- **Tout couper** (déconseillé) : décochez le step « Lint » dans la
  brique « Intégration continue ».
- Une exception ponctuelle et assumée se marque dans le code (`rubocop:disable`,
  `eslint-disable-next-line`, `# noqa`) **avec la raison en commentaire** —
  une exception sans raison est une règle qu'on a renoncé à tenir.
