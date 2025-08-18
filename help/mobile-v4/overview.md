---
title: Adobe Target avec Adobe Mobile Services SDK v4 pour Android
description: Adobe Target avec Adobe Mobile Services SDK v4 pour Android est le point de départ idéal pour les développeurs Android qui utilisent déjà Adobe Mobile Services SDK v4 et qui souhaitent commencer à personnaliser les expériences d’application avec Adobe Target.
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

# Adobe Target avec Adobe Mobile Services SDK v4 pour Android - Présentation

_Adobe Target avec Adobe Mobile Services SDK v4 pour Android_ est le point de départ idéal pour les développeurs Android qui utilisent déjà Adobe Mobile Services SDK v4 et qui souhaitent commencer à personnaliser les expériences d’application avec Adobe Target.

Une application Android de démonstration est fournie pour que vous puissiez suivre les leçons. Après avoir suivi ce tutoriel, vous devriez être prêt à commencer à implémenter [!DNL Target] dans votre propre application Android !

Après avoir terminé cet didacticiel, vous serez en mesure de :

* Valider la configuration de [Adobe Mobile Services SDK](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=fr)
* Implémentez les types de requêtes [!DNL Target] suivants :
   * Prérécupération de contenu [!DNL Target]
   * Traitement par lots de plusieurs emplacements de [!DNL Target] (mbox) dans une seule requête
   * Blocage des requêtes (s’exécute avant l’affichage de l’application)
   * Requêtes non bloquantes (s’exécute en arrière-plan)
   * Temps réel (sans mise en cache)
   * Récupération après débordement du cache
* Ajout de paramètres aux demandes de personnalisation améliorée
* Créer des audiences et des offres
* Personnaliser les dispositions
* Déploiement de nouvelles fonctionnalités avec l’indicateur de fonctionnalité

## Conditions préalables

Dans ces leçons, on suppose que vous :

* disposer d’un Adobe Id et d’un accès de niveau approbateur à l’interface d’Adobe Target (voir les étapes de vérification ci-dessous) ;
* connaître votre code client Adobe Target afin de pouvoir envoyer des requêtes à votre propre compte ; Le code client s’affiche dans l’interface d’Adobe Target sur le   Configuration > Implémentation > Écran Modifier les paramètres at.js
* disposer d’un accès à l’interface utilisateur [Mobile Services](https://mobilemarketing.adobe.com/) et la connaître ;
* disposer d’un IDE pour le développement d’applications mobiles Android ; Ce tutoriel présente [Android Studio](https://developer.android.com/studio/install) en différentes étapes et copies d’écran

Si vous ne disposez pas de l’accès requis aux solutions Experience Cloud, contactez votre administrateur ou administratrice Experience Cloud.

En outre, il est supposé que vous connaissez le développement Android en Java. Vous n’avez pas besoin d’être un expert Java pour suivre les leçons, mais vous en tirerez davantage si vous pouvez lire et comprendre le code confortablement.

### Vérifier l’accès à Adobe Target

Cette leçon nécessite l’accès à Adobe Target. Avant de passer aux étapes suivantes, assurez-vous d’avoir accès à Adobe Target en procédant comme suit :

1. Connectez-vous à [Adobe Experience Cloud](https://experience.adobe.com/)
1. Sur l’écran d’accueil d’Experience Cloud, cliquez sur [!DNL Target] :
   ![Écran d’accueil d’Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Vous devriez accéder à la liste des activités dans Adobe Target, comme illustré ci-dessous, et vous devriez voir que votre utilisateur dispose d’un accès de niveau Approbateur. Si vous ne parvenez pas à accéder à [!DNL Target] ou à vérifier l’accès au niveau de l’approbateur ou de l’approbatrice, contactez l’administration Experience Cloud de votre société, demandez cet accès et reprenez ce tutoriel une fois qu’il vous a été accordé :

   ![Interface utilisateur Adobe](assets/targetUI_approver.png)

## À propos des leçons

Dans ces leçons, vous allez mettre en œuvre Adobe Target dans une application de voyage de démonstration appelée « We.Travel » à l’aide de votre propre compte Adobe Target. À la fin du tutoriel, vous allez diffuser des messages personnalisés à l’utilisateur en fonction de son utilisation de l’application ! Les expériences de personnalisation finales ressembleront à ceci :

![Application We.Travel finale ](assets/overview_final_result.jpg)

Après avoir parcouru l’implémentation dans l’application We.Travel, vous pourrez commencer à utiliser [!DNL Target] dans votre propre application mobile.

Commençons !

**[SUIVANT : « Télécharger et mettre à jour l’exemple d’application » >](download-and-update-the-sample-app.md)**
