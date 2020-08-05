---
title: Gérer les critères personnalisés
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations comprend un ensemble dédié d'API qui vous permet de gérer votre catalogue de produits et/ou de contenu recommandés ; gérer vos algorithmes et campagnes de recommandations ; et diffuser des recommandations dans des objets JSON, HTML ou XML à afficher dans des canaux Web, mobiles, e-mail, IOT et autres.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 78b30bc0018527f9d8b2a5b50edee86e877d14c7
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# Gérer les critères personnalisés

Parfois, les algorithmes fournis par [!DNL Recommendations] ne peuvent pas faire apparaître des éléments particuliers que vous souhaitez promouvoir. Dans ce cas, les critères personnalisés vous permettent de fournir un ensemble spécifique d’éléments recommandés pour un élément ou une catégorie clé donné. Vous définissez le mappage entre l’élément clé ou la catégorie et les éléments recommandés, et vous importez ce mappage comme critère personnalisé. Ce processus est décrit dans la documentation [sur les critères](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)personnalisés. Comme indiqué dans cette documentation, vous pouvez créer, modifier et supprimer des critères personnalisés dans l’interface [!DNL Target] utilisateur. Cependant, [!DNL Target] fournit également un ensemble d’API Critères personnalisés qui permettent une gestion plus détaillée de vos critères personnalisés.

>[!IMPORTANT]
>
>Suivez cette ligne guide d’utilisation pour les critères personnalisés :
>
> Soit tout faire (créer, modifier, supprimer) pour un critère personnalisé donné à l’aide des API, soit tout faire (créer, modifier, supprimer) à l’aide de l’interface utilisateur. La gestion de vos critères personnalisés par le biais d’une combinaison de l’interface utilisateur et de l’API peut entraîner des informations conflictuelles ou des résultats inattendus. Par exemple, la création d’un critère personnalisé dans l’interface utilisateur, puis sa modification via l’API, ne reflétera pas vos mises à jour dans l’interface utilisateur, même si elles seront mises à jour dans l’arrière-plan, comme l’indique l’API.

## Créer des critères personnalisés

Pour créer des critères personnalisés à l’aide de l’API [](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)Créer des critères personnalisés, la syntaxe est la suivante :

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Les critères personnalisés créés à l’aide de l’API Créer des critères personnalisés, comme décrit dans cet exercice, s’affichent dans l’interface utilisateur, où ils sont conservés. Vous ne pourrez pas les modifier ni les supprimer de l’interface utilisateur. Vous pouvez les modifier ou les supprimer **via l’API**, mais dans les deux cas, elles continueront à apparaître dans l’ [!DNL Target] interface utilisateur. Pour conserver l’option de modification ou de suppression de l’interface utilisateur, créez les critères personnalisés à l’aide de l’interface utilisateur selon [la documentation](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html), plutôt que d’utiliser l’API Créer des critères personnalisés.

Ne passez à ce didacticiel qu’après avoir lu l’avertissement ci-dessus et avoir trouvé confortable de créer de nouveaux critères personnalisés qui ne peuvent pas être supprimés de l’interface utilisateur.

1. Vérifiez `TENANT_ID` et `API_KEY` pour **Créer des critères** personnalisés référencez les variables d&#39;environnement Postman établies précédemment. Utilisez l&#39;image ci-dessous pour la comparaison.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Ajoutez votre **corps** en tant que fichier JSON **brut** qui définit l’emplacement de votre fichier CSV de critères personnalisés. Utilisez l’exemple fourni dans la documentation de l’API [](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) Créer des critères personnalisés comme modèle, en fournissant vos `environmentId` valeurs et d’autres valeurs si nécessaire. Pour cet exemple, nous utilisons LAST_PURCHASED comme clé.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Envoyez la demande et observez la réponse, qui contient les détails des critères personnalisés que vous venez de créer.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Pour vérifier que vos critères personnalisés ont été créés, accédez à **[!UICONTROL Recommendations]>[!UICONTROL Critères]** et recherchez vos critères par nom, ou utilisez l’API **Critères personnalisés de** Liste à l’étape suivante.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

Dans ce cas, nous avons une erreur. Examinons l&#39;erreur en examinant de plus près les critères personnalisés, à l&#39;aide de l&#39;API **Critères personnalisés de** Liste.

## Liste Critères personnalisés

Pour récupérer une liste de tous vos critères personnalisés avec des détails pour chacun d’eux, utilisez l’API [Critères personnalisés de](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)Liste. La syntaxe est la suivante :

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Vérifiez `TENANT_ID` et `API_KEY` comme avant, puis envoyez la demande. Dans la réponse, notez l’ID de critère personnalisé, ainsi que les détails concernant le message d’erreur mentionné précédemment.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

Dans ce cas, l’erreur s’est produite car les informations du serveur sont incorrectes, ce qui signifie qu’ [!DNL Target] il est impossible d’accéder au fichier CSV contenant la définition de critères personnalisés. Modifions les critères personnalisés pour corriger ce problème.

## Modifier des critères personnalisés

Pour modifier les détails d’une définition de critère personnalisée, utilisez l’API [](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)Modifier les critères personnalisés. La syntaxe est la suivante :

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Vérifiez `TENANT_ID` et `API_KEY`, comme auparavant.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Spécifiez l’ID de critère du critère personnalisé (unique) que vous souhaitez modifier.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. Dans le corps, fournissez à JSON mis à jour les informations correctes sur le serveur. (Pour cette étape, spécifiez l’accès FTP à un serveur auquel vous pouvez accéder.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Envoyez la demande et notez la réponse.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Vérifions la réussite des critères personnalisés mis à jour à l&#39;aide de l&#39;API **** Obtenir des critères personnalisés.

## Obtenir des critères personnalisés

Pour vue les détails des critères personnalisés pour un critère personnalisé spécifique, utilisez l’API [](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)Obtenir des critères personnalisés. La syntaxe est la suivante :

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Spécifiez l’ID de critère du critère personnalisé dont vous souhaitez obtenir les détails. Envoyez la demande et passez en revue la réponse.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Vérifier la réussite. (Dans notre cas, vérifiez qu’il n’y a pas d’autres erreurs FTP.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Facultatif) Vérifiez que la mise à jour est reflétée avec précision dans l’interface utilisateur.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Supprimer des critères personnalisés

A l’aide de l’ID de critère mentionné précédemment, supprimez vos critères personnalisés à l’aide de l’API [](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)Supprimer les critères personnalisés. La syntaxe est la suivante :

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Spécifiez l’ID de critère du critère personnalisé (unique) que vous souhaitez supprimer. Cliquez sur **Envoyer**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Vérifiez que les critères ont été supprimés à l’aide de l’option Obtenir des critères personnalisés.
   ![DeleteCustomCritères2](assets/DeleteCustomCriteria2.png)Dans ce cas, l&#39;erreur 404 attendue indique que les critères supprimés sont introuvables.

>[!NOTE]
>Pour rappel, les critères ne seront pas supprimés de l’ [!DNL Target] interface utilisateur même s’ils ont été supprimés, car ils ont été créés à l’aide de l’API Créer des critères personnalisés.

Félicitations ! Vous pouvez désormais créer, liste, modifier, supprimer et obtenir des détails sur des critères personnalisés à l’aide de l’ [!DNL Recommendations] API. Dans la section suivante, vous utiliserez l’API de [!DNL Target] Diffusion pour récupérer les recommandations.

[Suivant : &quot;Récupérer Recommendations avec l’API de Diffusion côté serveur&quot; >](fetch-recs-server-side-delivery-api.md)
