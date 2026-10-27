# Politique de confidentialité — Kora

**Version de travail — champs et durées à valider avant publication**  
Date de mise à jour : 27 octobre 2026  
Responsable du traitement : **Kora Team**  
Adresse de contact pour les demandes relatives aux données : **[\Kora Support\]](https://discord.gg/XdzBPY3KgH)**  


> Cette politique décrit le comportement actuel du code Kora fourni. Elle ne remplace pas l’analyse du responsable du traitement. Avant de publier le lien dans le portail développeur Discord, complétez les champs ci-dessus, confirmez les durées de conservation et assurez-vous que le contact indiqué traite effectivement les demandes d’accès et d’effacement.

## 1. Qui est responsable ?

Le responsable du traitement des données gérées par l’instance Kora est **[IDENTITÉ DU PROPRIÉTAIRE / DE L’EXPLOITANT]** (« nous »). Discord traite également des données pour faire fonctionner sa plateforme, selon sa propre [Politique de confidentialité](https://discord.com/privacy). Kora est un bot indépendant ; il n’est ni exploité ni approuvé par Discord.

## 2. Données traitées

Selon les fonctions activées dans un serveur, Kora peut traiter les catégories suivantes :

- **Identifiants et informations de compte Discord :** identifiant d’utilisateur, identifiant de serveur, identifiants de salons et de rôles ; nom d’utilisateur, nom affiché et avatar peuvent être consultés ou affichés pour identifier un membre dans une réponse ou un journal.
- **Configuration du serveur :** identifiants des salons et rôles configurés pour la vérification, le ModMail, les logs, l’accueil, le honeypot, les rôles d’anniversaire et les statistiques.
- **Activité et statistiques :** nombre de messages, XP écrit, XP vocal, temps passé en vocal, réputation et horodatage nécessaire aux limites d’attribution. Kora ne stocke pas un enregistrement audio des conversations vocales. Il utilise les événements d’état vocal pour calculer une durée et publier les journaux de connexions/déconnexions si le salon de logs est configuré.
- **Anniversaires :** jour et mois fournis volontairement, identifiant Discord et informations nécessaires à l’attribution annuelle éventuelle d’un rôle. L’année de naissance n’est pas demandée par la commande `/anniversaire`.
- **Modération :** identifiants de la personne concernée et du modérateur, type d’action, motif et date pour les avertissements, expulsions et bannissements. Les actions peuvent aussi apparaître dans les journaux Discord et l’audit log du serveur.
- **ModMail et journaux du serveur :** catégorie du formulaire et réponses saisies dans les tickets ; événements d’arrivée/départ, changements de profil, de rôle, de salon ou de serveur ; contenu avant/après de messages édités et contenu disponible de messages supprimés. Ces informations sont publiées dans les salons Discord configurés et leur accès dépend des permissions du serveur. Le contenu des tickets et des logs est conservé dans Discord, pas dans la base SQLite de Kora.
- **Économie et cartes :** identifiants de serveur et d’utilisateur, solde virtuel, personnages obtenus, souhaits, échanges, prix, rareté, dates d’invocation et de récupération, ainsi que les noms, séries, favoris et URL d’images des personnages.
- **Données techniques :** journaux d’erreurs du processus peuvent contenir des identifiants et des informations d’événement nécessaires au diagnostic. Le jeton du bot est lu depuis la configuration locale et ne doit jamais être publié.

## 3. Finalités et bases de traitement

Les données sont utilisées pour faire fonctionner les commandes et fonctionnalités demandées par les administrateurs et les membres, maintenir les niveaux et collections, enregistrer les anniversaires choisis, exécuter les fonctions de modération et de sécurité, gérer les tickets, produire des journaux de serveur et diagnostiquer les erreurs.

Selon la fonction et le contexte, le responsable doit déterminer la base légale appropriée. Les fonctions demandées par un administrateur peuvent relever de l’intérêt légitime à gérer et sécuriser sa communauté ; le traitement d’une date d’anniversaire est facultatif et déclenché par le membre ; les obligations légales et la défense de droits peuvent justifier certaines conservations ciblées.

## 4. Sources et destinataires

Les données proviennent des interactions avec Kora, des événements des serveurs Discord où le bot est installé, des membres qui renseignent un formulaire ou une date d’anniversaire, et des administrateurs qui configurent le bot.

Kora utilise l’API GraphQL publique d’[AniList](https://docs.anilist.co/guide/terms-of-use) pour rechercher des personnages, séries, favoris et images. Les requêtes de recherche correspondantes et les données techniques des requêtes sont transmises à AniList ; les identifiants Discord des membres ne font pas partie des requêtes GraphQL d’après l’implémentation actuelle. Des données de catalogue et d’images peuvent être conservées en mémoire pour une durée limitée. Les cartes obtenues et les informations utiles à la collection sont conservées localement dans SQLite.

Les données peuvent être accessibles :

- à Discord, qui héberge les comptes, interactions, messages, salons et journaux du serveur selon ses propres conditions ;
- aux administrateurs et membres du personnel disposant des permissions sur les salons de tickets et de logs ;
- à l’exploitant de l’hébergement du bot et aux personnes autorisées à administrer son environnement, si un hébergeur tiers est utilisé ;
- à AniList pour les requêtes de recherche de personnages et le chargement de leurs images.

Nous ne vendons pas les données personnelles et ne les utilisons pas pour la publicité. Les transferts internationaux éventuels dépendent de Discord, AniList et de l’emplacement réel de l’hébergement. ;

## 5. Conservation

La base SQLite `database/kora.sqlite` est enregistrée dans le répertoire de l’instance du bot. Dans la version actuelle, les tables de statistiques, d’anniversaires, de modération, de tickets et de collections ne disposent pas toutes d’une purge automatique. Quitter un serveur ne supprime donc pas automatiquement toutes les données liées à ce serveur.

- Les statistiques, données de collection, souhaits, échanges et historiques restent dans la base tant qu’ils ne sont pas supprimés par une opération de maintenance ou à la suite d’une demande recevable.
- Les anniversaires restent enregistrés jusqu’à leur retrait avec `/anniversaire retirer`, une demande d’effacement recevable ou la suppression de la base concernée.
- Les cas de modération restent enregistrés jusqu’à leur suppression par les fonctions disponibles, une demande d’effacement recevable ou la suppression de la base concernée. Certaines données peuvent être conservées plus longtemps lorsqu’une obligation légale ou la défense de droits le justifie.
- Les tickets et journaux publiés dans Discord restent soumis aux paramètres de conservation, à la modération et à la suppression des messages/salons décidées par le serveur et aux règles de Discord.
- Les caches en mémoire du catalogue AniList expirent après environ 30 minutes et les images recadrées après environ 6 heures ; ils disparaissent également au redémarrage du processus.

**Action requise pour l’exploitant :** établir une durée chiffrée adaptée à chaque catégorie et mettre en place les purges correspondantes. Les durées ci-dessus décrivent les mécanismes identifiés dans le code ; elles ne constituent pas une durée maximale garantie.

## 6. Vos choix et vos droits

Vous pouvez retirer votre anniversaire avec `/anniversaire retirer`. Pour demander l’accès, la rectification, la limitation ou l’effacement d’autres données, écrivez au Support sur Discord **[\Kora Support\](https://discord.gg/XdzBPY3KgH)** depuis un moyen permettant de vérifier raisonnablement que la demande concerne votre compte Discord. Précisez le serveur concerné, votre identifiant Discord et le droit exercé ; n’envoyez pas de mot de passe ni de jeton Discord. Nous répondrons dans les délais prévus par la loi applicable, sous réserve des exceptions légales et des droits d’autres personnes.

Les demandes concernant les données que Discord traite pour son propre compte doivent être adressées à Discord via ses outils et sa politique de confidentialité. Vous pouvez également contacter l’autorité de protection des données compétente ; en France, il s’agit de la [CNIL](https://www.cnil.fr/).

## 7. Sécurité

Les données fonctionnelles sont stockées dans une base SQLite sur l’environnement qui exécute le bot. L’accès à cet environnement, aux sauvegardes et aux journaux doit être limité aux personnes autorisées. Le fichier `.env` contient le jeton Discord et des identifiants de configuration ; il ne doit pas être partagé ni ajouté au dépôt Git. Aucune promesse de chiffrement de la base au repos n’est faite par le code actuel.

En cas de suspicion d’accès non autorisé aux données, contactez le **Support**. Le responsable évaluera les obligations de notification applicables.

## 8. Mineurs

Kora ne demande pas l’âge ni l’année de naissance des membres. Il ne doit pas être utilisé pour solliciter des données sensibles. Les utilisateurs doivent satisfaire aux exigences d’âge applicables à Discord dans leur pays.

## 9. Modifications et contact

Cette politique peut être mise à jour si le bot, les données traitées, les prestataires ou les obligations applicables changent. La date en haut de page sera actualisée. Pour toute question ou demande, contactez le **Support**.

## 10. Références

- [Conditions développeur Discord](https://support-dev.discord.com/hc/en-us/articles/8562894815383-Discord-Developer-Terms-of-Service) — elles demandent notamment une politique de confidentialité publique décrivant les données, leur usage, leur partage et les modalités de suppression.
- [Politique développeur Discord](https://support-dev.discord.com/hc/en-us/articles/8563934450327-Discord-Developer-Policy).
- [Politique de confidentialité Discord](https://discord.com/privacy).
- [Règlement général sur la protection des données (RGPD), EUR-Lex](https://eur-lex.europa.eu/eli/reg/2016/679/oj).
- [Conditions d’utilisation de l’API AniList](https://docs.anilist.co/guide/terms-of-use).
