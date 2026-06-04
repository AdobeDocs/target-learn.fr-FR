---
title: Télécharger et mettre à jour l’exemple d’application We.Travel
description: L’exemple d’application We.Travel est préimplémenté avec Adobe Mobile Services SDK v4. Il vous suffit de le mettre à jour pour qu’il pointe vers vos propres comptes d’organisation et de solution Experience Cloud.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
TQID: https://experienceleague.adobe.com/23TuO5OZXkf9TDWMgIEXyu2Hx9f3dzI1n91u7A1Wix0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 530
ht-degree: 0%

---

# Télécharger et mettre à jour l’exemple d’application We.Travel

L’exemple d’application We.Travel est préimplémenté avec Adobe Mobile Services SDK v4. Il vous suffit de le mettre à jour, de sorte qu’il pointe vers vos propres comptes d’organisation et de solution Experience Cloud.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Téléchargez et ouvrez l’exemple d’application We.Travel dans Android Studio
* Vérifier et mettre à jour les paramètres SDK de Mobile Services pour [!DNL Target]

## Télécharger l’application We.Travel

* Téléchargez le fichier [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Décompresser le fichier zip
* Ouvrez l’application dans Android Studio en tant que projet existant (ignorez les erreurs relatives au « Mappage racine VCS non valide »).
* Exécutez l’application dans un émulateur pour confirmer que l’application se crée et que vous pouvez voir l’écran d’accueil
* Parcourez l&#39;application et vérifiez que vous pouvez terminer le processus de réservation (sélectionnez n&#39;importe quelle option de paiement et appuyez simplement sur « Continuer » pour passer sur l&#39;écran de facturation !)

  ![Ouvrir l’écran &#x200B;](assets/wetravel_homeScreen.png)![&#x200B; confirmation de l’application](assets/wetravel_confirmationScreen.png)

## Vérifier et mettre à jour les paramètres SDK de Mobile Services pour [!DNL Target]

Le SDK Adobe Mobile Services a été préinstallé dans l’application We.Travel [conformément à la documentation](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en). Vous allez maintenant mettre à jour l’installation pour pointer vers votre propre compte [!DNL Target].

Créez tout d’abord une application dans l’interface utilisateur de Mobile Services :

1. Connectez-vous à l’interface [Adobe Mobile Services](https://mobilemarketing.adobe.com/).
1. Accédez à la [!UICONTROL Gérer les applications], puis cliquez sur **[!UICONTROL Ajouter]** pour ajouter une nouvelle application à utiliser avec ce tutoriel (**[!UICONTROL Gérer les applications]** > **[!UICONTROL Ajouter]**).
1. Choisissez une suite de rapports Analytics avec des données hors production, attribuez un nom à l’application, sélectionnez le type **[!UICONTROL Standard]** et cliquez sur **[!UICONTROL Enregistrer]**.
1. Une fois l’application ajoutée, ajoutez votre code client [!DNL Target] à l’écran suivant dans la section [!UICONTROL Options de SDK Target] (vous trouverez votre code client dans l’interface [!DNL Target] sous **[!UICONTROL Configuration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Modifier les paramètres]**, en regard du bouton Télécharger le `at.js` ).
1. Le paramètre [!UICONTROL Délai d’expiration de la requête] détermine la durée pendant laquelle l’application attend la réponse du serveur [!DNL Target] avant d’exécuter les instructions de délai d’expiration. Laissez simplement le paramètre par défaut.
1. Activez le [!UICONTROL service d’identification des visiteurs] et assurez-vous que votre [!UICONTROL organisation] est sélectionnée dans la liste déroulante.
1. Enregistrez vos modifications en cliquant sur **[!UICONTROL Enregistrer]** en haut à droite de la fenêtre (et non sur celui de la section [!UICONTROL Liens universels], [!UICONTROL Liens d’application] ou [!UICONTROL Services push]).
1. Faites défiler jusqu’à la section Téléchargements d’App SDK au bas de la page et téléchargez le fichier de configuration :

   ![Télécharger le fichier de configuration](assets/config_file.jpg)

1. Remplacez le fichier `ADBMobileConfig.json` dans le dossier des ressources du projet Android Studio (app > src > main > assets).

1. Ouvrez maintenant le fichier `ADBMobileConfig.json` et assurez-vous qu’il contient les modifications attendues telles que votre code client [!DNL Target] et vos détails Analytics :
   ![Télécharger le fichier de configuration](assets/client_code.jpg)

Si vos paramètres ne s’affichent pas, confirmez que vous avez cliqué sur le bouton droit **[!UICONTROL Enregistrer]** dans l’interface [!UICONTROL Mobile Services] et que vous avez copié le fichier à l’emplacement approprié.

Félicitations ! Vous avez mis à jour le SDK avec les détails de votre compte [!DNL Target]. Nous effectuerons une validation supplémentaire de la configuration après avoir ajouté [!DNL Target] requêtes dans la leçon suivante.

**[NEXT : « Ajouter des requêtes Target » >](add-requests.md)**
