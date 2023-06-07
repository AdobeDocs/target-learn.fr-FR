---
title: Utilisation des fournisseurs de données pour intégrer des données tierces
description: Ce tutoriel présente les utilisateurs aux fournisseurs de données. Découvrez comment utiliser la fonctionnalité Fournisseurs de données pour transmettre facilement des données provenant de tiers à Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 25%

---

# Utilisation des fournisseurs de données pour intégrer des données tierces dans Adobe Target

[!UICONTROL L’option Fournisseurs de données est une fonctionnalité qui vous permet de transmettre facilement des données provenant de tiers à Target.  ]  Un tiers peut être un service météorologique, une plateforme de gestion des données, ou même votre propre service web. Vous pouvez ensuite utiliser ces données pour créer des audiences, cibler du contenu et enrichir le profil du visiteur.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Utilisation des fournisseurs de données

1. L’expert en implémentation ajoute du code avant at.js (ou dans la section En-tête de bibliothèque d’at.js) qui effectue l’appel API à un tiers, analyse la réponse et spécifie avec des paires nom/valeur de la réponse à envoyer à [!DNL Target].
1. at.js gère le scintillement et inclut les paires nom/valeur en tant que paramètres personnalisés dans la requête Target globale.
1. Le marketeur crée des audiences dans le [!DNL Target] en fonction de ces paramètres personnalisés.
1. Le marketeur utilise ces audiences pour cibler des expériences, des activités et des mesures, ainsi que pour les audiences avec création de rapports.

>[!NOTE]
>
>[!UICONTROL Fournisseurs de données] nécessite at.js 1.3 ou version ultérieure

## Supports

* [Implémentation des fournisseurs de données dans at.js et Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
