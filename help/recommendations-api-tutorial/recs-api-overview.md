---
title: Qu’est-ce que l’API Adobe Recommendations ?
description: Ce tutoriel explique aux développeurs la pratique de l’utilisation des API Recommendations d’Adobe Target pour configurer et gérer les catalogues de recommandations et les critères personnalisés, ainsi que l’utilisation de l’API de diffusion pour récupérer le contenu des recommandations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 542ff406fc24df54a2f1b007422492341ea46507
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# Présentation de l’API Adobe Recommendations

Les API pertinentes pour [!DNL Recommendations] incluent les [API d’administration](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) qui vous permettent d’effectuer les opérations suivantes :

* Gérer votre catalogue de produits ou de contenu recommandés
* Gestion des algorithmes et activités de [!DNL Recommendations]

À l’aide de l’[!DNL Target] [API de diffusion](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) avec Recommendations, vous pouvez également :

* Récupérez les recommandations dans les objets JSON, HTML ou XML afin qu’elles puissent être affichées sur le web, les appareils mobiles, les e-mails, l’Internet des objets (IOT) et d’autres canaux.

## Description du tutoriel

Ce tutoriel explique aux développeurs la pratique de l’utilisation des API [!DNL Recommendations] pour configurer et gérer des catalogues de [!DNL Recommendations] et des critères personnalisés, ainsi que l’utilisation de l’API de diffusion pour récupérer le contenu des recommandations. À la fin de ce tutoriel, vous serez en mesure de :

* Configuration et gestion des entités à l’aide de l’API Recommendations
* Configurer et gérer des critères personnalisés à l’aide de l’API Recommendations
* Découvrez comment utiliser Recommendations avec l’API de diffusion pour utiliser les résultats des recommandations sur les appareils non HTML

## Public

Ce tutoriel est destiné aux développeurs qui découvrent les API Target ou Recommendations.

## Conditions requises

L’utilisation des API d’administration Target nécessite [la configuration de l’authentification Adobe](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html){target="_blank"}. Assurez-vous d’avoir configuré ce paramètre avant de commencer ce tutoriel.

## Ressources

Notez les ressources suivantes, qui sont nécessaires pour comprendre ce tutoriel et le suivre avec succès :

| Ressource | Détails |
| --- | --- |
| Postman | Obtenez l&#39;application [Postman](https://www.postman.com/downloads/) pour votre système d&#39;exploitation. Postman basic est gratuit avec la création de compte. Bien que cela ne soit pas nécessaire pour utiliser les API Adobe Target en général, Postman facilite les workflows d’API et Adobe Target fournit plusieurs collections Postman pour l’aider à exécuter ses API et à apprendre à les utiliser. Le reste de ce tutoriel suppose une connaissance pratique de Postman. Pour obtenir de l’aide, consultez la documentation de [Postman](https://learning.getpostman.com/). |
| Références | Tout au long du reste de ce tutoriel, vous devez connaître les ressources suivantes :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation de Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentation de l’API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Suite : « Gestion de votre catalogue de recommandations » >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html){target="_blank"}
