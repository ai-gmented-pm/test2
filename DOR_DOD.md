<!-- Généré par Amorce (briques : dor, dod). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

## Definition of Ready

Une story passe en **Ready** si (et seulement si) ces 5 critères sont remplis :

- [ ] Critères d'acceptation écrits et compris de toute l'équipe — *une liste vérifiable de « c'est bon si... » — pas une intention vague.*
- [ ] Persona ou utilisateur cible identifié — *on sait pour qui on développe, donc quoi simplifier en cas de doute.*
- [ ] Maquette ou wireframe lié (même sommaire) — *un croquis suffit — il évite de découvrir le design en codant.*
- [ ] Dépendances identifiées (techniques ou fonctionnelles) — *on sait ce qui doit exister avant (une autre story, une API, une donnée).*
- [ ] Taille estimée en t-shirt size (S/M/L) — *l'estimation sert à découper et à planifier, pas à s'engager au jour près.*

### Gabarit de story

> **En tant que** [persona], **je veux** [action], **afin de** [bénéfice].
> Critères d'acceptation : ... — Dépendances : ... — Taille : S/M/L

Aucune entité n'est renseignée dans le profil : ajoutez-les dans le dashboard Amorce puis régénérez cette brique pour obtenir un gabarit par entité.

## Definition of Done

Une story est **Fait** si (et seulement si) tous ces points sont vrais :

- [ ] Revue de code approuvée avant merge (1 reviewer minimum) — *quatre yeux voient les bugs que deux yeux ratent — même en vitesse.*
- [ ] CI verte : tous les tests (unitaires + système) passent — *un test qui passe aujourd'hui protège la démo de demain.*
- [ ] Déployé et vérifié sur l'environnement de staging — *« ça marche chez moi » ne compte pas — seul compte l'environnement partagé.*
- [ ] Pas de requête N+1 introduite, temps de réponse vérifié — *une page lente en local sera insupportable en production.*
- [ ] Responsive vérifié sur un vrai téléphone — *l'émulateur du navigateur ne remplace pas un vrai écran tactile.*
- [ ] 0 bug P1 connu sur le flux livré — *on peut livrer avec des bugs mineurs connus, jamais avec un P1.*
- [ ] Build mobile testé sur le flux livré (vrai appareil ou émulateur) — *le web qui marche ne garantit rien côté mobile.*

### Vérifications techniques (Ruby — tests RSpec, lint RuboCop)

Ces points sont propres à la techno du projet. Les commandes sont celles du preset de stack : si elles changent, elles changent ici aussi.

- [ ] `bundle exec rspec` vert sur le périmètre livré — *la commande de tests du projet, pas « ça marchait tout à l'heure ».*
- [ ] `bundle exec rubocop` sans erreur (RuboCop, `.rubocop.yml`) — *le linter tranche les débats de style à la place de l'équipe.*
- [ ] Migrations réversibles : `bin/rails db:rollback` puis `bin/rails db:migrate` repasse sans erreur — *une migration qu'on ne peut pas annuler bloque toute l'équipe le jour où elle casse.*
- [ ] Pas de requête N+1 introduite (vérifié dans les logs de dev ou avec Bullet) — *une boucle qui interroge la base à chaque tour tient en local, pas en démo.*
- [ ] Aucun `binding.pry` / `puts` de debug laissé dans le code — *un point d'arrêt oublié fige la production sans un mot d'explication.*
