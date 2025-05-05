---
title: Adobe Target avec SDK Mobile Services Adobe v4 pour Android
description: Adobe Target avec SDK Mobile Services Adobe v4 pour Android est le point de départ idéal pour les développeurs Android qui utilisent déjà le SDK Mobile Services d’Adobe v4 et qui souhaitent commencer à personnaliser les expériences des applications avec Adobe Target.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile, Overview
doc-type: tutorial
kt: 3040
exl-id: 20f8ed4f-a86d-4c5e-9296-71a93724caa3
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---

# Adobe Target avec le SDK Mobile Services Adobe v4 pour Android - Aperçu

_Adobe Target avec SDK Mobile Services Adobe v4 pour Android_ est le point de départ idéal pour les développeurs Android qui utilisent déjà le SDK Mobile Services d’Adobe v4 et qui souhaitent commencer à personnaliser les expériences des applications avec Adobe Target.

Une application de démonstration Android vous permet de suivre les leçons. Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à implémenter [!DNL Target] dans votre propre application Android.

Après avoir terminé cet didacticiel, vous serez en mesure de :

* Validation de la configuration du [SDK Mobile Services Adobe](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=fr)
* Implémentez les types de requêtes [!DNL Target] suivants :
   * Prérécupération du contenu [!DNL Target]
   * Lot de plusieurs emplacements [!DNL Target] (mbox) dans une seule requête
   * Blocage des requêtes (s’exécute avant l’affichage de l’application)
   * Demandes non bloquées (s’exécute en arrière-plan)
   * Temps réel (hors mise en cache)
   * Récupération avec contournement de la mémoire cache
* Ajout de paramètres aux demandes de personnalisation améliorée
* Créer des audiences et des offres
* Personnalisation des mises en page
* Déploiement de nouvelles fonctionnalités avec indicateur de fonctionnalités

## Conditions préalables

Dans ces leçons, on suppose que vous :

* Posséder un identifiant d’Adobe et un accès de niveau approbateur à l’interface Adobe Target (voir les étapes de vérification ci-dessous)
* Connaissez votre code client Adobe Target afin de pouvoir envoyer des requêtes à votre propre compte. Le code client s’affiche dans l’interface d’Adobe Target sur la page   Configuration > Mise en oeuvre > Écran Modifier les paramètres at.js
* Ont accès à et connaissent l’ [ interface utilisateur de Mobile Services](https://mobilemarketing.adobe.com/)
* posséder un IDE pour le développement d’applications mobiles Android. Ce tutoriel présente [Android Studio](https://developer.android.com/studio/install) en différentes étapes et captures d’écran

Si vous ne disposez pas de l’accès requis aux solutions Experience Cloud, contactez votre administrateur Experience Cloud.

En outre, nous partons du principe que vous connaissez le développement Android dans Java. Vous n’avez pas besoin d’être un expert Java pour terminer les leçons, mais vous en tirerez plus d’informations si vous pouvez facilement lire et comprendre le code.

### Vérification de l’accès à Adobe Target

Cette leçon nécessite l’accès à Adobe Target. Avant de passer aux étapes suivantes, vérifiez que vous avez accès à Adobe Target en procédant comme suit :

1. Connectez-vous à [Adobe Experience Cloud](https://experience.adobe.com/)
1. Sur l’écran d’accueil de l’Experience Cloud, cliquez sur [!DNL Target] :
   ![Écran d’accueil Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Vous devez accéder à la liste Activités dans Adobe Target, comme illustré ci-dessous, et vous devriez constater que votre utilisateur dispose d’un accès de niveau Approbateur. Si vous ne parvenez pas à accéder à [!DNL Target] ou ne pouvez pas vérifier l’accès de niveau Approbateur, contactez l’un des administrateurs Experience Cloud de votre société, demandez cet accès et reprenez ce tutoriel une fois qu’il a été accordé :

   ![Interface utilisateur de l’Adobe](assets/targetUI_approver.png)

## À propos des leçons

Dans ces leçons, vous allez mettre en oeuvre Adobe Target dans une application de démonstration appelée &quot;We.Travel&quot; à l’aide de votre propre compte Adobe Target. À la fin du tutoriel, vous diffuserez des messages personnalisés à l’utilisateur en fonction de son utilisation de l’application. Les dernières expériences de personnalisation se présentent comme suit :

![ &lbrace;We.Travel app final](assets/overview_final_result.jpg)

Après avoir parcouru l’implémentation dans l’application We.Travel, vous pourrez commencer à utiliser [!DNL Target] dans votre propre application mobile.

Commençons !

**[NEXT : &quot;Télécharger et mettre à jour l’exemple d’application&quot; >](download-and-update-the-sample-app.md)**
