---
title: Mise en œuvre des fournisseurs de données pour intégrer des données tierces
description: Ce tutoriel fournit des détails d’implémentation et des exemples d’utilisation de la fonctionnalité des fournisseurs de données d’Adobe Target pour récupérer des données de fournisseurs de données tiers et les transmettre dans la requête Target.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt:
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
TQID: 'https://experienceleague.adobe.com/Oh0ngUGA-ZfpPHnQnN0VRgUG1ta4yqg8Pfm8mhCZTN0'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: d11449f8685d14c2bbd1e70f80711d4edab9d3a1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%
---
# Implémentez [!UICONTROL fournisseurs de données] pour intégrer des données tierces à Adobe Target

Détails d’implémentation et exemples d’utilisation de la fonctionnalité Adobe Target [!UICONTROL Fournisseurs de données] pour récupérer des données auprès de fournisseurs de données tiers et les transmettre dans la requête Target.

>[!NOTE]
>
>[!UICONTROL Fournisseurs de données] nécessite la `at.js` 1.3 ou une version ultérieure

## Implémentation des composants de base des fournisseurs de données

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Aperçu rapide des composants de base d’un `dataProvider` et de la manière d’obtenir votre code dans le bon ordre.\
Un exemple de travail avec le code utilisé dans la vidéo se trouve ici :
[&#128279;](https://target.enablementadobe.com/data-providers/simple.html)

## Intégration à une API tierce

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Exemple plus réaliste, l’intégration d’une API de météo.\
Un exemple de travail avec le code utilisé dans la vidéo se trouve ici :
[&#128279;](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Intégration à plusieurs fournisseurs

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Comment incorporer des données provenant de plusieurs fournisseurs dans votre requête [!DNL Target] globale.\
Un exemple de travail avec le code utilisé dans la vidéo se trouve ici :
[&#128279;](https://target.enablementadobe.com/data-providers/combined.html)

## Réduire l’impact du chargement de page

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Réduisez l’impact sur le temps de chargement de la page en stockant les données dans un objet de stockage de session. Vous pouvez également transmettre les valeurs en tant que paramètres de profil à l’aide du préfixe `profile.`, et simplement les transmettre dans la première requête [!DNL Target] de la session. Cependant, vous seriez limité à transmettre cinquante paramètres de profil par requête.

Un exemple de travail avec le code utilisé dans la vidéo se trouve ici : [&#128279;](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Documents annexes

* [Utilisation des fournisseurs de données avec Adobe Target](use-data-providers-to-integrate-third-party-data.md)
