---
title: Utilisation des fournisseurs de données pour intégrer des données tierces
description: Ce tutoriel présente aux utilisateurs et utilisatrices les fournisseurs de données. Découvrez comment utiliser la fonctionnalité Fournisseurs de données pour transmettre facilement des données de tiers à Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
TQID: https://experienceleague.adobe.com/XiUlJGHSFVxAMqdl6Y7hK9PoXOgiiUI43vrFeAj2Rpo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 16%

---

# Utilisation des fournisseurs de données pour intégrer des données tierces à Adobe Target

[!UICONTROL Fournisseurs de données] est une fonctionnalité qui vous permet de transmettre facilement des données de tiers à Target.  Un tiers peut être un service météorologique, une plateforme de gestion des données, ou même votre propre service web. Vous pouvez ensuite utiliser ces données pour créer des audiences, cibler du contenu et enrichir le profil du visiteur.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Utilisation des fournisseurs de données

1. Un expert en implémentation ajoute le code avant at.js (ou dans la section d’en-tête de bibliothèque d’at.js) qui effectue l’appel API au tiers, analyse la réponse et spécifie avec les paires nom/valeur de la réponse à envoyer à [!DNL Target].
1. at.js gère le scintillement et inclut les paires nom/valeur en tant que paramètres personnalisés dans la requête Target globale.
1. Le marketeur crée des audiences dans l’interface [!DNL Target] en fonction de ces paramètres personnalisés.
1. Le marketeur utilise ces audiences pour cibler les expériences, les activités et les mesures, ainsi que pour les audiences avec création de rapports.

>[!NOTE]
>
>[!UICONTROL Fournisseurs de données] nécessite at.js version 1.3 ou ultérieure.

## Documents annexes

* [Mise en œuvre des fournisseurs de données dans at.js et Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
