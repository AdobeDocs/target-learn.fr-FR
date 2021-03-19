---
title: Comment implémenter des fournisseurs de données pour intégrer des données tierces
description: Ce didacticiel fournit des détails d’implémentation et des exemples d’utilisation de la fonction Fournisseurs de données Adobe Target pour récupérer des données auprès de fournisseurs de données tiers et les transmettre dans la demande de Cible.
role: Développeur
level: Expérience
topic: Personnalisation, intégrations
feature: Implémentation, intégrations, API/SDK
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Mettre en oeuvre [!UICONTROL les fournisseurs de données] pour intégrer des données tierces dans Adobe Target

Détails de l’implémentation et exemples d’utilisation de la fonction [!UICONTROL Fournisseurs de données] Adobe Target pour récupérer des données auprès de fournisseurs de données tiers et les transmettre dans la demande de Cible.

>[!NOTE]
>
>[!UICONTROL Les ] fournisseurs de données nécessitent la version  `at.js` 1.3 ou ultérieure

## Mise en oeuvre des composants de base des fournisseurs de données

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Présentation rapide des composants de base d&#39;un `dataProvider` et comment obtenir votre code dans le bon ordre.\
Vous trouverez un exemple pratique du code utilisé dans la vidéo ici :
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Intégration à une API tierce

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un exemple plus réaliste, intégrant une API météorologique.\
Vous trouverez un exemple pratique du code utilisé dans la vidéo ici :
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Intégration à plusieurs fournisseurs

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Comment incorporer des données de plusieurs fournisseurs dans votre requête globale [!DNL Target].\
Vous trouverez un exemple pratique du code utilisé dans la vidéo ici :
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimiser l’impact du chargement de page

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Réduisez l’impact sur le temps de chargement des pages en stockant les données dans un objet d’enregistrement de session. Vous pouvez également transmettre les valeurs en tant que paramètres de profil à l’aide du préfixe `profile.` et simplement les transmettre dans la première requête [!DNL Target] de la session. Cependant, vous ne pouvez transmettre que cinquante paramètres de profil par requête.

Vous trouverez un exemple pratique du code utilisé dans la vidéo ici : [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Documents complémentaires

* [Utilisation des fournisseurs de données avec Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentation des fournisseurs de données](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)