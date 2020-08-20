---
title: Présentation de l’API Adobe Recommendations
keywords: recommendations;adobe recommendations;premium;api;apis
description: adobe target Recommendations comprend un ensemble dédié d'API qui vous permet de gérer votre catalogue de produits et/ou de contenu recommandés ; gérer vos algorithmes et campagnes de recommandations ; et diffuser des recommandations dans des objets JSON, HTML ou XML à afficher dans des canaux Web, mobiles, e-mail, IOT et autres.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b0e36ff68732f79c61797181da781ec7401f3f84
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---


# Présentation de l’API Adobe Recommendations

Les API pertinentes pour [!DNL Recommendations] inclure les API [](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) d’administration qui vous permettent d’effectuer les opérations suivantes :

* Gérer votre catalogue de produits ou de contenu recommandés
* Gérer vos [!DNL Recommendations] algorithmes et activités

Grâce à l’API [!DNL Target] [](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) diffusion avec Recommendations, vous pouvez également :

* Récupérez des recommandations dans des objets JSON, HTML ou XML afin de les afficher dans des canaux tels que Web, mobile, courrier électronique, Internet of Things (IOT) et autres.

## Description du didacticiel

Ce didacticiel guide les développeurs à travers des pratiques pratiques utilisant les [!DNL Recommendations] API pour configurer et gérer [!DNL Recommendations] des catalogues et des critères personnalisés, ainsi que l&#39;utilisation de l&#39;API de diffusion pour récupérer le contenu des recommandations. À la fin de ce didacticiel, vous pourrez :

* Configuration et gestion des entités à l’aide de l’API Recommendations
* Configuration et gestion de critères personnalisés à l’aide de l’API Recommendations
* Comprendre comment utiliser Recommendations avec l&#39;API de Diffusion pour utiliser les résultats de recommandations sur les périphériques non HTML

## Public

Ce didacticiel est destiné aux développeurs qui découvrent les API de Cible ou les API Recommendations.

## Conditions préalables

L&#39;utilisation des API d&#39;administration de Cible nécessite la configuration [de l&#39;authentification par](../apis/configure-io-target-integration.md)Adobe. Assurez-vous d’avoir configuré ce fichier avant de commencer ce didacticiel.

## Ressources

Notez les ressources suivantes, nécessaires pour comprendre ce didacticiel et le suivre avec succès :

| Ressource | Détails |
| --- | --- |
| Postman | Obtenez l&#39;application [](https://www.postman.com/downloads/) Postman pour votre système d&#39;exploitation. Postman basique est gratuit avec la création de compte. Bien qu&#39;il ne soit pas nécessaire pour utiliser les API Adobe Target en général, Postman facilite les workflows d&#39;API et Adobe Target fournit plusieurs collections Postman pour aider à exécuter ses API et apprendre comment elles fonctionnent. Le reste de ce tutoriel suppose une connaissance pratique de Postman. Pour obtenir de l&#39;aide, veuillez consulter la documentation [de](https://learning.getpostman.com/)Postman. |
| Références | La connaissance des ressources suivantes est assurée tout au long du reste de ce didacticiel :<UL><li>[E/S Adobe Github](https://github.com/adobeio)</li><li>[Documentation sur les E/S cible Adobe](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentation de l’API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Suivant : &quot;Gérer votre catalogue Recommendations&quot; >](manage-catalog.md)
