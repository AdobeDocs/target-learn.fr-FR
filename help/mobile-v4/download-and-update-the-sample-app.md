---
title: Téléchargement et mise à jour de l’application d’exemple We.Travel
description: 'L’exemple d’application We.Travel est préimplémenté avec le SDK Mobile Services Adobe v4. Vous devez simplement le mettre à jour afin qu’il pointe vers vos propres comptes d’organisation Experience Cloud et de solution.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: a6b645b6d9693a4c8882fd47ee0d61698c0b834d
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Téléchargement et mise à jour de l’application d’exemple We.Travel

L’exemple d’application We.Travel est préimplémenté avec le SDK Mobile Services Adobe v4. Il vous suffit de le mettre à jour afin qu’il pointe vers votre propre organisation Experience Cloud et vos propres comptes de solution.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Télécharger et ouvrir l’exemple d’application We.Travel dans Android Studio
* Vérifiez et mettez à jour les paramètres du SDK Mobile Services pour [!DNL Target]

## Téléchargement de l’application We.Travel

* Téléchargez [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Décompresser le fichier zip
* Ouvrez l’application dans Android Studio en tant que projet existant (ignorez les erreurs relatives au &quot;mappage racine VCS non valide&quot;).
* Exécutez l’application dans un émulateur pour confirmer que l’application est créée et que l’écran d’accueil s’affiche.
* Parcourez l’application et vérifiez que vous pouvez terminer le processus de réservation (sélectionnez une option de paiement et appuyez simplement sur &quot;Continuer&quot; pour passer l’écran de facturation !)

   ![Ouvrez l’écran ](assets/wetravel_homeScreen.png)![appConfirmation .](assets/wetravel_confirmationScreen.png)

## Vérifiez et mettez à jour les paramètres du SDK Mobile Services pour [!DNL Target]

Le SDK Adobe Mobile Services a été préinstallé dans l’application We.Travel [selon la documentation ](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en). Vous allez maintenant mettre à jour l’installation pour pointer vers votre propre compte [!DNL Target].

Tout d’abord, créez une application dans l’interface utilisateur de Mobile Services :

1. Connectez-vous à l’[interface Adobe Mobile Services](https://mobilemarketing.adobe.com).
1. Accédez à [!UICONTROL Gérer les applications], puis cliquez sur **[!UICONTROL Ajouter]** pour ajouter une nouvelle application à utiliser avec ce tutoriel (**[!UICONTROL Gérer les applications]** > **[!UICONTROL Ajouter]**).
1. Choisissez une suite de rapports Analytics avec des données hors production, attribuez un nom à l’application, sélectionnez le type **[!UICONTROL Standard]** et cliquez sur **[!UICONTROL Enregistrer]**.
1. Une fois l’application ajoutée, ajoutez votre [!DNL Target] code client sur l’écran suivant de la section [!UICONTROL Options Target du SDK] (vous trouverez votre code client dans l’interface [!DNL Target] sous **[!UICONTROL Configuration]** > **[!UICONTROL Implémentation]** **[!UICONTROL Modifier les paramètres]**, en regard de Télécharger `at.js`).
1. Le paramètre [!UICONTROL Délai d’expiration de la requête] détermine la durée pendant laquelle l’application attend la réponse du serveur [!DNL Target] avant d’exécuter les instructions d’expiration. Laissez simplement le paramètre par défaut.
1. Activez le [!UICONTROL service d’identification des visiteurs] et assurez-vous que votre [!UICONTROL organisation] est sélectionnée dans la liste déroulante.
1. Enregistrez vos modifications en cliquant sur **[!UICONTROL Enregistrer]** dans le coin supérieur droit de la fenêtre (et non sur celui des options [!UICONTROL Liens universels], [!UICONTROL Liens d’application] ou [!UICONTROL Services push] ).
1. Accédez à la section Téléchargements du SDK de l’application au bas de la page et téléchargez le fichier de configuration :

   ![Téléchargement du fichier de configuration](assets/config_file.jpg)

1. Remplacez le fichier `ADBMobileConfig.json` dans le dossier des ressources de votre projet Android Studio (application > src > main > ressources).

1. Ouvrez maintenant le fichier `ADBMobileConfig.json` et assurez-vous qu’il contient les modifications attendues, telles que votre [!DNL Target] code client et vos détails Analytics :
   ![Téléchargement du fichier de configuration](assets/client_code.jpg)

Si vos paramètres ne s’affichent pas, vérifiez que vous avez cliqué sur le bouton **[!UICONTROL Enregistrer]** approprié dans l’interface [!UICONTROL Mobile Services] et que vous avez copié le fichier à l’emplacement approprié.

Félicitations ! Vous avez mis à jour le SDK avec les détails de votre compte [!DNL Target]. Nous allons effectuer une validation supplémentaire de la configuration après avoir ajouté des requêtes [!DNL Target] dans la leçon suivante.

**[SUIVANT : &quot;Ajout de requêtes Target&quot; >](add-requests.md)**
