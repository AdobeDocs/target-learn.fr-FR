---
title: Adobe Target avec Adobe Mobile Services SDK v4 pour Android
description: Adobe Target avec Adobe Mobile Services SDK v4 pour Android est le point de départ idéal pour les développeurs Android qui utilisent déjà Adobe Mobile Services SDK v4 et souhaitent début de la personnalisation des expériences d’application avec Adobe Target.
role: Développeur
level: Intermédiaire
topic: Mobile, personnalisation
feature: Mise en oeuvre de Mobile, présentation
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# Adobe Target avec Adobe Mobile Services SDK v4 pour Android - Présentation

_Adobe Target avec Adobe Mobile Services SDK v4 pour_ Android est le point de départ idéal pour les développeurs Android qui utilisent déjà Adobe Mobile Services SDK v4 et souhaitent début de la personnalisation des expériences d’application avec Adobe Target.

Une application de démonstration Android vous permet de suivre les cours. Après avoir suivi ce didacticiel, vous devriez être prêt à début à mettre en oeuvre [!DNL Target] dans votre propre application Android !

Après avoir terminé cet didacticiel, vous serez en mesure de :

* Validation de la configuration du [Adobe Mobile Services SDK](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html)
* Mettez en oeuvre les types de requêtes [!DNL Target] suivants :
   * Prélecture du contenu [!DNL Target]
   * Traiter plusieurs [!DNL Target] emplacements (mbox) dans une seule requête
   * Blocage des requêtes (s’exécute avant l’affichage de l’application)
   * Demandes non bloquées (s’exécute en arrière-plan)
   * Temps réel (sans mise en cache)
   * Récupération en mémoire cache
* Ajouter des paramètres aux demandes de personnalisation améliorée
* Créer des audiences et des offres
* Personnalisation des mises en page
* Mise en service de nouvelles fonctionnalités avec indicateur de fonctionnalité

## Conditions préalables

Dans ces leçons, on suppose que vous :

* Disposer d’un ID d’Adobe et d’un accès de niveau approbateur à l’interface Adobe Target (voir les étapes de vérification ci-dessous)
* Connaissez votre code client Adobe Target afin que vous puissiez envoyer des requêtes à votre propre compte. Le code client s’affiche dans l’interface Adobe Target de la section   Configuration > Implémentation > Écran Modifier les paramètres at.js
* Ont accès à [l&#39;interface utilisateur de Mobile Services](https://mobilemarketing.adobe.com) et sont familières avec cette interface utilisateur
* Disposez d&#39;un IDE pour le développement d&#39;applications mobiles Android. Ce didacticiel présente [Android Studio](https://developer.android.com/studio/install) en différentes étapes et captures d’écran.

Si vous n’avez pas l’accès requis aux solutions Experience Cloud, contactez votre administrateur Experience Cloud.

En outre, il est supposé que vous connaissez bien le développement Android dans Java. Vous n&#39;avez pas besoin d&#39;être un expert Java pour terminer les leçons, mais vous en obtiendrez plus si vous pouvez lire et comprendre facilement le code.

### Vérifier l&#39;accès à Adobe Target

Cette leçon nécessite l&#39;accès à Adobe Target. Avant de passer aux étapes suivantes, vérifiez que vous avez accès à Adobe Target en procédant comme suit :

1. Connectez-vous au [Adobe Experience Cloud](https://experience.adobe.com/)
1. Dans l’écran d’accueil de l’Experience Cloud, cliquez sur [!DNL Target] :
   ![Écran d’accueil Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Vous devriez accéder à la liste Activités de Adobe Target, comme illustré ci-dessous et vous devriez voir que votre utilisateur dispose d’un accès de niveau Approbateur. Si vous ne parvenez pas à accéder à [!DNL Target] ou ne pouvez pas vérifier l’accès au niveau Approbateur, contactez l’un des administrateurs Experience Cloud de votre société, demandez cet accès et reprenez ce didacticiel une fois qu’il a été accordé :

   ![Interface utilisateur Adobe](assets/targetUI_approver.png)

## À propos des leçons

Dans ces leçons, vous allez mettre en oeuvre Adobe Target dans une application de démonstration de voyage appelée &quot;We.Travel&quot; en utilisant votre propre compte Adobe Target. D&#39;ici la fin du tutoriel, vous diffuserez des messages personnalisés à l&#39;utilisateur en fonction de leur utilisation de l&#39;application ! Les expériences de personnalisation finale se présenteront comme suit :

![Fin de l&#39;application We.Travel](assets/overview_final_result.jpg)

Après avoir parcouru l&#39;implémentation dans l&#39;application We.Travel, vous pourrez début en utilisant [!DNL Target] dans votre propre application mobile.

Commençons !

**[SUIVANT : &quot;Télécharger et mettre à jour l’exemple d’application&quot; >](download-and-update-the-sample-app.md)**
