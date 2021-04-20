---
title: Création d’Audiences et d’Offres dans Adobe Target
description: 'Dans cette leçon, nous construisons des audiences et des offres à Adobe Target pour les trois endroits que nous avons mis en place dans les leçons précédentes. Elles seront utilisées pour afficher des expériences personnalisées dans la leçon suivante.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---


# Création d’Audiences et d’Offres dans Adobe Target

Dans cette leçon, nous allons passer à l&#39;interface [!DNL Target] et construire des audiences et des offres pour les trois emplacements que nous avons mis en oeuvre dans les leçons précédentes.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pourrez :

* Création d’audiences dans Adobe Target
* Créer des offres dans Adobe Target

Plus précisément, dans cette leçon, nous allons créer les audiences et les offres nécessaires pour réaliser les cas d&#39;utilisation de la personnalisation définis au début du tutoriel. Nous voulons utiliser les écrans Accueil et Recherche pour aider les utilisateurs de l&#39;application à réserver leurs voyages et nous voulons utiliser l&#39;écran de remerciement pour afficher certaines promotions pertinentes en fonction de la destination de l&#39;utilisateur. Voici un tableau représentant ce que nous allons construire dans cette leçon pour chaque emplacement :

| Emplacement | Public | Offre |
| --- | --- | --- |
| wetravel_commit_home | Nouveaux utilisateurs d’applications mobiles | &quot;Sélectionnez votre Origine et votre destination pour rechercher les itinéraires de bus disponibles&quot; |
| wetravel_engage_search | Nouveaux utilisateurs d’applications mobiles | &quot;Utiliser des filtres pour affiner vos résultats de recherche&quot; |
| wetravel_commit_home | Renvoi d’utilisateurs d’applications mobiles | &quot;Bienvenue de retour ! Utilisez le code promotionnel BACK30 lors du passage en caisse pour bénéficier d&#39;une remise de 10 %.&quot; |
| wetravel_engage_search | Renvoi d’utilisateurs d’applications mobiles | contenu par défaut |
| wetravel_context_dest | Destination : San Diego | &quot;DJ&quot; |
| wetravel_context_dest | Destination : Los Angeles | &quot;Universel&quot; |

## Sélectionner votre espace de travail

Si votre société utilise les propriétés et les espaces de travail pour définir les limites de la personnalisation des applications et des sites Web (et que vous avez implémenté le paramètre at_property dans la dernière leçon), assurez-vous d’abord que vous êtes dans l’espace de travail approprié avant de poursuivre cette leçon. Si vous n’utilisez pas Propriétés et espaces de travail, ignorez cette étape. Sélectionnez l’espace de travail que vous avez utilisé dans la leçon précédente pour copier la valeur at_property :

![Exemple d’espace de travail](assets/workspace.jpg)

## Créer des Audiences

Maintenant, créons les audiences que nous utiliserons pour personnaliser l&#39;application.

### Création d’une Audience pour les nouveaux utilisateurs

Les Audiences d&#39;Adobe Target sont utilisées pour identifier des groupes spécifiques de visiteurs. Les Offres peuvent ensuite être ciblées sur ces groupes spécifiques. Pour les deux premiers emplacements, nous utiliserons une audience &quot;Nouveaux utilisateurs&quot; :

1. Cliquez sur **[!UICONTROL Audiences]** dans la barre de navigation supérieure.
1. Cliquez sur le bouton **[!UICONTROL Créer une Audience]**.
   ![Créer une Audience d’utilisateur](assets/audience_new_mobile_app_users_1.jpg)

1. Saisissez **[!UICONTROL Nouveaux utilisateurs d’applications mobiles]** comme nom d’audience.
1. Sélectionnez **[!UICONTROL Ajouter la règle]**.
1. Sélectionnez une règle **[!UICONTROL personnalisée]**.
   ![Créer une Audience d’utilisateur](assets/audience_new_mobile_app_users_2.jpg)

1. Sélectionnez **[!UICONTROL a.Launches]**.
1. Sélectionnez **[!UICONTROL est inférieur à]**.
1. Saisissez **5**.
1. Enregistrez la nouvelle audience.
   ![Créer une Audience d’utilisateur](assets/audience_new_mobile_app_users_3.jpg)

### Création d’une Audience pour les utilisateurs récurrents

Suivez les mêmes étapes que celles répertoriées ci-dessus pour créer une audience pour les utilisateurs récurrents.

1. Nommez l’audience _Utilisateurs d’applications mobiles renvoyés_.
1. Utilisez **[!UICONTROL a.Launches est supérieur ou égal à 5]** comme règle personnalisée.
1. Enregistrez la nouvelle audience.

   ![Créer une Audience d’utilisateur régulier](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>Toutes les mesures et dimensions de cycle de vie collectées dans le SDK mobile [!DNL Target] sont précédées de &quot;a&quot; (par exemple, a.Launches) et sont disponibles dans l’option &quot;Personnalisé&quot; du menu déroulant et peuvent être utilisées pour créer des audiences.

### Créer une Audience pour les utilisateurs Réservation d&#39;un voyage à San Diego

Nous allons ensuite créer quelques audiences pour certaines des destinations proposées par l&#39;application We.Travel. Lors de la dernière leçon, nous avons transmis la destination en tant que paramètre d&#39;emplacement dans la demande d&#39;emplacement wetravel_context_dest. Ce paramètre est disponible dans l&#39;option &quot;Personnalisé&quot; du menu déroulant.

>[!NOTE]
>
>Si un paramètre que vous prévoyez de voir dans la liste déroulante Personnalisé n&#39;apparaît pas dans l&#39;interface [!DNL Target], vérifiez par doublon qu&#39;il est effectivement transmis dans la requête. Si vous avez vérifié que la requête se trouve dans l’interface [!DNL Target], mais que celle-ci n’est pas chargée en différé, il vous suffit de taper le nom du paramètre et d’appuyer sur Entrée pour continuer à définir votre audience.

1. Nommez l&#39;audience _Destination : San Diego_.
1. Utilisez une règle personnalisée avec cette définition : _locationDest contient San Diego_.
1. Enregistrez la nouvelle audience.

   ![Créer une Audience &quot;San Diego&quot;](assets/audience_locationDest_san_diego.jpg)

### Créer une Audience pour les utilisateurs Réservation d&#39;un voyage à Los Angeles

1. Nommez l&#39;audience _Destination : Los Angeles_
1. Utilisez une règle personnalisée avec cette définition : _locationDest contient Los Angeles_
1. Enregistrez la nouvelle audience.

![Créer une Audience &quot;Los Angeles&quot;](assets/audience_locationDest_los_angeles.jpg)

## Création d’offres

Maintenant, créons des offres pour afficher ces messages. Pour rappel, les offres sont des fragments de code/contenu, qui sont fournis dans la réponse [!DNL Target]. Ils sont le plus souvent créés dans l’interface utilisateur [!DNL Target], mais ils peuvent également être créés via l’API ou à l’aide de l’intégration des fragments d’expérience avec Adobe Experience Manager. Dans les applications mobiles, les offres JSON sont courantes. Dans ce didacticiel, nous utiliserons des offres HTML, qui peuvent être utilisées pour diffuser tout contenu en texte brut (y compris JSON) dans l’application.

### Création de l’Offre pour les nouveaux utilisateurs

Commençons par créer des offres pour les messages destinés aux nouveaux utilisateurs :

1. Cliquez sur **[!UICONTROL Offres]** dans la barre de navigation supérieure.
1. Cliquez sur **[!UICONTROL Créer]**.
1. Sélectionnez **[!UICONTROL Offre HTML]**.

   ![Créer une Offre d’accueil](assets/offer_home_1.jpg)

1. Nommez l&#39;offre _Accueil : Engager de nouveaux utilisateurs_.
1. Saisissez _Sélectionnez Source et Destination pour rechercher les bus disponibles_ comme code.
1. Enregistrez la nouvelle offre.

   ![Créer une Offre HTML d’accueil](assets/offer_home_2.jpg)

### Création de l’Offre pour les utilisateurs récurrents

Maintenant, créons l’offre unique pour les utilisateurs récurrents (la deuxième offre sera le contenu par défaut, qui s’affichera comme rien) :

1. Nommez l&#39;offre _Accueil : Utilisateurs récurrents_.
1. Entrez _Bienvenue de nouveau ! Utilisez le code promotionnel BACK30 lors du passage en caisse pour obtenir une remise de 10 %._ comme code HTML.
1. Enregistrez la nouvelle offre.

   ![Créer une Offre HTML d’accueil](assets/offer_home_returning_users.jpg)

### Création de l’Offre San Diego

Lorsque &quot;DJ&quot; est renvoyé à l’activité ThankYou, la logique de la fonction filterRecommendationsBasedOnOffer() affiche une bannière pour &quot;Rock Night with DJ SAM&quot; :

1. Nommez l&#39;offre _Promotion pour San Diego_.
1. Saisissez _DJ_ comme code HTML.
1. Enregistrez la nouvelle offre.

![Créer une Offre &quot;San Diego&quot;](assets/offer_san_diego.jpg)

### Créer une Offre pour les utilisateurs se rendant à Los Angeles

Lorsque &quot;Universal&quot; est renvoyé à l’activité ThankYou, la logique de la fonction filterRecommendationsBasedOnOffer() affiche une bannière pour &quot;Universal Studios&quot; :

1. Nommez l&#39;offre _Promotion pour Los Angeles_.
1. Saisissez _Universal_ comme code HTML.
1. Enregistrez la nouvelle offre.

![Créer une Offre &quot;Los Angeles&quot;](assets/offer_los_angeles.jpg)

## Conclusion

Maintenant nous avons nos Audiences et nos Offres. Dans la leçon suivante, nous allons construire des activités qui lient les emplacements, les audiences et les offres ensemble pour créer des expériences personnalisées !

**[SUIVANT : &quot;Personnaliser les mises en page&quot; >](personalize-layouts.md)**
