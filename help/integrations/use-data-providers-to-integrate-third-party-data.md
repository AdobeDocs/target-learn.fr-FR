---
title: Utiliser les fournisseurs de données pour intégrer des données tierces dans un Adobe Target
seo-title: Utiliser les fournisseurs de données pour intégrer des données tierces dans un Adobe Target
description: L’option Fournisseurs de données est une fonctionnalité qui vous permet de transmettre facilement des données provenant de tiers à Target.  Un tiers peut être un service météorologique, une plateforme de gestion des données, ou même votre propre service web. Vous pouvez ensuite utiliser ces données pour créer des audiences, cibler du contenu et enrichir le profil du visiteur.
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 40%

---


# Utiliser les fournisseurs de données pour intégrer des données tierces dans un Adobe Target

[!UICONTROL L’option Fournisseurs de données est une fonctionnalité qui vous permet de transmettre facilement des données provenant de tiers à Target.  ]  Un tiers peut être un service météorologique, une plateforme de gestion des données, ou même votre propre service web. Vous pouvez ensuite utiliser ces données pour créer des audiences, cibler du contenu et enrichir le profil du visiteur.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Utilisation des fournisseurs de données

1. L’expert en implémentation ajoute le code avant at.js (ou dans la section En-tête de bibliothèque d’at.js) qui effectue l’appel d’API à un tiers, analyse la réponse et spécifie avec des paires nom/valeur de la réponse à envoyer à [!DNL Target].
1. at.js gère le scintillement et inclut les paires nom/valeur en tant que paramètres personnalisés dans la demande de Cible globale.
1. Marketer crée des audiences dans l’ [!DNL Target] interface en fonction de ces paramètres personnalisés.
1. Le spécialiste du marketing utilise ces audiences pour les expériences de cible, les activités et les mesures, ainsi que pour les audiences de rapports.

>[!NOTE]
>
>[!UICONTROL Les fournisseurs] de données nécessitent at.js 1.3 ou version ultérieure

## Documents complémentaires

* [Mise en oeuvre des fournisseurs de données dans at.js et Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
* [Documentation des fournisseurs de données](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)