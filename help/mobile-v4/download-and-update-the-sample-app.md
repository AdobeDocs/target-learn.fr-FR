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
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '479'
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

  ![Ouvrir l’écran ](assets/wetravel_homeScreen.png)![ confirmation de l’application](assets/wetravel_confirmationScreen.png)

## Vérifier et mettre à jour les paramètres SDK de Mobile Services pour [!DNL Target]

Le SDK Adobe Mobile Services a été préinstallé dans l’application We.Travel [conformément à la documentation](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=fr). Vous allez maintenant mettre à jour l’installation pour pointer vers votre propre compte [!DNL Target].

Créez tout d’abord une application dans l’interface utilisateur de Mobile Services :

1. Connectez-vous à l’interface [Adobe Mobile Services](https://mobilemarketing.adobe.com/).
1. Accédez à la [!UICONTROL Manage Apps], puis cliquez sur **[!UICONTROL Add]** pour ajouter une nouvelle application à utiliser avec ce tutoriel (**[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**).
1. Choisissez une suite de rapports Analytics avec des données hors production, attribuez un nom à l’application, sélectionnez le type de **[!UICONTROL Standard]** et cliquez sur **[!UICONTROL Save]**.
1. Une fois l’application ajoutée, ajoutez votre code client [!DNL Target] à l’écran suivant de la section [!UICONTROL SDK Target Options] (vous pouvez trouver votre code client dans l’interface [!DNL Target] sous **[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]**, en regard du bouton Télécharger le `at.js` ).
1. Le paramètre [!UICONTROL Request Timeout] détermine la durée pendant laquelle l’application attend la réponse du serveur [!DNL Target] avant d’exécuter les instructions de temporisation. Laissez simplement le paramètre par défaut.
1. Activez la [!UICONTROL Visitor ID Service] et assurez-vous que la [!UICONTROL Organization] est sélectionnée dans la liste déroulante.
1. Enregistrez vos modifications en cliquant sur **[!UICONTROL Save]** en haut à droite de la fenêtre (et non sur celle de la section [!UICONTROL Universal Links], Options de [!UICONTROL App Links] ou [!UICONTROL Push Services] ).
1. Faites défiler jusqu’à la section Téléchargements d’App SDK au bas de la page et téléchargez le fichier de configuration :

   ![Télécharger le fichier de configuration](assets/config_file.jpg)

1. Remplacez le fichier `ADBMobileConfig.json` dans le dossier des ressources du projet Android Studio (app > src > main > assets).

1. Ouvrez maintenant le fichier `ADBMobileConfig.json` et assurez-vous qu’il contient les modifications attendues telles que votre code client [!DNL Target] et vos détails Analytics :
   ![Télécharger le fichier de configuration](assets/client_code.jpg)

Si vos paramètres ne s’affichent pas, vérifiez que vous avez cliqué sur le bouton droit de la **[!UICONTROL Save]** dans l’interface [!UICONTROL Mobile Services] et que vous avez copié le fichier à l’emplacement approprié.

Félicitations ! Vous avez mis à jour le SDK avec les détails de votre compte [!DNL Target]. Nous effectuerons une validation supplémentaire de la configuration après avoir ajouté [!DNL Target] requêtes dans la leçon suivante.

**[NEXT : « Ajouter des requêtes Target » >](add-requests.md)**
