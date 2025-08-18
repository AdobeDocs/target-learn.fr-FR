---
title: Mise en œuvre des fournisseurs de données pour intégrer des données tierces
description: Ce tutoriel fournit des détails d’implémentation et des exemples d’utilisation de la fonctionnalité des fournisseurs de données d’Adobe Target pour récupérer des données de fournisseurs de données tiers et les transmettre dans la requête Target.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Implémenter des [!UICONTROL Data Providers] pour intégrer des données tierces dans Adobe Target

Détails d’implémentation et exemples d’utilisation de la fonction [!UICONTROL Data Providers] d’Adobe Target pour récupérer des données à partir de fournisseurs de données tiers et les transmettre dans la requête Target.

>[!NOTE]
>
>[!UICONTROL Data Providers] nécessite `at.js` 1.3 ou une version ultérieure

## Implémentation des composants de base des fournisseurs de données

>[!VIDEO](https://video.tv.adobe.com/v/33871/?quality=12&captions=fre_fr)

Aperçu rapide des composants de base d’un `dataProvider` et de la manière d’obtenir votre code dans le bon ordre.\
Un exemple de travail avec le code utilisé dans la vidéo se trouve ici :
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Intégration à une API tierce

>[!VIDEO](https://video.tv.adobe.com/v/33857?captions=fre_fr)

Exemple plus réaliste, l’intégration d’une API de météo.\
Un exemple de travail avec le code utilisé dans la vidéo se trouve ici :
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Intégration à plusieurs fournisseurs

>[!VIDEO](https://video.tv.adobe.com/v/36722?captions=fre_fr)

Comment incorporer des données provenant de plusieurs fournisseurs dans votre requête [!DNL Target] globale.\
Un exemple de travail avec le code utilisé dans la vidéo se trouve ici :
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Réduire l’impact du chargement de page

>[!VIDEO](https://video.tv.adobe.com/v/36723?captions=fre_fr)

Réduisez l’impact sur le temps de chargement de la page en stockant les données dans un objet de stockage de session. Vous pouvez également transmettre les valeurs en tant que paramètres de profil à l’aide du préfixe `profile.`, et simplement les transmettre dans la première requête [!DNL Target] de la session. Cependant, vous seriez limité à transmettre cinquante paramètres de profil par requête.

Un exemple de travail avec le code utilisé dans la vidéo se trouve ici : [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Documents annexes

* [Utilisation des fournisseurs de données avec Adobe Target](use-data-providers-to-integrate-third-party-data.md)
