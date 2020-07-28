---
title: Téléchargement et mise à jour de l’exemple d’application We.Travel
seo-title: Téléchargez l’exemple d’application et vérifiez le SDK des services mobiles.
description: 'L’exemple d’application We.Travel est préimplémenté avec le Adobe Mobile Services SDK v4. Il vous suffit de le mettre à jour pour qu''il pointe vers votre propre organisation Experience Cloud et vos comptes de solution.   '
seo-description: L’exemple d’application We.Travel est préimplémenté avec le Adobe Mobile Services SDK v4. Il vous suffit de le mettre à jour pour qu'il pointe vers votre propre organisation Experience Cloud et vos comptes de solution.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Téléchargement et mise à jour de l’exemple d’application We.Travel

L’exemple d’application We.Travel est préimplémenté avec le Adobe Mobile Services SDK v4. Il vous suffit de le mettre à jour pour qu&#39;il pointe vers votre propre organisation Experience Cloud et vos comptes de solution.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pourrez :

* Téléchargement et ouverture de l’exemple d’application We.Travel dans Android Studio
* Vérification et mise à jour des paramètres du SDK Mobile Services pour [!DNL Target]

## Téléchargement de l’application Web.Travel

* Téléchargez le [fichier sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Décompresser le fichier zip
* Ouvrez l’application dans Android Studio en tant que projet existant (ignorez les erreurs relatives au &quot;mappage racine VCS non valide&quot;).
* Exécutez l’application dans un émulateur pour vérifier que l’application est générée et que l’écran d’accueil s’affiche.
* Parcourez l&#39;application et vérifiez que vous pouvez effectuer le processus de réservation (sélectionnez une option de paiement et cliquez simplement sur &quot;Continuer&quot; pour passer en revue l&#39;écran de facturation !)

   ![Ouvrez l’écran](assets/wetravel_homeScreen.png)![appConfirmation.](assets/wetravel_confirmationScreen.png)

## Vérification et mise à jour des paramètres du SDK Mobile Services pour [!DNL Target]

L’Adobe Mobile Services SDK a été préinstallé dans l’application We.Travel [conformément à la documentation](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). Vous allez maintenant mettre à jour l&#39;installation pour pointer vers votre propre [!DNL Target] compte.

Tout d’abord, créez une application dans l’interface utilisateur de Mobile Services :

1. Log in to the [Adobe Mobile Services interface](https://mobilemarketing.adobe.com).
1. Accédez à [!UICONTROL Gérer les applications], puis cliquez sur **[!UICONTROL Ajouter]** pour ajouter une nouvelle application à utiliser avec ce didacticiel (**[!UICONTROL Gérer les applications]** > **[!UICONTROL Ajouter).]**
1. Choisissez une suite de rapports Analytics contenant des données hors production, attribuez un nom à l’application, sélectionnez le type **[!UICONTROL Standard]** et cliquez sur **[!UICONTROL Enregistrer]**.
1. Une fois l’application ajoutée, ajoutez votre code [!DNL Target] client dans l’écran suivant de la section Options [!UICONTROL de Cible du] SDK (vous trouverez votre code client dans l’ [!DNL Target] interface sous **[!UICONTROL Configuration]** > **[!UICONTROL Implémentation > Modifier les paramètres, en regard du bouton Télécharger le ).]******`at.js`
1. Le paramètre [!UICONTROL Request Timeout] détermine la durée pendant laquelle l’application attend la réponse du [!DNL Target] serveur avant d’exécuter les instructions d’expiration. Il vous suffit de laisser le paramètre par défaut.
1. Activez le service [!UICONTROL d’identification des] Visiteurs et assurez-vous que votre [!UICONTROL organisation] est sélectionnée dans la liste déroulante.
1. Enregistrez vos modifications en cliquant sur **[!UICONTROL Enregistrer]** dans le coin supérieur droit de la fenêtre (et non dans la section Liens universels, liens [!UICONTROL d’] application ou Services [!UICONTROL Push).]
1. Accédez à la section Téléchargements du SDK de l’application au bas de la page et téléchargez le fichier de configuration :

   ![Téléchargement du fichier de configuration](assets/config_file.jpg)

1. Remplacez le `ADBMobileConfig.json` fichier dans le dossier des ressources du projet Android Studio (application > src > main > assets).

1. Ouvrez maintenant le `ADBMobileConfig.json` fichier et assurez-vous qu’il contient les modifications attendues, telles que votre code [!DNL Target] client et vos détails Analytics :
   ![Téléchargement du fichier de configuration](assets/client_code.jpg)

Si vos paramètres ne s’affichent pas, vérifiez que vous avez cliqué sur le bouton **[!UICONTROL Enregistrer]** approprié dans l’interface [!UICONTROL Mobile Services] et que vous avez copié le fichier à l’emplacement approprié.

Félicitations ! Vous avez mis à jour le SDK avec les détails de votre [!DNL Target] compte ! Nous procéderons à une validation supplémentaire de la configuration après avoir ajouté [!DNL Target] des requêtes dans la leçon suivante.

**[SUIVANT : &quot;Ajouter les demandes de Cible&quot; >](add-requests.md)**
