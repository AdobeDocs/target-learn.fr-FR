---
title: Téléchargement et mise à jour de l’exemple d’application We.Travel
description: 'L’exemple d’application We.Travel est préimplémenté avec le Adobe Mobile Services SDK v4. Il vous suffit de le mettre à jour pour qu''il pointe vers votre propre organisation Experience Cloud et vos comptes de solution.   '
role: Développeur
level: Intermédiaire
topic: Mobile, personnalisation
feature: Mise en oeuvre de Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Téléchargement et mise à jour de l’exemple d’application We.Travel

L’exemple d’application We.Travel est préimplémenté avec le Adobe Mobile Services SDK v4. Il vous suffit de le mettre à jour pour qu&#39;il pointe vers votre propre organisation Experience Cloud et vos comptes de solution.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pourrez :

* Téléchargement et ouverture de l’exemple d’application We.Travel dans Android Studio
* Vérification et mise à jour des paramètres du SDK Mobile Services pour [!DNL Target]

## Téléchargement de l’application Web.Travel

* Téléchargez le fichier [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Décompresser le fichier zip
* Ouvrez l’application dans Android Studio en tant que projet existant (ignorez les erreurs relatives au &quot;mappage racine VCS non valide&quot;).
* Exécutez l’application dans un émulateur pour vérifier que l’application est générée et que l’écran d’accueil s’affiche.
* Parcourez l&#39;application et vérifiez que vous pouvez effectuer le processus de réservation (sélectionnez une option de paiement et cliquez simplement sur &quot;Continuer&quot; pour ignorer l&#39;écran de facturation !)

   ![Ouvrez l’écran ](assets/wetravel_homeScreen.png)![appConfirmation.](assets/wetravel_confirmationScreen.png)

## Vérification et mise à jour des paramètres du SDK Mobile Services pour [!DNL Target]

L’Adobe Mobile Services SDK a été préinstallé dans l’application We.Travel [conformément à la documentation](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). Vous allez maintenant mettre à jour l&#39;installation pour pointer vers votre propre compte [!DNL Target].

Tout d’abord, créez une application dans l’interface utilisateur de Mobile Services :

1. Connectez-vous à l&#39;[interface Adobe Mobile Services](https://mobilemarketing.adobe.com).
1. Accédez à [!UICONTROL Gérer les applications], puis cliquez sur **[!UICONTROL Ajouter]** pour ajouter une nouvelle application à utiliser avec ce didacticiel (**[!UICONTROL Gérer les applications]** > **[!UICONTROL Ajouter]**).
1. Choisissez une suite de rapports Analytics avec des données autres que celles de production, attribuez un nom à l’application, sélectionnez le type **[!UICONTROL Standard]** et cliquez sur **[!UICONTROL Enregistrer]**.
1. Une fois l’application ajoutée, ajoutez votre [!DNL Target] code client dans l’écran suivant de la section [!UICONTROL Options de Cible du SDK] (vous trouverez votre code client dans l’interface [!DNL Target] sous **[!UICONTROL Configuration]** > **[!UICONTROL Implémentation]** > **[!UICONTROL Modifier les paramètres]**, en regard du téléchargement &lt;a &lt;a 0/>).`at.js`
1. Le paramètre [!UICONTROL Délai d’expiration de la demande] détermine la durée pendant laquelle l’application attend la réponse du serveur [!DNL Target] avant d’exécuter les instructions d’expiration. Il vous suffit de laisser le paramètre par défaut.
1. Activez le [!UICONTROL service d’identification des Visiteurs] et assurez-vous que votre [!UICONTROL organisation] est sélectionnée dans la liste déroulante.
1. Enregistrez vos modifications en cliquant sur **[!UICONTROL Enregistrer]** dans le coin supérieur droit de la fenêtre (et non sur celui de la section [!UICONTROL Liens universels], [!UICONTROL Liens d’application] ou [!UICONTROL Services Push]).
1. Accédez à la section Téléchargements du SDK de l’application au bas de la page et téléchargez le fichier de configuration :

   ![Téléchargement du fichier de configuration](assets/config_file.jpg)

1. Remplacez le fichier `ADBMobileConfig.json` dans le dossier des ressources du projet Android Studio (application > src > main > assets).

1. Ouvrez maintenant le fichier `ADBMobileConfig.json` et assurez-vous qu’il contient les modifications attendues, telles que votre code client [!DNL Target] et vos détails Analytics :
   ![Téléchargement du fichier de configuration](assets/client_code.jpg)

Si vos paramètres ne s’affichent pas, vérifiez que vous avez cliqué sur le bouton droit **[!UICONTROL Enregistrer]** dans l’interface [!UICONTROL Mobile Services] et que vous avez copié le fichier à l’emplacement approprié.

Félicitations ! Vous avez mis à jour le SDK avec vos [!DNL Target] détails de compte ! Nous procéderons à une validation supplémentaire de la configuration après avoir ajouté des requêtes [!DNL Target] dans la leçon suivante.

**[SUIVANT : &quot;Demandes de Cible d’Ajoute&quot; >](add-requests.md)**
