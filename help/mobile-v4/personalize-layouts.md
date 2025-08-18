---
title: Personnaliser les mises en page
description: Dans cette dernière leçon, nous allons créer deux activités de personnalisation dans Target pour nos audiences. Découvrez comment charger et afficher les activités dans l’application et vérifier que le contenu s’affiche au bon moment et aux bons emplacements.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
author: Daniel Wright
exl-id: a9f033d9-9f72-4154-88f5-d36423a404d0
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---

# Personnaliser les mises en page

Il est maintenant temps de tout rassembler et de créer des expériences personnalisées. Une _activité_ est le mécanisme [!DNL Target] qui relie les emplacements, les audiences et les offres entre eux, de sorte que lorsque la requête est effectuée à partir de l’application, [!DNL Target] répond avec le contenu personnalisé. Nous allons créer deux activités de personnalisation dans [!DNL Target] et vérifier que le contenu personnalisé s’affiche pour le bon utilisateur au bon moment et au bon endroit.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Créer des activités dans Adobe Target
* Validation des activités dans l’exemple d’application

## Création d’activités dans Adobe Target

Découvrez comment créer des activités Engager les utilisateurs et les offres contextuelles .

### Première activité - « Impliquer les utilisateurs »

Voici un résumé de l’activité que nous allons créer :

| Public | Emplacements | Offres |
|---|---|---|
| Nouveaux utilisateurs de l’application mobile | wetravel_engage_home, wetravel_engage_search | Accueil : Engager De Nouveaux Utilisateurs, Rechercher : Engager De Nouveaux Utilisateurs |
| Utilisateurs d’applications mobiles récurrents | wetravel_engage_home, wetravel_engage_search | Accueil : utilisateurs récurrents, default_content |

Dans l’interface [!DNL Target], procédez comme suit :

1. Sélectionnez **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

   ![Créer une activité](assets/activity_create_1.jpg)

1. Cliquez sur **[!UICONTROL Mobile App]**.
1. Sélectionnez le **[!UICONTROL Form composer]**.
1. Sélectionnez votre espace de travail (le même espace de travail que celui utilisé dans les leçons précédentes).
1. Sélectionnez votre Propriété (la même propriété que celle que vous avez utilisée dans les leçons précédentes).
1. Cliquez sur **[!UICONTROL Next]**.

   ![Créer une activité](assets/activity_create_2.jpg)

1. Remplacez le titre de l’activité par **[!UICONTROL Engage Users]**.
1. Sélectionnez le **[!UICONTROL ellipsis]** > **[!UICONTROL Change Audience]**.
   ![Les nouveaux utilisateurs de l’application mobile changent d’audience](assets/activity_create_3.jpg)
1. Définissez l’audience sur **[!UICONTROL New Mobile App Users]**.
1. Cliquez sur **[!UICONTROL Done]**.
   ![Nouvelle audience d’utilisateurs d’applications mobiles](assets/activity_create_4.jpg)

1. Remplacez l’emplacement par _wetravel_engage_home_.
1. Sélectionnez la flèche de liste déroulante en regard de Contenu par défaut et sélectionnez **[!UICONTROL Change HTML Offer]**.

   ![Nouvelle audience d’utilisateurs d’applications mobiles](assets/activity_create_5.jpg)

1. Sélectionnez l’offre **[!UICONTROL Home: Engage New Users]**.
1. Sélectionnez **[!UICONTROL Done]**.

   ![Nouvelle audience d’utilisateurs d’applications mobiles](assets/activity_create_6.jpg)

1. Sélectionnez **[!UICONTROL Add Location]**.
   ![Nouvelle audience d’utilisateurs d’applications mobiles](assets/activity_create_7.jpg)

1. Sélectionnez l’emplacement _wetravel_engage_search_.
1. Modifiez l’offre HTML.

   ![Nouvelle audience d’utilisateurs d’applications mobiles](assets/activity_create_8.jpg)

1. Sélectionnez l’offre **[!UICONTROL Search: Engage New Users]**.
1. Cliquez sur **[!UICONTROL Done]**.

   ![Nouvelle audience d’utilisateurs d’applications mobiles](assets/activity_create_9.jpg)

Vous venez de connecter une audience à des emplacements et à des offres, ce qui crée une expérience personnalisée pour les nouveaux utilisateurs de l&#39;application mobile. L’expérience doit maintenant ressembler à ceci :

![Expérimentez Une Finale](assets/activity_engage_users_a_final.jpg)

Créez maintenant une expérience pour les utilisateurs d’applications mobiles récurrents :

1. Sélectionnez **[!UICONTROL Add Experience Targeting]** à gauche.
1. Sélectionnez l’**[!UICONTROL Returning Mobile App Users]** Audience .
1. Sélectionnez **[!UICONTROL Done]**.
   ![Audience Des Utilisateurs D’Applications Mobiles Récurrents](assets/activity_create_11.jpg)

Utilisez à présent le même processus que celui utilisé précédemment pour configurer la nouvelle expérience . La configuration de l’expérience Utilisateurs d’applications mobiles récurrents doit se présenter comme suit :

![Utilisateurs De L’Application Mobile Récurrents - Final](assets/activity_engage_users_b_final.jpg)

Passons à l’écran suivant de la configuration :

1. Cliquez sur **[!UICONTROL Next]** pour accéder à l’écran **[!UICONTROL Targeting]**.
1. Utilisez les paramètres par défaut pour le ciblage. Si vous aviez des expériences pour des audiences qui se chevauchaient (par exemple, _New York Users_ et _First Time Users_), vous pourriez organiser l’ordre de priorité sur cet écran.
1. Cliquez sur **[!UICONTROL Next]** pour accéder à **[!UICONTROL Goals & Settings]**.

   ![Activité Engage Users - Ciblage par défaut](assets/activity_engage_users_targeting.jpg)

Maintenant, terminons la configuration de l’activité :

1. Définissez la **[!UICONTROL Primary Goal]** sur **[!UICONTROL Conversion]**.
1. Définissez l’action sur **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (Cet emplacement se trouvant sur l’écran de confirmation, nous pouvons l’utiliser pour mesurer les conversions).

   ![Activité Engage Users - Objectifs](assets/activity_create_12.jpg)

1. Conservez tous les autres paramètres à l’écran aux valeurs par défaut.
1. Cliquez sur **[!UICONTROL Save & Close]** pour enregistrer l’activité.
1. Activez le **[!UICONTROL Activity]** dans l’écran suivant.

![Audience B de l’expérience](assets/activity_create_13.jpg)

Notre première activité est maintenant en ligne et prête à être testée !

### Deuxième Activité - « Offres Contextuelles »

Voici un résumé de la deuxième activité que nous allons créer :

| Public | Emplacement | Offres |
| --- | --- | --- |
| Destination : San Diego | wetravel_context_dest | Promotion pour San Diego |
| Destination : Los Angeles | wetravel_context_dest | Promotion pour Los Angeles |

Répétez le même processus que ci-dessus pour l&#39;Activité suivante : « Offres contextuelles ». La configuration finale des deux expériences est affichée ci-dessous :

#### San Diego

![Offres contextuelles - Expérience A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Offres contextuelles - Expérience B](assets/activity_contextual_b_final.jpg)

À l’étape Objectifs et paramètres , nous modifierons l’objectif du Principal en fonction de l’emplacement sur l’écran de confirmation de réservation :

1. Sous le **[!UICONTROL Reporting Settings]** , définissez la **[!UICONTROL Primary Goal]** sur **[!UICONTROL Conversion]**.
1. Définissez l’action sur **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (dans cette activité, cette mesure n’a aucun sens, car il s’agit également du même emplacement qui fournit l’expérience).
1. Cliquez sur **[!UICONTROL Save & Close]**.

![Offres contextuelles - Expérience](assets/activity_create_14.jpg)

Activez l’activité dans l’écran suivant.

Notre deuxième activité est maintenant en ligne et prête à être testée !

## Validation de l’offre d’accueil

Exécutez l’émulateur et recherchez la première offre à afficher en bas de l’écran d’accueil. Si vous êtes un utilisateur récurrent avec 5 lancements d’application ou plus, l’offre _retour de bienvenue_ s’affiche. Si vous êtes un nouvel utilisateur (moins de 5 lancements d’application), le message _nouvel utilisateur_ s’affiche normalement :

![Valider l’offre d’accueil](assets/layout_home_validate.jpg)

Si la nouvelle offre utilisateur ne s’affiche pas, essayez d’effacer les données de votre émulateur. Cela réinitialisera les lancements d’application sur 1 lors de votre prochain lancement. Pour ce faire, accédez à **[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**. Vous devrez peut-être redémarrer Android Studio également si Logcat ne fonctionne pas correctement :

![Effacer l’émulateur](assets/layout_home_validate_avd_wipe.jpg)

Vous pouvez également valider la réponse dans Logcat en filtrant pour _wetravel_engage_home_ :

![Valider L’Offre D’Accueil - Logcat](assets/layout_home_validate_logcat.jpg)

## Validation de l’offre de recherche

Sélectionnez **[!UICONTROL San Jose]** comme **[!UICONTROL Departure]** et **[!UICONTROL San Diego]** comme **[!UICONTROL Destination]**, puis cliquez sur **[!UICONTROL Find Bus]** pour rechercher les bus disponibles.

Sur l’écran des résultats, vous devriez voir le message _utiliser des filtres_. Si vous êtes un utilisateur récurrent avec 5 lancements d’application ou plus, aucun message n’apparaîtra ici, car le contenu par défaut est défini pour cet emplacement (qui est vide) :

![Valider l’offre de recherche](assets/layout_search_validate.jpg)

## Validation des offres contextuelles sur l’écran de remerciement

Maintenant, continuez le processus de réservation :

* Sélectionnez un bus sur l&#39;écran des résultats.
* Sélectionnez une place sur l’écran de passage en caisse.
* Sélectionnez **[!UICONTROL Credit Card]** sur l&#39;écran de paiement (laissez les informations de paiement vides - aucune réservation réelle n&#39;aura lieu).

Comme San Diego a été sélectionnée comme destination, vous devriez voir la bannière d’offre _DJ SAM_ sur l’écran de confirmation :

![Valider l’offre contextuelle - San Diego](assets/layout_context_san_diego.jpg)

Sélectionnez maintenant **[!UICONTROL Done]** et essayez une autre réservation avec Los Angeles comme destination. L’écran de confirmation doit afficher la bannière _Universal Studios_ :

![Valider l’offre contextuelle - Los Angeles](assets/layout_context_los_angeles.jpg)

## Conclusion

Félicitations ! Cela conclut la partie principale du tutoriel Adobe Target SDK 4.x pour Android. Vous disposez désormais des compétences nécessaires pour implémenter la personnalisation dans les applications Android. Vous pouvez vous référer à cette documentation et à cette application de démonstration comme référence pour vos projets futurs.

Suivant : l’indicateur de fonctionnalité est une autre fonctionnalité qui peut être implémentée avec Adobe Target dans Android. Pour en savoir plus sur les indicateurs de fonctionnalité, consultez la leçon suivante.

**[NEXT : indicateur de fonctionnalité >](feature-flagging.md)**
