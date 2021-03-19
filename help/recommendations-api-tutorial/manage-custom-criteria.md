---
title: Comment gérer les critères personnalisés
description: Cette partie du didacticiel guide les développeurs à travers les étapes requises pour utiliser les API Adobe Target pour gérer, créer, liste, modifier, obtenir et supprimer des critères Adobe Target.
role: Développeur
level: Intermédiaire
topic: Personnalisation, administration, intégrations, développement
feature: API/SDK, Recommendations, Administration et configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 1%

---


# Gérer les critères personnalisés

Parfois, les algorithmes fournis par [!DNL Recommendations] ne sont pas en mesure de faire apparaître des éléments particuliers que vous souhaitez promouvoir. Dans ce cas, les critères personnalisés vous permettent de fournir un ensemble spécifique d’éléments recommandés pour un élément ou une catégorie clé donné. Vous définissez le mappage entre l’élément clé ou la catégorie et les éléments recommandés, et vous importez ce mappage comme critère personnalisé. Ce processus est décrit dans la [documentation des critères personnalisés](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html). Comme indiqué dans cette documentation, vous pouvez créer, modifier et supprimer des critères personnalisés par le biais de l&#39;[!DNL Target] interface utilisateur (interface utilisateur). Cependant, [!DNL Target] fournit également un ensemble d&#39;API Critères personnalisés qui permettent une gestion plus détaillée de vos critères personnalisés.

>[!IMPORTANT]
>
>Suivez cette ligne guide d’utilisation pour les critères personnalisés :
>
> Soit tout faire (créer, modifier, supprimer) pour un critère personnalisé donné à l’aide des API, soit tout faire (créer, modifier, supprimer) à l’aide de l’interface utilisateur. La gestion de vos critères personnalisés par le biais d’une combinaison de l’interface utilisateur et de l’API peut entraîner des informations conflictuelles ou des résultats inattendus. Par exemple, la création d’un critère personnalisé dans l’interface utilisateur, puis sa modification via l’API, ne reflétera pas vos mises à jour dans l’interface utilisateur, même si elles seront mises à jour dans l’arrière-plan, comme l’indique l’API.

## Créer des critères personnalisés

Pour créer des critères personnalisés à l&#39;aide de l&#39;[API Créer des critères personnalisés](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom), la syntaxe est la suivante :

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Les critères personnalisés créés à l’aide de l’API Créer des critères personnalisés, comme décrit dans cet exercice, s’affichent dans l’interface utilisateur, où ils sont conservés. Vous ne pourrez pas les modifier ni les supprimer de l’interface utilisateur. Vous pouvez les modifier ou les supprimer **via l&#39;API**, mais dans les deux cas, ils continueront à apparaître dans l&#39;interface utilisateur [!DNL Target]. Pour conserver l’option de modification ou de suppression de l’interface utilisateur, créez les critères personnalisés à l’aide de l’interface utilisateur par [la documentation](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html), plutôt que d’utiliser l’API Créer des critères personnalisés.

Ne passez à ce didacticiel qu’après avoir lu l’avertissement ci-dessus et avoir trouvé confortable de créer de nouveaux critères personnalisés qui ne peuvent pas être supprimés de l’interface utilisateur.

1. Vérifiez `TENANT_ID` et `API_KEY` pour **Créez des critères personnalisés** et référencez les variables d&#39;environnement Postman établies précédemment. Utilisez l&#39;image ci-dessous pour la comparaison.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Ajoutez votre fichier **Body** comme **raw** JSON qui définit l’emplacement de votre fichier CSV de critères personnalisés. Utilisez l&#39;exemple fourni dans la documentation [Créer une API de critères personnalisés](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) comme modèle, fournissant vos `environmentId` et d&#39;autres valeurs si nécessaire. Pour cet exemple, nous utilisons LAST_PURCHASED comme clé.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Envoyez la demande et observez la réponse, qui contient les détails des critères personnalisés que vous venez de créer.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Pour vérifier que vos critères personnalisés ont été créés, naviguez dans Adobe Target jusqu’à **[!UICONTROL Recommendations] > [!UICONTROL Critères]** et recherchez vos critères par nom, ou utilisez l’**API Critères personnalisés de Liste** à l’étape suivante.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

Dans ce cas, nous avons une erreur. Examinons l&#39;erreur en examinant de plus près les critères personnalisés, à l&#39;aide de l&#39;**API Critères personnalisés de la Liste**.

## Liste Critères personnalisés

Pour récupérer une liste de tous vos critères personnalisés avec des détails pour chacun d&#39;eux, utilisez l&#39;[API Critères personnalisés de Liste](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). La syntaxe est la suivante :

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Vérifiez `TENANT_ID` et `API_KEY` comme avant, puis envoyez la demande. Dans la réponse, notez l’ID de critère personnalisé, ainsi que les détails concernant le message d’erreur mentionné précédemment.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

Dans ce cas, l&#39;erreur s&#39;est produite car les informations du serveur sont incorrectes, ce qui signifie que [!DNL Target] ne peut pas accéder au fichier CSV contenant la définition de critères personnalisés. Modifions les critères personnalisés pour corriger ce problème.

## Modifier des critères personnalisés

Pour modifier les détails d’une définition de critère personnalisée, utilisez l’[API Modifier les critères personnalisés](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). La syntaxe est la suivante :

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Vérifiez `TENANT_ID` et `API_KEY`, comme auparavant.
   ![ModifierCritèresPersonnalisés1](assets/EditCustomCriteria1.png)

1. Spécifiez l’ID de critère du critère personnalisé (unique) que vous souhaitez modifier.
   ![ModifierCritèresPersonnalisés2](assets/EditCustomCriteria2.png)

1. Dans le corps, fournissez à JSON mis à jour les informations correctes sur le serveur. (Pour cette étape, spécifiez l’accès FTP à un serveur auquel vous pouvez accéder.)
   ![ModifierCritèresPersonnalisés3](assets/EditCustomCriteria3.png)

1. Envoyez la demande et notez la réponse.
   ![ModifierCritèresPersonnalisés4](assets/EditCustomCriteria4.png)

Vérifions la réussite des critères personnalisés mis à jour, en utilisant l&#39;**API Obtenir des critères personnalisés**.

## Obtenir des critères personnalisés

Pour vue les détails des critères personnalisés pour un critère personnalisé spécifique, utilisez l&#39;[API Obtenir des critères personnalisés](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). La syntaxe est la suivante :

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Spécifiez l’ID de critère du critère personnalisé dont vous souhaitez obtenir les détails. Envoyez la demande et passez en revue la réponse.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Vérifier la réussite. (Dans notre cas, vérifiez qu’il n’y a pas d’autres erreurs FTP.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Facultatif) Vérifiez que la mise à jour est reflétée avec précision dans l’interface utilisateur.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Supprimer des critères personnalisés

En utilisant l&#39;ID de critère mentionné précédemment, supprimez vos critères personnalisés à l&#39;aide de l&#39;[API Supprimer les critères personnalisés](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom). La syntaxe est la suivante :

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Spécifiez l’ID de critère du critère personnalisé (unique) que vous souhaitez supprimer. Cliquez sur **Envoyer**.
   ![DeleteCustomCritères1](assets/DeleteCustomCriteria1.png)

1. Vérifiez que les critères ont été supprimés à l’aide de l’option Obtenir des critères personnalisés.
   ![DeleteCustomCritères2](assets/DeleteCustomCriteria2.png)
 Dans ce cas, l&#39;erreur 404 attendue indique que les critères supprimés sont introuvables.

>[!NOTE]
>Pour rappel, les critères ne seront pas supprimés de l&#39;interface utilisateur [!DNL Target] même s&#39;ils ont été supprimés, car ils ont été créés à l&#39;aide de l&#39;API Créer des critères personnalisés.

Félicitations ! Vous pouvez désormais créer, liste, modifier, supprimer et obtenir des détails sur des critères personnalisés à l’aide de l’API [!DNL Recommendations]. Dans la section suivante, vous utiliserez l&#39;API de Diffusion [!DNL Target] pour récupérer les recommandations.

[Suivant : &quot;Récupérer Recommendations avec l’API de Diffusion côté serveur&quot; >](fetch-recs-server-side-delivery-api.md)
