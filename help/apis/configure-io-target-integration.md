---
title: Configuration de l’authentification pour les API Adobe Target
description: Ce tutoriel guide les développeurs à travers les étapes requises pour générer les jetons d’authentification nécessaires pour interagir avec les API Adobe Target. Suivez ces étapes pour utiliser Adobe Developer Console afin de générer et de tester le jeton d’accès porteur, nécessaire pour utiliser les API Target.
role: Developer, Admin, Architect
level: Intermediate
topic: Personnalisation, administration, intégrations, développement
feature: API/SDK, administration et configuration
doc-type: tutorial
kt: null
thumbnail: null
author: Judy Kim
exl-id: 8a1e93e4-67b2-4942-a8da-fc0f2cbb2df2
source-git-commit: ee9aac0144e35abf32c5d8eafe10a013bf30d8d3
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 2%

---

# Configuration de l’authentification pour les API Adobe Target

Les API d’administration d’Adobe Target, y compris les [!DNL Recommendations] API d’administration, sont sécurisées par une authentification afin de s’assurer que seuls les utilisateurs autorisés les utilisent pour accéder à Adobe Target. Utilisez [Adobe Developer Console](https://console.adobe.io/) pour gérer cette authentification pour toutes les solutions Adobe Experience Cloud, y compris [!DNL Target].

Cette leçon décrit les étapes préliminaires nécessaires à la génération des jetons d’authentification nécessaires pour interagir avec les API Adobe Target. Dans les sections qui suivent, vous allez :

1. Créez un projet (précédemment appelé intégration) dans Adobe Developer Console.
2. Exportez les détails du projet vers Postman.
3. Générez un jeton d’accès au porteur.
4. Testez le jeton d’accès au porteur.

## Conditions préalables

| Ressource | Détails |
| --- | --- |
| Postman | Pour réussir ces étapes, obtenez l’[application Postman](https://www.postman.com/downloads/) correspondant à votre système d’exploitation. Postman basic est gratuit avec la création de compte. Bien qu’il ne soit pas nécessaire pour utiliser les API Adobe Target en général, Postman facilite les processus d’API et Adobe Target fournit plusieurs collections Postman pour aider à exécuter ses API et apprendre à les utiliser. Le reste de ce tutoriel repose sur des connaissances opérationnelles de Postman. Pour obtenir de l’aide, reportez-vous à la [documentation Postman](https://learning.getpostman.com/). |
| Références | Toute la suite de ce tutoriel vous familiarisera avec les ressources suivantes :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation sur Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentation de l’API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Création d’un projet d’Adobe I/O

Dans cette section, vous accédez à Adobe Developer Console et créez un projet pour [!DNL Adobe Target]. Pour plus d’informations, consultez la [documentation sur les projets](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. Dans [Adobe Admin Console](https://adminconsole.adobe.com/), assurez-vous que votre compte utilisateur d’Adobe a reçu un accès de niveau [Administrateur de produit](https://helpx.adobe.com/enterprise/using/admin-roles.html) et [Développeur](https://helpx.adobe.com/enterprise/using/manage-developers.html) à [!DNL Target].

2. Dans [Adobe Developer Console](https://console.adobe.io/), sélectionnez l’organisation Experience Cloud pour laquelle vous souhaitez créer cette intégration. (Notez qu’il est probable que vous n’ayez accès qu’à une seule organisation Experience Cloud.)

   ![configure-io-target-create-project2.png](assets/configure-io-target-createproject2.png)

3. Cliquez sur **[!UICONTROL Créer un projet]**.

   ![configure-io-target-create-project3.png](assets/configure-io-target-createproject3.png)

4. Cliquez sur **[!UICONTROL Ajouter une API]** pour ajouter une API REST à votre projet afin d’accéder aux services et produits Adobe.

   ![Ajout d’une API](assets/configure-io-target-createproject4.png)

5. Sélectionnez **[!DNL Adobe Target]** comme service d’Adobe avec lequel vous souhaitez intégrer. Cliquez sur le bouton **[!UICONTROL Suivant]** qui s’affiche.

   ![configure-io-target-create project5](assets/configure-io-target-createproject5.png)

6. Sélectionnez une option pour associer des clés publiques et privées à l’intégration du compte de service que vous créez pour Target. Pour ce tutoriel, sélectionnez **[!UICONTROL Option 1 : Générez une paire de clés]** et cliquez sur **[!UICONTROL Générer la paire de clés]**.
   ![configure-io-target-create-project6](assets/configure-io-target-createproject6.png)

7. Notez les résultats ! Comme indiqué, notez le fichier de configuration automatiquement téléchargé (`config`), qui contient votre clé privée. Cliquez sur **[!UICONTROL Suivant]**.
   ![configure-io-target-create-project7](assets/configure-io-target-createproject7.png)
8. Dans votre système de fichiers, vérifiez l’emplacement de `config`, qui est le fichier de configuration compressé créé à l’étape précédente. Encore une fois, ce fichier `config` contient votre clé privée, dont vous aurez besoin ultérieurement. L’emplacement exact de votre système de fichiers peut différer de celui illustré ici.
   ![configure-io-target-create-project8](assets/configure-io-target-createproject8.png)
9. De retour dans Adobe Developer Console, sélectionnez le [profil(s) de produit](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) correspondant aux propriétés dans lesquelles vous utilisez [!DNL Recommendations]. (Si vous n’utilisez pas de propriétés, sélectionnez l’option Espace de travail par défaut .) Cliquez sur **[!UICONTROL Enregistrer l’API configurée]**.
   ![configure-io-target-create-project9](assets/configure-io-target-createproject9.png)

10. Cliquez sur **[!UICONTROL Créer une intégration]**. Vous devriez recevoir un message temporaire indiquant que votre API a été correctement configurée.

11. Pour terminer, renommez votre projet en un nom plus significatif que le `Project 1` d’origine. Pour ce faire, accédez au projet à l’aide du chemin de navigation comme indiqué, cliquez sur **[!UICONTROL Modifier le projet]** pour accéder au modal **[!UICONTROL Modifier le projet], puis renommez le projet.

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>Dans ce tutoriel, nous nommons notre projet &quot;Intégration de Target&quot;. Si vous prévoyez d’utiliser votre projet pour plus d’informations qu’Adobe Target, vous pouvez le nommer en conséquence. Par exemple, vous pouvez choisir de le nommer &quot;API d’Adobe&quot; ou &quot;API d’Experience Cloud&quot;, car il peut être utilisé avec d’autres solutions dans Adobe Experience Cloud.

## Exportation des détails du projet

Maintenant que vous disposez d’un projet d’Adobe que vous pouvez utiliser pour accéder à [!DNL Target], vous devez vous assurer d’envoyer les détails de ce projet avec vos demandes d’API d’Adobe. Ces détails sont requis pour interagir avec plusieurs API Adobe, y compris plusieurs API [!DNL Target]. Par exemple, les détails de l’intégration incluent les informations d’autorisation et d’authentification requises par les API d’administration [!DNL Target]. Par conséquent, pour utiliser les API avec Postman, vous devez obtenir ces détails dans Postman.

Il existe de nombreuses façons de spécifier les détails de votre projet dans Postman, mais dans cette section, nous profitons de certaines fonctionnalités et collections préconfigurées. Tout d’abord (dans cette section), vous allez exporter les détails de votre intégration dans un environnement Postman. Ensuite (dans la section suivante), vous allez générer un jeton d’accès au porteur pour vous accorder l’accès aux ressources d’Adobe nécessaires.

>[!NOTE]
>
>Pour obtenir des instructions vidéo applicables à toute solution Experience Cloud, y compris [!DNL Target], voir [Utilisation de Postman avec les API Experience Platform](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html). Les sections suivantes concernent les API [!DNL Target] :
>
> 1. Exportation des détails de l’intégration d’Adobe I/O vers Postman
> 2. Génération d’un jeton d’accès avec Postman

>
> 
Ces étapes sont également fournies ci-dessous.

1. Toujours dans [Adobe Developer Console](https://console.adobe.io/), accédez aux **[!UICONTROL informations d’identification du compte de service (JWT)]** de votre nouveau projet. Utilisez le volet de navigation de gauche ou la section **[!UICONTROL Informations d’identification]** comme indiqué.
   ![JWT1](assets/configure-io-target-jwt1.png)
Dans  **[!UICONTROL les détails d’identification]**, notez que vous pouvez afficher votre ou vos clés  **publiques**, votre  **ID client** et d’autres informations relatives à votre compte de service.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Cliquez pour accéder aux informations sur l’API **[!UICONTROL Adobe Target]**. Utilisez le volet de navigation de gauche ou la section **[!UICONTROL Produits et services connectés]** comme indiqué.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Cliquez sur **[!UICONTROL Télécharger pour Postman]** > **[!UICONTROL Compte de service (JWT)]** pour créer un fichier JSON capturant vos informations d’authentification pour un environnement Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)
Notez le fichier JSON dans votre système de fichiers.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. Dans Postman, cliquez sur l’icône représentant un engrenage pour gérer vos environnements, puis cliquez sur **Importer** pour importer le fichier JSON (environnement).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Choisissez votre fichier et cliquez sur **Ouvrir**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. Dans le modal Postman **Manage Environments** (Gérer les environnements), cliquez sur le nom de l’environnement nouvellement importé pour l’inspecter. (Le nom de votre environnement peut être différent de celui illustré ici. Modifiez le nom suivant vos besoins. Il ne doit pas nécessairement correspondre au nom du projet Adobe.)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. Remarque : Les valeurs `CLIENT_SECRET` et `API_KEY` (ainsi que d’autres variables) sont prérenseignées à partir de votre intégration, comme défini dans Adobe Developer Console. (La variable Postman `CLIENT_SECRET` doit correspondre aux informations d’identification de l’Adobe `CLIENT SECRET` affichées dans Developer Console, et `API_KEY` dans Postman doit également correspondre à `CLIENT ID` dans Developer Console.) En revanche, notez `PRIVATE_KEY`, `JWT_TOKEN` et `ACCESS_TOKEN` sont vides. Commençons par fournir la valeur `PRIVATE_KEY`.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**Surprise !**
   >
   >Posez un quiz ! Pouvez-vous vous rappeler où se trouve votre clé privée ?
   >C’est vrai, il se trouve dans le fichier `config` téléchargé précédemment à partir d’Adobe Developer Console !

8. À partir de votre système de fichiers, ouvrez votre fichier `config`, puis ouvrez le fichier de clé `private`.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Sélectionnez et copiez tout le contenu du fichier de clé `private`.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. Dans Postman, collez votre valeur de clé privée dans les champs **VALEUR INITIALE** et **VALEUR ACTUELLE**.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Cliquez sur **[!UICONTROL Mettre à jour]**, puis fermez la fenêtre modale Environnements .


## Génération du jeton d’accès au porteur

Dans cette section, vous générez votre jeton d’accès au porteur, nécessaire pour authentifier votre interaction avec les API Adobe Target. Pour générer votre jeton d’accès au porteur, vous devez envoyer les détails de votre intégration (définis dans les sections précédentes) à [Adobe Identity Management Service (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Il existe plusieurs façons de procéder, mais dans ce tutoriel, vous allez créer une requête POST personnalisée à l’API IMS. Je plaisante. Dans ce tutoriel, nous profitons d’une collection Postman contenant un appel IMS prédéfini qui rend le processus direct et facile. Une fois la collection importée, vous pouvez la réutiliser si nécessaire afin de générer de nouveaux jetons non seulement pour Adobe Target, mais également pour d’autres API d’Adobe.

1. Accédez aux [exemples d’appels de l’API Adobe Identity Management Service](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Cliquez sur la **collection Postman Génération de jetons d’accès aux Adobes I/O**.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Obtenez le fichier JSON brut pour cette collection en cliquant sur **Brut**, puis en copiant le fichier JSON obtenu dans le presse-papiers. (Vous pouvez également enregistrer le fichier JSON brut en tant que fichier .json.)
   ![token3](assets/configure-io-target-generatetoken3.png)
4. Importez la collection dans Postman en la collant et en l’envoyant à partir du Presse-papiers. (Vous pouvez également télécharger le fichier .json que vous avez enregistré.) Cliquez sur **Continue** (Continuer).
   ![token4](assets/configure-io-target-generatetoken4.png)
5. Sélectionnez le **[!UICONTROL IMS : JWT Generate + Auth via User Token]** requête dans la collection Postman Adobe I/O Access Token Generation, vérifiez que votre environnement est sélectionné, puis cliquez sur **Send** pour générer le jeton.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Ce jeton d’accès au porteur sera valide pendant 24 heures. Envoyez à nouveau la requête chaque fois que vous devez générer un nouveau jeton.

6. Ouvrez à nouveau le modal Manage Environments (Gérer les environnements), puis sélectionnez votre environnement.
   ![token6](assets/configure-io-target-jwt11.png)
7. Notez que les valeurs `ACCESS_TOKEN` et `JWT_TOKEN` sont désormais renseignées.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>Q : Dois-je utiliser la collection Postman Adobe I/O Access Token Generation pour générer le jeton Web JSON (JWT) et le jeton d’accès au porteur ?
>
>A : Non ! La collection Postman Adobe I/O Access Token Generation est disponible afin de faciliter la génération du jeton d’accès JWT et du jeton d’accès porteur dans Postman. Vous pouvez également utiliser les fonctionnalités d’ Adobe Developer Console pour générer manuellement le jeton d’accès au porteur.

## Tester le jeton d’accès au porteur

Dans cet exercice, vous utiliserez votre nouveau jeton d’accès au porteur en envoyant une requête API qui récupère une liste des activités de votre compte [!DNL Target]. Une réponse réussie indique que votre projet d’Adobe et votre authentification fonctionnent comme prévu afin d’utiliser l’API.

1. Importez les [API d’administration Adobe Target Collection Postman](https://developers.adobetarget.com/api/#admin-postman-collection). Suivez tous les invites jusqu’à ce que la collection soit importée dans Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Développez la collection et notez la requête **[!UICONTROL Lister les activités]** .
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Notez que les variables telles que `{{access_token}}` ne sont initialement pas résolues. Vous pouvez résoudre ce problème de plusieurs manières différentes (par exemple, vous pouvez définir une nouvelle variable de collection appelée `{{access_token}}`), mais dans ce tutoriel, vous allez modifier la requête d’API afin d’exploiter l’environnement Postman que vous utilisiez précédemment. Cela permettra à l’environnement de continuer à servir de consolidation unique et cohérente de toutes les variables communes à toutes les API Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Saisissez pour remplacer `{{access_token}}` par `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Saisissez pour remplacer `{{api_key}}` par `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Saisissez pour remplacer `{{tenant}}` par `{{TENANT_ID}}`. Remarque : `{{TENANT_ID}}` n’est pas encore reconnu.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Ouvrez le modal Manage Environments (Gérer les environnements), puis sélectionnez votre environnement.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Saisissez pour ajouter une nouvelle variable d’environnement `{{TENANT_ID}}`. Copiez et collez votre valeur d’ID de tenant dans les champs **VALEUR INITIALE** et **VALEUR ACTUELLE** pour votre nouvelle variable d’environnement `TENANT_ID`.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >L’ID de tenant est différent de votre [!DNL Target] `clientcode`. L’ID de tenant existe dans l’URL lorsque vous êtes connecté à [!DNL Target]. Pour obtenir votre ID de tenant, connectez-vous à [!DNL Adobe Experience Cloud], ouvrez [!DNL Target], puis cliquez sur la carte [!DNL Target]. Utilisez la valeur de l’identifiant du client comme indiqué dans le sous-domaine de l’URL.
   >
   >Par exemple, si votre URL lors de la connexion à Adobe Target est
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >alors votre identifiant de tenant est &quot;mycompany&quot;.

1. Envoyez votre requête, après avoir vérifié que vous avez sélectionné l’environnement approprié. Vous devriez recevoir une réponse contenant votre liste d’activités.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

Félicitations ! Maintenant que vous avez vérifié votre authentification d’Adobe, vous pouvez l’utiliser pour interagir avec les API Adobe Target (ainsi qu’avec d’autres API d’Adobe). Par exemple, vous pouvez [utiliser les API Recommendations](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html) pour créer ou gérer des recommandations.
