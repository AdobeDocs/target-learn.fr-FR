---
title: Téléchargement et mise à jour de l’application d’exemple We.Travel
description: L’exemple d’application We.Travel est préimplémenté avec le SDK Mobile Services Adobe v4. Vous devez simplement le mettre à jour afin qu’il pointe vers vos propres comptes d’organisation Experience Cloud et de solution.
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

# Téléchargement et mise à jour de l’application d’exemple We.Travel

L’exemple d’application We.Travel est préimplémenté avec le SDK Mobile Services Adobe v4. Il vous suffit de le mettre à jour afin qu’il pointe vers votre propre organisation Experience Cloud et vos propres comptes de solution.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Télécharger et ouvrir l’exemple d’application We.Travel dans Android Studio
* Vérification et mise à jour des paramètres du SDK Mobile Services pour [!DNL Target]

## Téléchargement de l’application We.Travel

* Téléchargez le fichier [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Décompresser le fichier zip
* Ouvrez l’application dans Android Studio en tant que projet existant (ignorez les erreurs concernant le &quot;mappage racine VCS non valide&quot;).
* Exécutez l’application dans un émulateur pour confirmer que l’application est créée et que l’écran d’accueil s’affiche.
* Parcourez l’application et vérifiez que vous pouvez terminer le processus de réservation (sélectionnez une option de paiement et appuyez simplement sur &quot;Continuer&quot; pour passer l’écran de facturation !)

  ![ Ouvrez l’application ](assets/wetravel_homeScreen.png)![Ecran de confirmation](assets/wetravel_confirmationScreen.png)

## Vérification et mise à jour des paramètres du SDK Mobile Services pour [!DNL Target]

Le SDK Mobile Services Adobe a été préinstallé dans l’application We.Travel [, conformément à la documentation ](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en). Vous allez maintenant mettre à jour l&#39;installation pour pointer vers votre propre compte [!DNL Target].

Tout d’abord, créez une application dans l’interface utilisateur de Mobile Services :

1. Connectez-vous à l’ [interface Adobe Mobile Services](https://mobilemarketing.adobe.com/).
1. Accédez à [!UICONTROL Manage Apps], puis cliquez sur **[!UICONTROL Add]** pour ajouter une nouvelle application à utiliser avec ce tutoriel (**[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**).
1. Choisissez une suite de rapports Analytics avec des données hors production, attribuez un nom à l’application, sélectionnez le type **[!UICONTROL Standard]** et cliquez sur **[!UICONTROL Save]**.
1. Une fois l’application ajoutée, ajoutez votre code client [!DNL Target] sur l’écran suivant de la section [!UICONTROL SDK Target Options] (vous trouverez votre code client dans l’interface [!DNL Target] sous **[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]**, en regard du bouton Télécharger `at.js` ).
1. Le paramètre [!UICONTROL Request Timeout] détermine la durée pendant laquelle l’application attend la réponse du serveur [!DNL Target] avant d’exécuter les instructions d’expiration. Laissez simplement le paramètre par défaut.
1. Activez le [!UICONTROL Visitor ID Service] et assurez-vous que votre [!UICONTROL Organization] est sélectionné dans la liste déroulante.
1. Enregistrez vos modifications en cliquant sur **[!UICONTROL Save]** dans le coin supérieur droit de la fenêtre (et non sur celui des options [!UICONTROL Universal Links], [!UICONTROL App Links] ou [!UICONTROL Push Services] ).
1. Accédez à la section Téléchargements du SDK de l’application au bas de la page et téléchargez le fichier de configuration :

   ![Télécharger le fichier de configuration](assets/config_file.jpg)

1. Remplacez le fichier `ADBMobileConfig.json` dans le dossier des ressources de votre projet Android Studio (application > src > main > ressources).

1. Ouvrez maintenant le fichier `ADBMobileConfig.json` et assurez-vous qu’il contient les modifications attendues, telles que votre code client [!DNL Target] et vos détails Analytics :
   ![Télécharger le fichier de configuration](assets/client_code.jpg)

Si vos paramètres ne s’affichent pas, vérifiez que vous avez cliqué sur le bouton **[!UICONTROL Save]** approprié dans l’interface [!UICONTROL Mobile Services] et que vous avez copié le fichier à l’emplacement correct.

Félicitations ! Vous avez mis à jour le SDK avec les détails de votre compte [!DNL Target] ! Nous allons effectuer une validation supplémentaire de la configuration après avoir ajouté [!DNL Target] requêtes dans la leçon suivante.

**[NEXT : &quot;Ajouter des requêtes Target&quot; >](add-requests.md)**
