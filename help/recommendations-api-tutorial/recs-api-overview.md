---
title: Qu’est-ce que l’API Adobe Recommendations ?
description: Ce tutoriel guide les développeurs à travers des pratiques pratiques pratiques à l’aide des API Recommendations d’Adobe Target pour configurer et gérer des catalogues Recommendations et des critères personnalisés, ainsi qu’à l’aide de l’API de diffusion pour récupérer le contenu des recommandations.
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
source-wordcount: '374'
ht-degree: 3%

---

# Présentation de l’API Adobe Recommendations

API pertinentes pour [!DNL Recommendations] include [API d’administration](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) qui vous permettent d’effectuer les opérations suivantes :

* Gestion de votre catalogue de produits ou de contenu recommandables
* Gérez vos [!DNL Recommendations] algorithmes et activités

En utilisant la variable [!DNL Target] [API de diffusion](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) avec Recommendations, vous pouvez également :

* Récupérez les recommandations dans les objets JSON, HTML ou XML afin qu’elles puissent être affichées sur le web, les appareils mobiles, les e-mails, l’Internet des objets (IOT) et sur d’autres canaux.

## Description du tutoriel

Ce tutoriel guide les développeurs à travers la pratique à l’aide de la méthode [!DNL Recommendations] API à configurer et gérer [!DNL Recommendations] catalogues et critères personnalisés, ainsi que l’utilisation de l’API de diffusion pour récupérer le contenu des recommandations. À la fin de ce tutoriel, vous serez en mesure de :

* Configuration et gestion des entités à l’aide de l’API Recommendations
* Configuration et gestion de critères personnalisés à l’aide de l’API Recommendations
* Comprendre comment utiliser Recommendations avec l’API de diffusion pour utiliser les résultats de recommandations sur les périphériques non HTMLS

## Public

Ce tutoriel est destiné aux développeurs qui découvrent les API Target ou les API Recommendations.

## Conditions requises

L’utilisation des API d’administration de Target nécessite [Configuration de l’authentification des Adobes](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html){target="_blank"}. Assurez-vous d’avoir configuré cette option avant de commencer ce tutoriel.

## Ressources

Notez les ressources suivantes, qui sont nécessaires pour comprendre ce tutoriel et le suivre avec succès :

| Ressource | Détails |
| --- | --- |
| Postman | Obtenez la variable [application Postman](https://www.postman.com/downloads/) pour votre système d’exploitation. Postman basic est gratuit avec la création de compte. Bien qu’elles ne soient pas requises pour utiliser les API Adobe Target en général, Postman facilite les processus d’API et Adobe Target fournit plusieurs collections Postman pour aider à exécuter ses API et apprendre à les utiliser. Le reste de ce tutoriel suppose des connaissances opérationnelles de Postman. Pour obtenir de l’aide, reportez-vous à la section [Documentation Postman](https://learning.getpostman.com/). |
| Références | Toute la suite de ce tutoriel vous familiarisera avec les ressources suivantes :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation sur Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentation de l’API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Suite : &quot;Gestion de votre catalogue Recommendations&quot; >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html){target="_blank"}
