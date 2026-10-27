# Kora Discord Bot

Kora est un bot Discord communautaire écrit en TypeScript avec [discord.js](https://discord.js.org/) et SQLite (`better-sqlite3`). Il regroupe des outils de modération, des profils et niveaux, une économie virtuelle à collectionner et des outils d’accueil et de support.

> Kora est un projet indépendant, non affilié à Discord ou AniList. Les fonctionnalités de cartes utilisent l’API publique AniList.

## Fonctionnalités

- **Configuration de serveur** : `/setup` prépare les rôles, les salons de vérification, ModMail, honeypot, logs et salle des trophées ; `/config` permet de modifier plusieurs salons.
- **Sécurité et support** : captcha, attribution du rôle Membre après vérification, honeypot, formulaires ModMail, réclamation/libération/fermeture des tickets et journaux d’événements.
- **Modération** : `/clear`, `/warn`, `/ban`, `/unban`, `/kick`, `/infractions`, `/clear-warn` et `/server-info`.
- **Profils et activité** : `/profil`, niveaux écrits et vocaux, réputation, classements et commande `/anniversaire` avec liste, retrait et configuration du rôle d’anniversaire.
- **Cartes et économie** : `/carte` pour invoquer, collectionner, échanger, vendre, offrir et rechercher des personnages AniList. Les pièces sont virtuelles et sans valeur réelle.
- **Mini-jeux** : pierre-feuille-ciseaux et morpion.
- **Accueil** : message d’arrivée configuré avec `/welcome-config`.

Les commandes slash sont chargées depuis `src/commands/`. Les événements Discord sont chargés depuis `events/`. Les données persistantes sont enregistrées dans `database/kora.sqlite`.

## Prérequis

- Node.js 20 ou une version LTS récente compatible avec les dépendances.
- npm.
- Une application et un bot créés dans le [portail développeur Discord](https://discord.com/developers/applications).

Active les intents **Server Members Intent**, **Presence Intent** et **Message Content Intent** dans le portail développeur. Le démarrage initial `/setup` demande au bot les permissions d’administrateur car il crée des rôles et configure plusieurs salons et permissions. Invite le bot seulement sur les serveurs que tu administres et vérifie sa hiérarchie de rôles.

## Installation

```bash
npm install
```

Copie `.env.example` vers `.env`, puis renseigne les valeurs :

```env
DISCORD_TOKEN=ton_token_de_bot
CLIENT_ID=identifiant_de_ton_application
GUILD_ID=identifiant_du_serveur_de_test
SUPPORT_GUILD_ID=identifiant_du_serveur_support
```

`GUILD_ID` est facultatif : s’il est défini, les commandes sont déployées sur ce serveur pour les tests. Sans cette variable, elles sont déployées globalement. `SUPPORT_GUILD_ID` est facultatif et limite le formulaire de signalement de bug au serveur support configuré.

**Ne publie jamais `.env`, le jeton du bot ou `database/kora.sqlite`.** Ils sont exclus de Git par `.gitignore`. Si un jeton a été partagé, régénère-le immédiatement dans le portail développeur.

## Lancer le bot

Déploie les commandes slash, puis démarre le bot :

```bash
npm run deploy
npm run dev
```

Pour lancer sans surveillance de fichiers :

```bash
npm start
```

Dans Discord, exécute `/setup` avec un compte administrateur du serveur. Cette commande crée ou réutilise les rôles et salons configurés, y compris le salon privé de logs. Configure ensuite les salons de bienvenue ou autres options avec les commandes dédiées.

Pour vérifier les types TypeScript :

```bash
npm run typecheck
```

## Base de données et sauvegardes

Kora crée le dossier `database/` et le fichier `database/kora.sqlite` au démarrage des modules de données. Arrête le bot avant de copier ou restaurer la base afin d’éviter une sauvegarde incohérente. Protége les sauvegardes comme des données personnelles : elles contiennent notamment des identifiants Discord, des statistiques, anniversaires, cas de modération et données de collection. Définis une durée de conservation, limite l’accès aux sauvegardes et supprime-les lorsqu’elles ne sont plus nécessaires.

## Documentation légale et liens Developer Portal

Avant de rendre l’application accessible à d’autres serveurs, complète et publie ces documents sur des URL HTTPS publiques, puis renseigne les URL dans la page de l’application du portail développeur Discord :

- [Conditions d’utilisation](CONDITIONS-UTILISATION.md)
- [Politique de confidentialité](POLITIQUE-CONFIDENTIALITE.md)

Les deux documents contiennent des champs `[À COMPLÉTER]`. Remplace-les par l’identité et les coordonnées réelles de l’exploitant, confirme les prestataires et les durées de conservation, puis vérifie le texte selon les lois applicables. Le README et les fichiers du dépôt seuls ne créent pas une page publique dans le Developer Portal.

## AniList

Les commandes de cartes interrogent l’API GraphQL publique AniList : <https://graphql.anilist.co>. Kora n’est pas affilié à AniList. Respecte les [conditions d’utilisation de l’API](https://docs.anilist.co/guide/terms-of-use), notamment les restrictions sur la collecte massive et l’utilisation commerciale.

## Contributions et signalement

Les contributions et rapports de bogues sont les bienvenus. N’inclus jamais de jeton, de fichier `.env`, de sauvegarde SQLite, ni de données personnelles réelles dans une issue ou une pull request. Pour une demande d’accès ou de suppression de données, utilise le contact indiqué dans la [Politique de confidentialité](POLITIQUE-CONFIDENTIALITE.md), pas une issue publique.

## Licence

Aucune licence de redistribution n’est déclarée dans ce dépôt pour le moment. **[Ajoute un fichier `LICENSE` et indique le titulaire/droit de réutilisation avant d’accepter des contributions ou d’autoriser la redistribution.]**
