---
title: Utiliser des jetons de réponse et des Événements personnalisés at.js avec Adobe Target
seo-title: Utiliser des jetons de réponse et des Événements personnalisés at.js avec Adobe Target
description: Les jetons de réponse et les Événements personnalisés d’at.js vous permettent de partager des informations de profil de Cible vers des systèmes tiers. Tout objet du profil du visiteur de Cible, y compris les attributs de profil personnalisés, les informations géographiques, les détails d’activité et les profils intégrés, peut être ajouté à la réponse de Cible dans laquelle vous pouvez utiliser du code JavaScript personnalisé pour l’intégrer à un tiers.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# Utiliser des jetons de réponse et des Événements personnalisés at.js avec Adobe Target

Les jetons de réponse et les Événements personnalisés `at.js` vous permettent de partager des informations de profil de [!DNL Target] vers des systèmes tiers. Tout objet du profil de visiteur [!DNL Target], y compris les attributs de profil personnalisés, les informations géographiques, les détails d&#39;activité et les profils intégrés, peut être ajouté à la réponse [!DNL Target] dans laquelle vous pouvez utiliser du code JavaScript personnalisé pour l&#39;intégrer à un tiers.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Utilisation des jetons de réponse et des Événements personnalisés d’at.js

1. Déterminer les données dont vous avez besoin à partir de [!DNL Target]
1. Activez les jetons de réponse pour les données dont vous avez besoin en activant la bascule sur l&#39;écran Configuration->Jetons de réponse.
1. Déterminer l&#39;écouteur de événement à utiliser
1. Ecrivez le code JavaScript nécessaire pour écouter le événement Adobe Target, lire les jetons de réponse et faire ce dont vous avez besoin pour votre intégration.
1. Déployez le code JavaScript de votre écouteur de événement à l’aide d’une action de code personnalisé dans Lancer après l’action &quot;Charger la Cible&quot; ou ajoutez-le à la section Pied de page de la bibliothèque d’at.js sur l’écran Configuration->Implémentation et enregistrez un nouveau fichier at.js.
1. AQ et publier votre intégration

## Ressources supplémentaires

* [Utiliser l&#39;Experience Cloud Debugger avec Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentation du jeton de réponse](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [Documentation du Événement personnalisé d’at.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Utilisation des fournisseurs de données dans Adobe Target](use-data-providers-to-integrate-third-party-data.md)