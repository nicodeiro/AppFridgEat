# FridgEat — ce qu'on a décidé

Ce document résume les décisions prises avant d'écrire le code. Il sert de référence pour toute la suite.

## L'idée

**Ton frigo te dit ce qu'il contient, ce qui va périmer et quoi cuisiner ce soir.**

Le problème : on range les courses, on oublie ce qu'il y a dans le frigo, des produits périment au fond d'un bac et finissent à la poubelle. Et chaque soir, devant le frigo ouvert, on se demande quoi faire avec ce qu'il y a.

Les apps d'inventaire existantes butent presque toutes sur la saisie à la main, que plus personne ne fait au bout d'une semaine. FridgEat se démarque sur deux points :

- **la saisie en une photo** (les courses posées sur la table, ou le ticket de caisse) ;
- **la mascotte au cœur de l'app**, pas un simple logo.

## Pour qui

Les 18-35 ans qui vivent seuls ou à deux (étudiants, jeunes actifs), sur iPhone d'abord. Ils font leurs courses environ une fois par semaine et manquent d'idées pour cuisiner.

Les familles (frigo partagé entre plusieurs personnes, donc des comptes) viendront plus tard.

## La mascotte : FridgEat

Un frigo avec des yeux, qui s'appelle FridgEat comme l'app.

- C'est **l'écran d'accueil** : on touche la porte, elle s'ouvre, on voit le contenu.
- Son regard reflète l'état du frigo :
  - **tout est frais** : yeux pétillants ;
  - **un produit va périmer** : yeux inquiets, tournés vers la porte ;
  - **frigo vide** : yeux mi-clos, un peu tristes ;
  - **après avoir rangé des courses** : yeux rieurs.
- Il cligne des yeux et suit le doigt, pour paraître vivant.
- Les notifications sont écrites avec sa voix (« Psst… les yaourts, c'est demain dernier délai ! »).

## Version 1

1. **Remplir le frigo en une photo** : l'app liste les produits et estime leur date de péremption, que l'utilisateur corrige d'un tap si besoin. L'ajout à la main reste possible.
2. **« Qu'est-ce que je cuisine ? »** : 3 recettes avec ce qu'on a, en utilisant d'abord ce qui va bientôt périmer. Les ingrédients utilisés sortent du frigo tout seuls.
3. **Les rappels** : une notification la veille de la péremption d'un produit.

**Hors V1** : comptes et partage en famille, liste de courses, scan des codes-barres, infos nutritionnelles, planning des repas, publicité.

## Modèle économique

L'app est **gratuite à télécharger et à utiliser**. Sur l'App Store, elle apparaît comme « Gratuit – achats intégrés ».

| Gratuit | FridgEat+ (abonnement) |
|---|---|
| La mascotte et ses réactions | Photos illimitées (avec une limite haute contre les abus) |
| Ajout manuel des produits | Recettes sur mesure écrites par l'IA (« rapide », « végé », « pour 4 »…) |
| Rappels avant péremption | Personnalisation de la mascotte (couleurs, accessoires) |
| Recettes tirées de la liste intégrée à l'app | |
| 5 photos offertes au départ, puis 2 par mois | |

**Prix** : 2,99 € par mois ou 19,99 € par an, avec 7 jours d'essai gratuit.

### Les chiffres (ordres de grandeur, à mesurer)

- Analyse d'une photo par l'IA : environ 0,5 à 1,5 centime.
- 3 recettes écrites par l'IA : environ 1 à 2 centimes.
- Recettes tirées de la liste intégrée : 0 € (la liste est produite une fois, pour environ 10 €).
- Un utilisateur gratuit coûte environ 3 centimes par mois ; un abonné qui utilise beaucoup l'app, au maximum environ 0,50 €.
- Sur un abonnement à 2,99 €, il reste environ 2,10 € après TVA et commission d'Apple (15 % dans le programme pour les petits développeurs). La marge est donc d'environ 1,60 € par abonné et par mois.
- Un abonné couvre les coûts d'une cinquantaine d'utilisateurs gratuits. Entre 2 et 5 % d'abonnés, l'app couvre ses coûts ou dégage une marge confortable.

### Plus tard

- **Pub récompensée** (une vidéo pour obtenir une photo de plus quand les photos gratuites sont épuisées), environ une par semaine au maximum, ajoutée **après la sortie**. Elle ne rapporte presque rien en elle-même, mais elle finance les photos des utilisateurs gratuits et met l'abonnement en avant.
- Accessoires pour la mascotte vendus à l'unité, partenariats avec des drives.

## Choix techniques

- **Expo (React Native)** : un seul code pour iPhone, et Android plus tard. L'app est construite sur les serveurs d'Expo, donc sans Mac.
- **Données stockées sur le téléphone**, sans compte à créer.
- **Rappels** programmés par le téléphone lui-même.
- **Recettes** : une liste d'environ 300 recettes intégrée à l'app.
- **Photo** : un petit serveur garde la clé de l'IA en sécurité et compte les photos gratuites. On comparera plusieurs modèles sur de vraies photos pour garder le moins cher qui marche bien.
- **Abonnement** : le système de paiement d'Apple, géré avec RevenueCat.

## Les étapes

0. ~~Nettoyage : supprimer l'ancien squelette et écrire ce document.~~ Fait.
1. La mascotte animée et l'écran d'accueil.
2. Le frigo : ajout à la main, liste des produits, dates, rappels.
3. Les recettes tirées de la liste intégrée.
4. La photo avec l'IA (serveur et compteur de photos gratuites).
5. L'abonnement FridgEat+.
6. La préparation pour l'App Store : icône, captures d'écran, politique de confidentialité, test sur iPhone via TestFlight, envoi à Apple.

## À vérifier en cours de route

- Le coût réel d'une photo, mesuré sur de vraies courses et de vrais tickets.
- Si l'iPhone peut lire les tickets de caisse directement sur le téléphone (gratuitement) avec une qualité suffisante.
- Le taux d'abonnement après la sortie.
