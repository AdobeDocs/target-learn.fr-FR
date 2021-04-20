---
title: Gestion de votre catalogue Recommendations à l’aide d’API
description: Cette partie du didacticiel guide les développeurs à travers les étapes requises pour utiliser les API Adobe Target pour créer, mettre à jour, enregistrer, obtenir et supprimer des entités dans votre catalogue Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---


# Gérer votre catalogue [!DNL Recommendations] à l’aide d’API

A ce stade, vous avez appris à générer un jeton d&#39;accès, à l’aide du flux d’authentification JWT, pour utiliser les API d’administration Adobe Target avec Adobe I/O.

Vous pouvez utiliser les [API Recommendations](https://developers.adobetarget.com/api/recommendations/) pour ajouter, mettre à jour ou supprimer des éléments dans votre catalogue de recommandations. Comme pour le reste des API d’administration Adobe Target, les API [!DNL Recommendations] nécessitent une authentification.

>[!TIP]
>
>Envoyez le **[!UICONTROL SGI : JWT Generate + Auth via la demande User Token]** chaque fois que vous devez actualiser votre jeton d&#39;accès pour l’authentification, car elle expire après 24 heures. Voir [Configurer l’authentification de l’API d’Adobe](../apis/configure-io-target-integration.md) pour obtenir des instructions.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>Avant de continuer, obtenez la [collection Recommendations Postman](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## Création et mise à jour d&#39;éléments à l&#39;aide de l&#39;API Enregistrer les entités

Pour renseigner votre base de données de produits [!DNL Recommendations] à l’aide de l’API plutôt que d’un flux de produits CSV ou de demandes [!DNL Target] déclenchées sur les pages de produits, utilisez l’[API Enregistrer les entités](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). Cette demande ajoute ou met à jour un élément dans un seul environnement [!DNL Target]. La syntaxe est la suivante :

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Par exemple, les entités d&#39;enregistrement peuvent être utilisées pour mettre à jour des articles chaque fois que certains seuils sont atteints (seuils d&#39;inventaire ou de prix, par exemple) afin de les marquer et de les empêcher d&#39;être recommandés.

1. Accédez à **[!DNL Target]> [!UICONTROL Configuration] > [!UICONTROL Hôtes] > [!UICONTROL Environnements]** pour obtenir l&#39;ID d&#39;Environnement [!DNL Target] dans lequel vous souhaitez ajouter ou mettre à jour un élément.

   ![SaveEntities1](assets/SaveEntities01.png)

2. Vérifiez que `TENANT_ID` et `API_KEY` font référence aux variables d&#39;environnement de Postman établies précédemment. Utilisez l&#39;image ci-dessous pour la comparaison. Si nécessaire, modifiez les en-têtes et le chemin d’accès dans votre requête d’API pour qu’ils correspondent à ceux de l’image ci-dessous.

   ![SaveEntities3](assets/SaveEntities03.png)

3. Saisissez votre code JSON sous la forme **raw** dans le **Body**. N&#39;oubliez pas de spécifier votre ID d&#39;environnement en utilisant la variable `environment`. (Dans l’exemple ci-dessous, l’ID d’environnement est 6781.)

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   Vous trouverez ci-dessous un exemple de fichier JSON qui ajoute entity.id kit2001 avec les valeurs d’entité associées pour un produit Four de grille-pain, dans l’environnement 6781.

   ```
      {
      "entities": [{
              "name": "Toaster Oven",
              "id": "kit2001",
              "environment": 6781,
              "categories": [
                  "housewares:appliances"
              ],
              "attributes": {
                  "inventory": 77,
                  "margin": 23,
                  "message": "crashing helicopter",
                  "pageUrl": "www.foobar.foo.com/helicopter.html",
                  "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
              }
          }]
      }
   ```

4. Cliquez sur **Envoyer**. Vous devriez recevoir la réponse suivante.

   ![SaveEntities5.png](assets/SaveEntities05.png)

L’objet JSON peut être mis à l’échelle pour envoyer plusieurs produits. Par exemple, ce fichier JSON spécifie deux entités.

```
    {
        "entities": [{
                "name": "Toaster Oven",
                "id": "kit2001",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 89,
                    "margin": 11,
                    "message": "Toaster Oven",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 102.5
                }
            },
            {
                "name": "Blender",
                "id": "kit2002",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 36,
                    "margin": 5,
                    "message": "Blender",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 54.5
                }
            }
        ]
    }
```

1. Maintenant c&#39;est ton tour ! Utilisez l&#39;API **Enregistrer les entités** pour ajouter les éléments suivants à votre catalogue. Utilisez l’exemple JSON ci-dessus comme point de départ. (Vous devez étendre le fichier JSON pour inclure d’autres entités.)

   ![SaveEntities6.png](assets/SaveEntities06.png)

Oups, on dirait que ces deux derniers éléments n&#39;ont pas leur place. Examinons-les à l&#39;aide de l&#39;API **Get Entity**, et si nécessaire, supprimons-les à l&#39;aide de l&#39;API **Delete Entities**.

## Obtention des détails de l&#39;élément avec l&#39;API Get Entity

Pour récupérer les détails d&#39;un élément existant, utilisez [Get Entity API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). La syntaxe est la suivante :

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

Les détails d&#39;entité ne peuvent être récupérés que pour une seule entité à la fois. Vous pouvez utiliser l’option Obtenir l’entité pour confirmer que des mises à jour ont été effectuées dans le catalogue comme prévu ou pour contrôler le contenu du catalogue.

1. Dans la demande d’API, spécifiez l’ID d’entité à l’aide de la variable `entityId`. L&#39;exemple suivant renvoie des détails pour l&#39;entité dont entityId=kit2004.

   ![GetEntity1](assets/GetEntity1.png)

2. Vérifiez que `TENANT_ID` et `API_KEY` font référence aux variables d&#39;environnement de Postman établies précédemment. Utilisez l&#39;image ci-dessous pour la comparaison. Si nécessaire, modifiez les en-têtes et le chemin d’accès dans votre requête d’API pour qu’ils correspondent à ceux de l’image ci-dessous.

   ![GetEntity2](assets/GetEntity2.png)

3. Envoyez la demande.

   ![GetEntity3](assets/GetEntity3.png)
Si vous recevez une erreur indiquant que l&#39;entité est introuvable, comme indiqué dans l&#39;exemple ci-dessus, vérifiez que vous envoyez la demande à l&#39; [!DNL Target] environnement correct.

   >[!NOTE]
   Si aucun environnement n&#39;est explicitement spécifié, Get Entity tente d&#39;obtenir l&#39;entité à partir de votre [environnement par défaut](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html#section_4F8539B07C0C45E886E8525C344D5FB0) uniquement. Si vous souhaitez extraire de n’importe quel environnement autre que votre environnement par défaut, vous devez spécifier l’identifiant d’environnement.

4. Si nécessaire, ajoutez le paramètre `environmentId` et réenvoyez la demande.

   ![GetEntity4](assets/GetEntity4.png)

5. Envoyez une autre demande **Get Entity**, cette fois pour inspecter l&#39;entité dont entityId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

Supposons que vous décidiez que ces entités doivent être supprimées de votre catalogue. Utilisons l&#39;API **Supprimer les entités**.

## Suppression d&#39;éléments à l&#39;aide de l&#39;API Supprimer des entités

Pour supprimer des éléments de votre catalogue, utilisez l&#39;[API Supprimer les entités](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). La syntaxe est la suivante :

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
Cette API supprime les entités référencées par les identifiants que vous spécifiez.
Si aucun ID d&#39;entité n&#39;est fourni, toutes les entités de l&#39;environnement donné sont supprimées. Si aucun ID d&#39;environnement n&#39;est donné, les entités seront supprimées de tous les environnements. Faites attention à ceci !

1. Accédez à **[!DNL Target]> [!UICONTROL Configuration] > [!UICONTROL Hôtes] > [!UICONTROL Environnements]** pour obtenir l&#39;ID d&#39;Environnement [!DNL Target] à partir duquel vous souhaitez supprimer des éléments.

   ![DeleteEntities1](assets/SaveEntities01.png)

2. Dans la demande d&#39;API, spécifiez les ID d&#39;entité des entités que vous souhaitez supprimer, en utilisant la syntaxe `&ids=[comma-delimited-entity-ids]` (un paramètre de requête). Lors de la suppression de plusieurs entités, séparez les identifiants à l’aide de virgules.

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. Spécifiez l’ID d’environnement en utilisant la syntaxe `&environment=[environmentId]`, sinon les entités de tous les environnements seront supprimées.

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. Vérifiez que `TENANT_ID` et `API_KEY` font référence aux variables d&#39;environnement de Postman établies précédemment. Utilisez l&#39;image ci-dessous pour la comparaison. Si nécessaire, modifiez les en-têtes et le chemin d’accès dans votre requête d’API pour qu’ils correspondent à ceux de l’image ci-dessous.

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. Envoyez la demande.

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. Vérifiez vos résultats à l&#39;aide de **Get Entity**, qui doit maintenant indiquer que les entités supprimées sont introuvables.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

Félicitations ! Vous pouvez désormais utiliser les API [!DNL Recommendations] pour créer, mettre à jour, supprimer et obtenir des détails sur les entités de votre catalogue. Dans la section suivante, vous apprendrez comment gérer les critères personnalisés.

[Suivant : &quot;Gérer les critères personnalisés&quot; >](manage-custom-criteria.md)
