<!-- Généré par Amorce (brique : standup_slack). Modifiez-le depuis le tableau de bord de l'équipe : une édition manuelle ici sera écrasée au prochain push. -->

# Rappel de standup dans Slack

Le standup n'a pas besoin d'un humain qui pense à le lancer : un workflow
GitHub Actions (`.github/workflows/standup_reminder.yml`) poste le rappel dans **#projet**,
quotidienne, du lundi au vendredi, à 09:30 (heure de Paris).

Tant que le secret `SLACK_WEBHOOK_URL` n'est pas créé, le workflow tourne
mais ne poste rien (il pose un avertissement dans les logs plutôt que
d'échouer). Les quatre étapes ci-dessous prennent cinq minutes.

## Brancher le bot en 4 étapes

1. **Créer l'app Slack** — sur <https://api.slack.com/apps>, *Create New App*
   → *From scratch*. Nommez-la « Standup #projet » et choisissez le workspace
   de l'équipe.
2. **Activer le webhook entrant** — dans l'app, menu *Incoming Webhooks* →
   bouton *Activate Incoming Webhooks* sur **On** → *Add New Webhook to
   Workspace* → choisissez le channel **#projet** → *Allow*. Copiez l'URL
   obtenue (elle commence par `https://hooks.slack.com/services/...`).
3. **Coller l'URL dans les secrets du repo** — sur GitHub :
   *Settings → Secrets and variables → Actions → New repository secret*.
   Nom exact : `SLACK_WEBHOOK_URL`. Valeur : l'URL copiée. *Add secret*.
4. **Vérifier** — onglet *Actions* du repo → workflow **Rappel de standup** →
   *Run workflow* (déclenchement manuel). Le message doit apparaître dans
   #projet dans la minute.

## Changer l'heure ou la cadence

Ne modifiez pas le `cron` à la main : le fichier est régénéré et écrasé au
prochain push depuis Amorce. Réglez plutôt les paramètres de la brique
« Rappel de standup » (channel, heure, fréquence) sur le tableau de bord,
puis relancez la synchronisation.

Deux points d'attention :

- GitHub Actions planifie **en UTC** et ignore les fuseaux. Amorce convertit
  depuis l'heure de Paris en heure d'hiver ; en été, le rappel tombe une
  heure plus tard qu'affiché.
- Les crons de GitHub Actions ne sont pas à la minute près : un retard de
  quelques minutes aux heures de pointe est normal.

## Pourquoi le webhook ne se colle pas dans Amorce

Un webhook entrant Slack est un secret porteur : quiconque l'a peut poster
dans #projet. Amorce ne le demande pas et ne le stocke nulle part, pour
une raison simple — Amorce n'appelle jamais Slack. C'est GitHub Actions,
depuis votre repo, qui poste le message. Faire transiter le secret par
Amorce ajouterait un dépositaire de plus sans rien apporter : un endroit de
plus à sécuriser, à auditer et à purger en cas de fuite.

Corollaire : c'est vous qui le révoquez (bouton *Revoke* dans l'app Slack)
et vous seuls. Si un membre quitte le projet, régénérez le webhook et
mettez à jour le secret du repo.

## Si rien ne se poste

| Symptôme | Cause probable |
| --- | --- |
| Log « Secret SLACK_WEBHOOK_URL absent » | L'étape 3 n'a pas été faite, ou le nom du secret n'est pas exactement `SLACK_WEBHOOK_URL`. |
| `curl` répond `no_service` ou `invalid_token` | Le webhook a été révoqué ou l'app désinstallée : refaites l'étape 2 et remplacez le secret. |
| Le workflow ne se déclenche jamais | GitHub désactive les workflows planifiés d'un repo **sans activité depuis 60 jours** : poussez un commit, ou relancez à la main. |
| Le message tombe une heure trop tard | Heure d'été (voir plus haut). |
