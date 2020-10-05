---
title: adobe target avec Adobe Mobile Services SDK v4 pour Android
description: adobe target avec Adobe Mobile Services SDK v4 pour Android est le point de départ idéal pour les développeurs Android qui utilisent déjà Adobe Mobile Services SDK v4 et souhaitent début de la personnalisation des expériences d’application avec Adobe Target.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: d6cedd55dcc9c08d2d2ca5709e15fe5ea9fab8b8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---


# adobe target avec Adobe Mobile Services SDK v4 pour Android - Présentation

_adobe target avec Adobe Mobile Services SDK v4 pour Android_ est le point de départ idéal pour les développeurs Android qui utilisent déjà Adobe Mobile Services SDK v4 et souhaitent début de la personnalisation des expériences d’application avec Adobe Target.

Une application de démonstration Android vous permet de suivre les cours. Après avoir suivi ce didacticiel, vous devriez être prêt à début la mise en oeuvre [!DNL Target] dans votre propre application Android !

Après avoir terminé cet didacticiel, vous serez en mesure de :

* Validation de la configuration du SDK [](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html) Adobe Mobile Services
* Mettez en oeuvre les types de [!DNL Target] requêtes suivants :
   * Prérécupération du [!DNL Target] contenu
   * Traiter plusieurs [!DNL Target] emplacements (mbox) dans une seule requête
   * Blocage des requêtes (s’exécute avant l’affichage de l’application)
   * Demandes non bloquées (s’exécute en arrière-plan)
   * Temps réel (sans mise en cache)
   * Récupération en mémoire cache
* ajouter des paramètres aux demandes de personnalisation améliorée
* Créer des audiences et des offres
* Personnalisation des mises en page
* Mise en service de nouvelles fonctionnalités avec indicateur de fonctionnalité

## Conditions préalables

Dans ces leçons, on suppose que vous :

* Disposer d’un ID d’Adobe et d’un accès de niveau approbateur à l’interface Adobe Target (voir les étapes de vérification ci-dessous)
* Connaissez votre code client Adobe Target afin que vous puissiez envoyer des requêtes à votre propre compte. Le code client s’affiche dans l’interface Adobe Target de l’écran Configuration > Implémentation > Modifier les paramètres at.js.
* Ont accès à l’interface utilisateur de [Mobile Services et sont familiers avec celle-ci](https://mobilemarketing.adobe.com)
* Disposez d&#39;un IDE pour le développement d&#39;applications mobiles Android. Ce didacticiel présente [Android Studio](https://developer.android.com/studio/install) en différentes étapes et captures d’écran.

Si vous n’avez pas l’accès requis aux solutions Experience Cloud, contactez votre administrateur Experience Cloud.

En outre, il est supposé que vous connaissez bien le développement Android dans Java. Vous n&#39;avez pas besoin d&#39;être un expert Java pour terminer les leçons, mais vous en obtiendrez plus si vous pouvez lire et comprendre facilement le code.

### Vérifier l&#39;accès à Adobe Target

Cette leçon nécessite l&#39;accès à Adobe Target. Avant de passer aux étapes suivantes, vérifiez que vous avez accès à Adobe Target en procédant comme suit :

1. Connectez-vous au [Adobe Experience Cloud](https://experience.adobe.com/)
1. From the Experience Cloud home screen, click [!DNL Target]:
   ![Écran d’accueil Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Vous devriez accéder à la liste Activités de Adobe Target, comme illustré ci-dessous et vous devriez voir que votre utilisateur dispose d’un accès de niveau Approbateur. Si vous ne parvenez pas à accéder [!DNL Target] ou ne pouvez pas vérifier l’accès au niveau Approbateur, contactez l’un des administrateurs Experience Cloud de votre société, demandez cet accès et reprenez ce didacticiel une fois qu’il a été accordé :

   ![Interface utilisateur Adobe](assets/targetUI_approver.png)

## À propos des leçons

Dans ces leçons, vous allez mettre en oeuvre Adobe Target dans une application de démonstration de voyage appelée &quot;We.Travel&quot; en utilisant votre propre compte Adobe Target. D&#39;ici la fin du tutoriel, vous diffuserez des messages personnalisés à l&#39;utilisateur en fonction de leur utilisation de l&#39;application ! Les expériences de personnalisation finale se présenteront comme suit :

![Fin de l&#39;application We.Travel](assets/overview_final_result.jpg)

Après avoir parcouru l&#39;implémentation dans l&#39;application We.Travel, vous pourrez début en utilisant [!DNL Target] votre propre application mobile.

Commençons !

**[SUIVANT : &quot;Télécharger et mettre à jour l’exemple d’application&quot; >](download-and-update-the-sample-app.md)**
