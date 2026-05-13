---
title: Utilisation des jetons de réponse et des événements personnalisés at.js
description: Découvrez comment utiliser les jetons de réponse et les événements personnalisés at.js pour partager des informations de profil de Target vers des systèmes tiers.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
TQID: https://experienceleague.adobe.com/gJfFi9mC3iKY8pEdvE1Tuk7Mk2rUOdTKtv67vXQwkO8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 3%

---

# Utilisation de jetons de réponse et d’événements personnalisés at.js avec Adobe Target

Les jetons de réponse et `at.js` événements personnalisés vous permettent de partager des informations de profil de [!DNL Target] vers des systèmes tiers. Tout objet dans le profil du visiteur [!DNL Target], y compris les attributs de profil personnalisés, les informations géographiques, les détails d’activité et les profils intégrés, peut être ajouté à la réponse [!DNL Target] où vous pouvez utiliser le JavaScript personnalisé pour l’intégration à un tiers.

>[!VIDEO](https://video.tv.adobe.com/v/33875/?captions=fre_fr&quality=12)

## Utilisation des jetons de réponse et des événements personnalisés at.js

1. Détermination des données dont vous avez besoin à partir de [!DNL Target]
1. Activez les jetons de réponse pour les données dont vous avez besoin en appuyant sur le bouton (bascule) de l’écran Configuration->Jetons de réponse .
1. Détermination de l’écouteur d’événement à utiliser
1. Écrivez le code JavaScript nécessaire pour écouter l’événement Adobe Target, lire les jetons de réponse et faire ce dont vous avez besoin pour votre intégration
1. Déployez votre écouteur d’événement JavaScript à l’aide d’une action de code personnalisé dans Launch après l’action « Charger Target » ou ajoutez-la à la section Pied de bibliothèque d’at.js sur l’écran Configuration->Implémentation et enregistrez un nouveau fichier at.js
1. Contrôle qualité et publication de votre intégration

## Ressources supplémentaires

* [Utilisation d’Experience Cloud Debugger avec Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentation sur le jeton de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr)
* [Utilisation des fournisseurs de données dans Adobe Target](use-data-providers-to-integrate-third-party-data.md)
