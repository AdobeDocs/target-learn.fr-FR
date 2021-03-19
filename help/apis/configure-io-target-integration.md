---
title: Configuration de l’authentification pour les API Adobe Target
description: Ce didacticiel guide les développeurs à travers les étapes requises pour générer les jetons d’authentification nécessaires pour interagir avec les API Adobe Target. Suivez ces étapes pour utiliser la Console développeur Adobe pour générer et tester le jeton d'accès porteur, nécessaire pour utiliser les API de Cible.
role: Développeur, administrateur, architecte
level: Intermédiaire
topic: Personnalisation, administration, intégrations, développement
feature: API/SDKs, administration et configuration
doc-type: tutorial
kt: null
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: 2c371ea17ce38928bcf3655a0d604a69e29963a0
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 2%

---


# Configuration de l’authentification pour les API Adobe Target

Les API d’administration Adobe Target, y compris les [!DNL Recommendations] API d’administration, sont sécurisées par l’authentification afin de garantir que seuls les utilisateurs autorisés les utilisent pour accéder à Adobe Target. Utilisez [Adobe Developer Console](https://console.adobe.io/) pour gérer cette authentification pour toutes les solutions Adobe Experience Cloud, y compris [!DNL Target].

Cette leçon décrit les étapes préliminaires nécessaires à la génération des jetons d’authentification nécessaires pour interagir avec les API Adobe Target. Dans les sections suivantes, vous allez :

1. Créez un projet (précédemment appelé intégration) dans la console de développement des Adobes.
2. Exportez les détails du projet vers Postman.
3. Générez un jeton d&#39;accès au porteur.
4. Testez le jeton d&#39;accès porteur.

## Conditions préalables

| Ressource | Détails |
| --- | --- |
| Postman | Pour réussir ces étapes, obtenez l&#39;[application Postman](https://www.postman.com/downloads/) pour votre système d&#39;exploitation. Postman basique est gratuit avec la création de compte. Bien qu&#39;il ne soit pas nécessaire pour utiliser les API Adobe Target en général, Postman facilite les workflows d&#39;API et Adobe Target fournit plusieurs collections Postman pour aider à exécuter ses API et apprendre comment elles fonctionnent. Le reste de ce tutoriel suppose une connaissance pratique de Postman. Pour obtenir de l&#39;aide, veuillez consulter la [documentation de Postman](https://learning.getpostman.com/). |
| Références | La connaissance des ressources suivantes est assurée tout au long du reste de ce didacticiel :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation sur les Adobes I/O de cible](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentation de l’API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Création d’un projet d’Adobe I/O

Dans cette section, vous accéderez à la console de développement des Adobes et créerez un projet pour [!DNL Adobe Target]. Pour plus d&#39;informations, consultez la [documentation relative aux projets](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. Dans le [Adobe Admin Console](https://adminconsole.adobe.com/), assurez-vous que votre compte utilisateur d&#39;Adobe a été autorisé à la fois à accéder au niveau [Administrateur de produit](https://helpx.adobe.com/enterprise/using/admin-roles.html) et au niveau [Développeur](https://helpx.adobe.com/enterprise/using/manage-developers.html) [!DNL Target].

2. Dans la [Console développeur d&#39;Adobes](https://console.adobe.io/), sélectionnez l&#39;organisation Experience Cloud pour laquelle vous souhaitez créer cette intégration. (Notez qu’il est probable que vous n’ayez accès qu’à une seule organisation Experience Cloud.)

   ![configure-io-cible-create-project2.png](assets/configure-io-target-createproject2.png)

3. Cliquez sur **[!UICONTROL Créer un nouveau projet]**.

   ![configure-io-cible-create-project3.png](assets/configure-io-target-createproject3.png)

4. Cliquez sur **[!UICONTROL Ajouter l&#39;API]** pour ajouter une API REST à votre projet afin d&#39;accéder aux services et aux produits d&#39;Adobe.

   ![API Ajoute](assets/configure-io-target-createproject4.png)

5. Sélectionnez **[!DNL Adobe Target]** comme service d&#39;Adobe avec lequel vous souhaitez intégrer. Cliquez sur le bouton **[!UICONTROL Suivant]** qui s’affiche.

   ![configure-io-cible-create-project5](assets/configure-io-target-createproject5.png)

6. Sélectionnez une option pour associer des clés publiques et privées à l’intégration du compte de service que vous créez pour la Cible. Pour ce didacticiel, sélectionnez **[!UICONTROL Option 1 : Générez une paire de clés]** et cliquez sur **[!UICONTROL Générer la paire de clés]**.
   ![configure-io-cible-create-project6](assets/configure-io-target-createproject6.png)

7. Notez les résultats ! Selon les instructions, notez le fichier de configuration automatiquement téléchargé (`config`), qui contient votre clé privée. Cliquez sur **[!UICONTROL Suivant]**.
   ![configure-io-cible-createproject7](assets/configure-io-target-createproject7.png)
8. Dans votre système de fichiers, vérifiez l’emplacement de `config`, qui est le fichier de configuration compressé créé à l’étape précédente. De nouveau, ce fichier `config` contient votre clé privée, dont vous aurez besoin ultérieurement. L&#39;emplacement exact dans votre système de fichiers peut différer de celui qui est illustré ici.
   ![configure-io-cible-createproject8](assets/configure-io-target-createproject8.png)
9. De retour dans la console de développement des Adobes, sélectionnez le [profil(s) de produit](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) correspondant aux propriétés dans lesquelles vous utilisez [!DNL Recommendations]. (Si vous n’utilisez pas de propriétés, sélectionnez l’option Espace de travail par défaut.) Cliquez sur **[!UICONTROL Enregistrer l&#39;API configurée]**.
   ![configure-io-cible-create-project9](assets/configure-io-target-createproject9.png)

10. Cliquez sur **[!UICONTROL Créer une intégration]**. Vous devriez recevoir un message temporaire indiquant que votre API a été correctement configurée.

11. En guise de dernière étape, renommez votre projet en un nom plus significatif que le `Project 1` original. Pour ce faire, accédez au projet à l’aide du chemin de navigation indiqué, cliquez sur **[!UICONTROL Modifier le projet]** pour accéder au module **[!UICONTROL Modifier le projet], puis renommez le projet.

![configure-io-cible-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>Dans ce didacticiel, nous nommons notre projet &quot;Intégration de Cibles&quot;. Si vous prévoyez d’utiliser votre projet pour plus d’Adobe Target, vous pouvez lui attribuer un nom en conséquence. Par exemple, vous pouvez choisir de lui attribuer le nom &quot;API Adobe&quot; ou &quot;API Experience Cloud&quot;, car il peut être utilisé avec d’autres solutions dans Adobe Experience Cloud.

## Exporter les détails du projet

Maintenant que vous disposez d&#39;un projet d&#39;Adobe que vous pouvez utiliser pour accéder à [!DNL Target], vous devez vous assurer d&#39;envoyer les détails de ce projet avec vos demandes d&#39;API d&#39;Adobe. Ces détails sont nécessaires pour interagir avec plusieurs API d&#39;Adobe, y compris plusieurs API [!DNL Target]. Par exemple, les détails de l’intégration incluent les informations d’autorisation et d’authentification requises par les API d’administration [!DNL Target]. Par conséquent, pour utiliser les API avec Postman, vous devez envoyer ces détails à Postman.

Il y a plusieurs façons de préciser les détails de votre projet dans Postman, mais dans cette section, nous profitons de certaines fonctionnalités et collections préétablies. D&#39;abord (dans cette section), vous exporterez les détails de votre intégration dans un environnement Postman. Ensuite (dans la section suivante), vous allez générer un jeton d&#39;accès au porteur pour vous accorder l&#39;accès aux ressources d&#39;Adobe nécessaires.

>[!NOTE]
>
>Pour obtenir des instructions vidéo applicables à toute solution Experience Cloud, y compris [!DNL Target], voir [Utiliser Postman avec les API Experience Platform](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html). Les sections suivantes concernent les API [!DNL Target] :
>
> 1. Exporter les détails de l&#39;intégration des Adobes I/O à Postman
> 2. Générer un Jeton d&#39;accès avec Postman

>
> 
Ces étapes sont également décrites ci-dessous.

1. Toujours dans la [Console développeur d&#39;Adobes](https://console.adobe.io/), accédez à la vue des **[!UICONTROL informations d&#39;identification du compte de service (JWT)]** de votre nouveau projet. Utilisez le volet de navigation de gauche ou la section **[!UICONTROL Informations d&#39;identification]** comme indiqué.
   ![JWT1](assets/configure-io-target-jwt1.png)
Dans les détails **[!UICONTROL des informations d’]** identification, notez que vous pouvez vue votre(s) **clé(s)** publique(s), votre ID **de**client et d’autres informations relatives à votre compte de service.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Cliquez sur pour accéder aux informations sur l&#39;API **[!UICONTROL Adobe Target]**. Utilisez le volet de navigation de gauche ou la section **[!UICONTROL Produits et services connectés]** comme indiqué.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Cliquez sur **[!UICONTROL Télécharger pour Postman]** > **[!UICONTROL Compte de service (JWT)]** pour créer un fichier JSON qui capture vos informations d&#39;authentification pour un environnement Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)
Notez le fichier JSON dans votre système de fichiers.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. Dans Postman, cliquez sur l’icône représentant un engrenage pour gérer vos environnements, puis cliquez sur **Importer** pour importer le fichier JSON (environnement).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Choisissez votre fichier et cliquez sur **Ouvrir**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. Dans le module postal **Gérer les Environnements**, cliquez sur le nom de l&#39;environnement nouvellement importé pour l&#39;inspecter. (Votre nom d&#39;environnement peut être différent de celui indiqué ici. Modifiez le nom selon vos besoins. Il n’est pas nécessaire de faire correspondre le nom du projet d’Adobe.)
   ![JWT6](assets/configure-io-target-jwt6.png)
7. Les valeurs des notes `CLIENT_SECRET` et `API_KEY` (ainsi que d&#39;autres variables) sont prérenseignées, à partir de votre intégration telle que définie dans la console de développement des Adobes. (La variable Postman `CLIENT_SECRET` doit correspondre aux informations d’identification de l’Adobe `CLIENT SECRET` affichées dans la Console développeur et `API_KEY` dans Postman doit également correspondre à `CLIENT ID` dans la Console développeur.) Par contre, la note `PRIVATE_KEY`, `JWT_TOKEN` et `ACCESS_TOKEN` sont vides. Début en fournissant la valeur `PRIVATE_KEY`.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**Surprise !**
   >
   >Quoique-nique ! Pouvez-vous vous souvenir où se trouve votre clé privée ?
   >C&#39;est exact, il se trouve dans le fichier `config` téléchargé plus tôt à partir de la Console développeur de l&#39;Adobe !

8. A partir de votre système de fichiers, ouvrez votre fichier `config`, puis ouvrez le fichier de clé `private`.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Sélectionnez et copiez l&#39;intégralité du contenu du fichier de clés `private`.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. Dans Postman, collez votre valeur de clé privée dans les champs **VALEUR INITIALE** et **VALEUR ACTUELLE**.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Cliquez sur **[!UICONTROL Mettre à jour]**, puis fermez le mode Environnements.


## Générer le jeton d&#39;accès porteur

Dans cette section, vous générez votre jeton d&#39;accès au porteur, qui est nécessaire pour authentifier votre interaction avec les API Adobe Target. Pour générer votre jeton d&#39;accès porteur, vous devez envoyer vos détails d&#39;intégration (établis dans les sections précédentes) au [service Identity Management d&#39;Adobe (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Il existe plusieurs façons de le faire, mais dans ce tutoriel, vous avez créé une demande de POST sur mesure à l&#39;API IMS. Je plaisante. Dans ce tutoriel, nous profitons d&#39;une collection Postman contenant un appel IMS préconstruit qui rend le processus direct et facile. Une fois la collection importée, vous pouvez la réutiliser au besoin, afin de générer de nouveaux jetons non seulement pour Adobe Target, mais également pour d’autres API d’Adobe.

1. Accédez à l&#39;exemple d&#39;appel [Adobe Identity Management Service API ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Cliquez sur **Adobe I/O Jeton d&#39;accès Generation Postman collection**.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Obtenez le fichier JSON brut pour cette collection en cliquant sur **Brut**, puis en copiant le fichier JSON résultant dans le Presse-papiers. (Vous pouvez également enregistrer le fichier JSON brut dans un fichier .json.)
   ![token3](assets/configure-io-target-generatetoken3.png)
4. Dans Postman, importez la collection en collant et en envoyant le fichier JSON brut à partir du Presse-papiers. (Vous pouvez également télécharger le fichier .json que vous avez enregistré.) Cliquez sur **Continue** (Continuer).
   ![jeton4](assets/configure-io-target-generatetoken4.png)
5. Sélectionnez l&#39;IMS **[!UICONTROL IMS : JWT Generate + Auth via User Token]** requête dans la collection Postman de génération de Jetons d&#39;accès d’Adobe I/O, assurez-vous que votre environnement est sélectionné, puis cliquez sur **Envoyer** pour générer le jeton.

   ![jeton5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Ce jeton d&#39;accès au porteur sera valable 24 heures. Envoyez de nouveau la demande chaque fois que vous devez générer un nouveau jeton.

6. Ouvrez à nouveau le module Gérer les Environnements, puis sélectionnez votre environnement.
   ![token6](assets/configure-io-target-jwt11.png)
7. Notez que les valeurs `ACCESS_TOKEN` et `JWT_TOKEN` sont maintenant renseignées.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>Q : Dois-je utiliser la collection Postman de la génération de Jetons d&#39;accès d&#39;Adobe I/O pour générer le JSON Web Token (JWT) et le jeton d&#39;accès porteur ?
>
>A : Non ! La collection Postman de la génération de Jetons d&#39;accès d&#39;Adobe I/O est disponible pour faciliter la génération du jeton d&#39;accès JWT et porteur dans Postman. Vous pouvez également utiliser les fonctionnalités de la console de développement Adobe pour générer manuellement le jeton d&#39;accès porteur.

## Testez le jeton d&#39;accès porteur

Dans cet exercice, vous utiliserez votre nouveau jeton d&#39;accès au porteur en envoyant une demande d&#39;API qui récupère une liste d&#39;activités de votre compte [!DNL Target]. Une réponse positive indique que votre projet d’Adobe et votre authentification fonctionnent comme prévu afin d’utiliser l’API.

1. Importez les [API d&#39;administration Adobe Target Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection). Suivez toutes les invites jusqu&#39;à ce que la collection soit importée dans Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Développez la collection et notez la demande **[!UICONTROL Listes activités]**.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Notez que les variables telles que `{{access_token}}` ne sont pas résolues au départ. Vous pouvez résoudre ce problème de plusieurs manières différentes (par exemple, vous pouvez définir une nouvelle variable de collecte appelée `{{access_token}}`), mais dans ce didacticiel, vous allez plutôt modifier la demande d&#39;API pour tirer parti de l&#39;environnement Postman que vous utilisiez précédemment. Cela permettra à l’environnement de continuer à servir de consolidation unique et cohérente de toutes les variables communes aux API d’Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Tapez `{{access_token}}` pour remplacer `{{ACCESS_TOKEN}}` par .
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Tapez `{{api_key}}` pour remplacer `{{API_KEY}}` par .
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Tapez `{{tenant}}` pour remplacer `{{TENANT_ID}}` par . La note `{{TENANT_ID}}` n&#39;est pas encore reconnue.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Ouvrez le module Gérer les Environnements, puis sélectionnez votre environnement.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Tapez pour ajouter une nouvelle variable d&#39;environnement `{{TENANT_ID}}`. Copiez et collez la valeur de votre ID de client dans les champs **VALEUR INITIALE** et **VALEUR ACTUELLE** de votre nouvelle variable d&#39;environnement `TENANT_ID`.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >L&#39;ID de client est différent de votre [!DNL Target] `clientcode`. L&#39;ID de client existe dans l&#39;URL lorsque vous êtes connecté à [!DNL Target]. Pour obtenir votre ID de client, connectez-vous à [!DNL Adobe Experience Cloud], ouvrez [!DNL Target], puis cliquez sur la carte [!DNL Target]. Utilisez la valeur ID du client comme indiqué dans le sous-domaine URL.
   >
   >Par exemple, si votre URL lors de la connexion à Adobe Target est
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >votre ID de client est alors &quot;mycompany&quot;.

1. Envoyez votre demande, après avoir sélectionné l’environnement approprié. Vous devriez recevoir une réponse contenant votre liste d&#39;activités.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

Félicitations ! Maintenant que vous avez vérifié votre authentification d&#39;Adobe, vous pouvez l&#39;utiliser pour interagir avec les API Adobe Target (ainsi qu&#39;avec d&#39;autres API d&#39;Adobe). Par exemple, vous pouvez [utiliser les API Recommendations](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html) pour créer ou gérer des recommandations.
