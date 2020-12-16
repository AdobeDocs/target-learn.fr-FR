---
title: Présentation de l’API Adobe Recommendations
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations comprend un ensemble dédié d'API qui vous permet de gérer votre catalogue de produits et/ou de contenu recommandés ; gérer vos algorithmes et campagnes de recommandations ; et diffuser des recommandations dans des objets JSON, HTML ou XML à afficher dans des canaux Web, mobiles, e-mail, IOT et autres.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---


# Présentation de l’API Adobe Recommendations

Les API pertinentes pour [!DNL Recommendations] incluent [les API admin](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) qui vous permettent de :

* Gérer votre catalogue de produits ou de contenu recommandés
* Gérer vos algorithmes et activités [!DNL Recommendations]

Grâce à l&#39;API de diffusion [!DNL Target] [](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) avec Recommendations, vous pouvez également :

* Récupérez des recommandations dans des objets JSON, HTML ou XML afin de les afficher dans des canaux tels que Web, mobile, courrier électronique, Internet of Things (IOT) et autres.

## Description du didacticiel

Ce didacticiel guide les développeurs à travers des pratiques pratiques utilisant les API [!DNL Recommendations] pour configurer et gérer les catalogues et critères personnalisés [!DNL Recommendations], ainsi que l&#39;utilisation de l&#39;API de diffusion pour récupérer le contenu des recommandations. À la fin de ce didacticiel, vous pourrez :

* Configuration et gestion des entités à l’aide de l’API Recommendations
* Configuration et gestion de critères personnalisés à l’aide de l’API Recommendations
* Comprendre comment utiliser Recommendations avec l&#39;API de Diffusion pour utiliser les résultats de recommandations sur les périphériques non HTML

## Public

Ce didacticiel est destiné aux développeurs qui découvrent les API de Cible ou les API Recommendations.

## Conditions préalables

L&#39;utilisation des API d&#39;administration de Cible nécessite [configuration de l&#39;authentification d&#39;Adobe](../apis/configure-io-target-integration.md). Assurez-vous d’avoir configuré ce fichier avant de commencer ce didacticiel.

## Ressources

Notez les ressources suivantes, nécessaires pour comprendre ce didacticiel et le suivre avec succès :

| Ressource | Détails |
| --- | --- |
| Postman | Obtenez l&#39;application [Postman](https://www.postman.com/downloads/) pour votre système d&#39;exploitation. Postman basique est gratuit avec la création de compte. Bien qu&#39;il ne soit pas nécessaire pour utiliser les API Adobe Target en général, Postman facilite les workflows d&#39;API et Adobe Target fournit plusieurs collections Postman pour aider à exécuter ses API et apprendre comment elles fonctionnent. Le reste de ce tutoriel suppose une connaissance pratique de Postman. Pour obtenir de l&#39;aide, veuillez consulter la [documentation de Postman](https://learning.getpostman.com/). |
| Références | La connaissance des ressources suivantes est assurée tout au long du reste de ce didacticiel :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation de cible Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentation de l’API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Suivant : &quot;Gérer votre catalogue Recommendations&quot; >](manage-catalog.md)
