<!-- Généré par Amorce (brique : environnements). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Environnements

_Trois environnements et une règle de promotion : rien n'arrive en prod sans être passé par staging._

## Les environnements
- **dev (local)** : la machine de chaque membre — lancement : `bin/dev` — chacun développe et teste chez soi avant de pousser.
- **staging** : copie de prod chez Render (web service + PostgreSQL managé), alimentée par `main` — on y valide dans des conditions réelles avant de promouvoir.
- **prod** : l'environnement des utilisateurs, promu depuis staging — personne n'y pousse directement.

## Promotion
- Le chemin est toujours le même : dev → staging → prod.
- On ne promeut en prod que ce qui a été vu et validé en staging.
- Qui promeut : n'importe quel membre, en l'annonçant sur le canal de l'équipe.

## Checklist de setup chez Render (web service + PostgreSQL managé)
- [ ] Créer le compte (ou l'équipe) chez l'hébergeur
- [ ] Créer le service applicatif depuis le repo GitHub (déploiement auto sur `main`)
- [ ] Provisionner les services managés nécessaires (base de données...)
- [ ] Renseigner les variables d'environnement — mécanisme du preset : Rails credentials (config/master.key hors Git) + variables d'environnement de l'hébergeur
- [ ] Créer l'environnement de staging (même config que prod, base séparée)
- [ ] Déclencher un premier déploiement et vérifier l'URL publique
- [ ] Noter les URLs dans le README

## Distribution des builds mobiles (dev)
- iOS : builds internes via TestFlight — inviter toute l'équipe + les testeurs en distribution interne.
- Android : APK interne partagé (ou piste interne Play Console) — un lien de téléchargement direct suffit pour tester vite.
- Un build de dev distribué par jour minimum — tester sur vrai téléphone révèle ce que le simulateur cache.
