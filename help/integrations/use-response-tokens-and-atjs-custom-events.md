---
title: Utilisation des jetons de réponse et des événements personnalisés at.js
description: Découvrez comment utiliser les jetons de réponse et les événements personnalisés at.js pour partager des informations de profil de Target avec des systèmes tiers.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 3%

---

# Utilisation des jetons de réponse et des événements personnalisés at.js avec Adobe Target

Les jetons de réponse et les événements personnalisés `at.js` vous permettent de partager des informations de profil de [!DNL Target] avec des systèmes tiers. Tout objet du profil du visiteur [!DNL Target], y compris les attributs de profil personnalisés, les informations géographiques, les détails d’activité et les profils intégrés, peut être ajouté à la réponse [!DNL Target] dans laquelle vous pouvez utiliser JavaScript personnalisé pour l’intégration à un tiers.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Utilisation des jetons de réponse et des événements personnalisés at.js

1. Déterminer les données dont vous avez besoin à partir de [!DNL Target]
1. Activez les jetons de réponse pour les données dont vous avez besoin en activant le bouton d’activation/désactivation sur l’écran Configuration ->Jetons de réponse .
1. Déterminer quel écouteur d’événement vous devez utiliser
1. Écrivez le JavaScript nécessaire pour écouter l’événement Adobe Target, lire les jetons de réponse et faire ce dont vous avez besoin pour votre intégration.
1. Déployez votre écouteur d’événement JavaScript à l’aide d’une action de code personnalisé dans Launch après l’action &quot;Charger Target&quot; ou ajoutez-la à la section Library Footer (Pied de page de bibliothèque) d’at.js dans l’écran Configuration ->Mise en oeuvre et enregistrez un nouveau fichier at.js.
1. AQ et publication de votre intégration

## Ressources supplémentaires

* [Utilisation de l’Experience Cloud Debugger avec Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentation sur les jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Utilisation des fournisseurs de données dans Adobe Target](use-data-providers-to-integrate-third-party-data.md)
