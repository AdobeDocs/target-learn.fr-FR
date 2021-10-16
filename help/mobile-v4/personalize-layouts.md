---
title: Personnalisation des mises en page
description: 'Dans cette dernière leçon, nous créons deux activités de personnalisation dans Target pour nos audiences. Découvrez comment charger et afficher les activités dans l’application et vérifier que le contenu s’affiche au bon moment aux bons endroits.  '
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
source-wordcount: '1092'
ht-degree: 1%

---

# Personnalisation des mises en page

Il est maintenant temps de tout rassembler et créer des expériences personnalisées. Une _activité_ est le mécanisme [!DNL Target] qui relie les emplacements, les audiences et les offres ensemble, de sorte que lorsque la demande est effectuée à partir de l’application, [!DNL Target] répond avec le contenu personnalisé. Nous allons créer deux activités de personnalisation dans [!DNL Target] et valider que le contenu personnalisé s’affiche pour le bon utilisateur au bon moment et au bon emplacement.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Création d’activités dans Adobe Target
* Validation des activités dans l’exemple d’application

## Création d’activités dans Adobe Target

Découvrez comment créer des activités Interagir avec les utilisateurs et Offres contextuelles .

### Première activité - &quot;Interagir avec les utilisateurs&quot;

Voici un résumé de l’activité que nous allons créer :

| Public | Emplacements | Offres |
|---|---|---|
| Nouveaux utilisateurs d’applications mobiles | wetravel_engage_home, wetravel_engage_search | Accueil : Interagir avec les nouveaux utilisateurs, Rechercher : Interagir avec les nouveaux utilisateurs |
| Renvoi d’utilisateurs d’applications mobiles | wetravel_engage_home, wetravel_engage_search | Accueil : Utilisateurs récurrents, default_content |

Dans l&#39;interface [!DNL Target], procédez comme suit :

1. Sélectionnez **[!UICONTROL Activités]** > **[!UICONTROL Créer l’activité]** > **[!UICONTROL Ciblage d’expérience]**.

   ![Création d’une activité](assets/activity_create_1.jpg)

1. Cliquez sur **[!UICONTROL Application mobile]**.
1. Sélectionnez le **[!UICONTROL compositeur de formulaire]**.
1. Sélectionnez votre espace de travail (le même espace de travail que celui utilisé dans les leçons précédentes).
1. Sélectionnez votre propriété (la même propriété que celle utilisée dans les leçons précédentes).
1. Cliquez sur **[!UICONTROL Suivant]**.

   ![Création d’une activité](assets/activity_create_2.jpg)

1. Remplacez le titre de l’activité par **[!UICONTROL Interagir avec les utilisateurs]**.
1. Sélectionnez les **[!UICONTROL points de suspension]** > **[!UICONTROL Changer l’audience]**.
   ![Nouveaux utilisateurs d’applications mobiles - Changement d’audience](assets/activity_create_3.jpg)
1. Définissez l’audience sur **[!UICONTROL Nouveaux utilisateurs d’applications mobiles]**.
1. Cliquez sur **[!UICONTROL Terminé]**.
   ![Nouveaux utilisateurs d’applications mobiles](assets/activity_create_4.jpg)

1. Remplacez l’emplacement par _wetravel_engage_home_.
1. Sélectionnez la flèche de liste déroulante en regard de Contenu par défaut et sélectionnez **[!UICONTROL Modifier l’offre de HTML]**.

   ![Nouveaux utilisateurs d’applications mobiles](assets/activity_create_5.jpg)

1. Sélectionnez la **[!UICONTROL Page d’accueil : Interagir avec l’offre Nouveaux utilisateurs]**.
1. Sélectionnez **[!UICONTROL Terminé]**.

   ![Nouveaux utilisateurs d’applications mobiles](assets/activity_create_6.jpg)

1. Sélectionnez **[!UICONTROL Ajouter un emplacement]**.
   ![Nouveaux utilisateurs d’applications mobiles](assets/activity_create_7.jpg)

1. Sélectionnez l’emplacement _wetravel_engage_search_.
1. Modifiez l’offre de HTML.

   ![Nouveaux utilisateurs d’applications mobiles](assets/activity_create_8.jpg)

1. Sélectionnez la **[!UICONTROL recherche : Interagir avec l’offre Nouveaux utilisateurs]**.
1. Cliquez sur **[!UICONTROL Terminé]**.

   ![Nouveaux utilisateurs d’applications mobiles](assets/activity_create_9.jpg)

Vous venez de connecter une audience à des emplacements et des offres, créant ainsi une expérience personnalisée pour les nouveaux utilisateurs de l’application mobile. L’expérience doit maintenant se présenter comme suit :

![Expérience finale](assets/activity_engage_users_a_final.jpg)

Créez maintenant une expérience pour les utilisateurs de l’application mobile récurrents :

1. Sélectionnez **[!UICONTROL Ajouter le ciblage d’expérience]** à gauche.
1. Sélectionnez le public **[!UICONTROL Utilisateurs de l’application mobile récurrents]**.
1. Sélectionnez **[!UICONTROL Terminé]**.
   ![Renvoi de l’audience des utilisateurs d’applications mobiles](assets/activity_create_11.jpg)

Maintenant, utilisez le même processus que précédemment pour configurer la nouvelle expérience. La configuration de l’expérience Utilisateurs d’applications mobiles récurrents doit se présenter comme suit :

![Renvoi final des utilisateurs d’applications mobiles](assets/activity_engage_users_b_final.jpg)

Passons à l’écran suivant de la configuration :

1. Cliquez sur **[!UICONTROL Suivant]** pour accéder à l’écran **[!UICONTROL Ciblage]**.
1. Utilisez les paramètres par défaut pour le ciblage. Si des expériences s’appliquaient à des audiences qui se chevauchaient (par exemple, _Utilisateurs de New York_ et _Nouveaux utilisateurs_) vous pouvez classer l’ordre de priorité dans cet écran.
1. Cliquez sur **[!UICONTROL Suivant]** pour passer à **[!UICONTROL Objectifs et paramètres]**.

   ![Activité Interagir avec les utilisateurs - Ciblage par défaut](assets/activity_engage_users_targeting.jpg)

Terminons maintenant la configuration de l’activité :

1. Définissez l’ **[!UICONTROL objectif Principal]** sur **[!UICONTROL Conversion]**.
1. Définissez l’action sur **[!UICONTROL A affiché une mbox]** > _wetravel_context_dest_ (Puisque cet emplacement se trouve sur l’écran de confirmation, nous pouvons l’utiliser pour mesurer les conversions).

   ![Activité Interagir avec les utilisateurs - Objectifs](assets/activity_create_12.jpg)

1. Conservez les valeurs par défaut de tous les autres paramètres de l’écran.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer l’activité.
1. Activez l’**[!UICONTROL activité]** dans l’écran suivant.

![Audience de l’expérience B](assets/activity_create_13.jpg)

Notre première activité est maintenant en ligne et prête à être testée !

### Deuxième activité - &quot;Offres contextuelles&quot;

Voici un résumé de la seconde activité que nous allons créer :

| Public | Emplacement | Offres |
| --- | --- | --- |
| Destination : San Diego | wetravel_context_dest | Promotion pour San Diego |
| Destination : Los Angeles | wetravel_context_dest | Promotion pour Los Angeles |

Répétez la même procédure que ci-dessus pour l’activité suivante : &quot;Offres contextuelles&quot;. La configuration finale des deux expériences est présentée ci-dessous :

#### San Diego

![Offres Contextuelles - Expérience A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Offres contextuelles - Expérience B](assets/activity_contextual_b_final.jpg)

À l’étape Objectifs et paramètres , nous allons modifier l’Principal Objectif en l’emplacement sur l’écran de confirmation de réservation :

1. Sous **[!UICONTROL Paramètres de création de rapports]**, définissez **[!UICONTROL Principal Objectif]** sur **[!UICONTROL Conversion]**.
1. Définissez l’action sur **[!UICONTROL A affiché une mbox]** > _wetravel_context_dest_ (dans cette activité, cette mesure n’a pratiquement aucun sens puisqu’il s’agit également du même emplacement qui fournit l’expérience).
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

![Offres contextuelles - Expérience](assets/activity_create_14.jpg)

Activez l’activité dans l’écran suivant.

Maintenant, notre seconde activité est en ligne et prête à être testée !

## Validation de l’offre d’accueil

Exécutez l’émulateur et recherchez la première offre à afficher en bas de l’écran d’accueil. Si vous êtes un utilisateur récurrent avec 5 lancements d’application ou plus, l’offre _de retour_ s’affiche. Si vous êtes un nouvel utilisateur (moins de 5 lancements d’applications), le message _nouvel utilisateur_ devrait s’afficher :

![Validation de l’offre d’accueil](assets/layout_home_validate.jpg)

Si la nouvelle offre utilisateur ne s’affiche pas, essayez d’effacer les données de votre émulateur. Cela réinitialise le lancement de l’application sur 1 lors de votre prochain lancement. Cette opération est effectuée sous **[!UICONTROL Outils]** > **[!UICONTROL Gestionnaire AVD]**. Vous devrez peut-être redémarrer Android Studio, si Logcat ne fonctionne pas correctement :

![Émulateur d’effacement](assets/layout_home_validate_avd_wipe.jpg)

Vous pouvez également valider la réponse dans Logcat en filtrant _wetravel_engage_home_ :

![Validation de l’offre d’accueil - Logcat](assets/layout_home_validate_logcat.jpg)

## Validation de l’offre de recherche

Sélectionnez **[!UICONTROL San José]** comme **[!UICONTROL Départ]** et **[!UICONTROL San Diego]** comme **[!UICONTROL Destination]** et cliquez sur **[!UICONTROL Rechercher le bus]** pour rechercher les bus disponibles.

Dans l’écran des résultats, le message _use filters_ devrait s’afficher. Si vous êtes un utilisateur récurrent avec 5 lancements d’applications ou plus, aucun message n’apparaît ici puisque le contenu par défaut est défini pour cet emplacement (qui est vide) :

![Validation de l’offre de recherche](assets/layout_search_validate.jpg)

## Validation des offres contextuelles sur l’écran de remerciement

Poursuivez maintenant le processus de réservation :

* Sélectionnez un bus dans l’écran des résultats.
* Sélectionnez un siège dans l’écran de passage en caisse.
* Sélectionnez **[!UICONTROL Carte de crédit]** dans l’écran de paiement (laissez les informations de paiement vides - aucune réservation réelle n’aura lieu).

Comme San Diego a été sélectionné comme destination, la bannière d’offre _DJ SAM_ devrait s’afficher sur l’écran de confirmation :

![Validation de l’offre contextuelle - San Diego](assets/layout_context_san_diego.jpg)

Sélectionnez maintenant **[!UICONTROL Terminé]** et essayez une autre réservation avec Los Angeles comme destination. L’écran de confirmation doit afficher la bannière _Universal Studios_ :

![Validation de l’offre contextuelle - Los Angeles](assets/layout_context_los_angeles.jpg)

## Conclusion

Félicitations ! Ceci termine la partie principale du tutoriel Adobe Target SDK 4.x pour Android. Vous disposez désormais des compétences nécessaires pour mettre en oeuvre la personnalisation dans les applications Android. Vous pouvez vous référer à cette documentation et application de démonstration comme référence pour vos projets futurs.

Suivant : Le marquage des fonctionnalités est une autre fonctionnalité qui peut être implémentée avec Adobe Target sous Android. Pour en savoir plus sur le marquage des fonctionnalités, consultez la leçon suivante.

**[SUIVANT : Marquage des fonctionnalités >](feature-flagging.md)**
