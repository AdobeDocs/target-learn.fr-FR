---
title: Mise en oeuvre des fournisseurs de données pour intégrer des données tierces dans l’Adobe Target
seo-title: Mise en oeuvre des fournisseurs de données pour intégrer des données tierces dans l’Adobe Target
description: Les détails d’implémentation et des exemples d’utilisation de la fonction Fournisseurs de données d’Adobe Target pour récupérer des données de fournisseurs tiers et les transmettre dans la demande de Cible.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Mise en oeuvre des fournisseurs [!UICONTROL de] données pour intégrer des données tierces dans l’Adobe Target

Implementation details and examples of how to use Adobe Target&#39;s [!UICONTROL Data Providers] feature to retrieve data from third-party data providers and pass it in the Target request.

>[!NOTE]
>
>[!UICONTROL Les fournisseurs] de données requièrent `at.js` 1.3 ou une version supérieure

## Mise en oeuvre des composants de base des fournisseurs de données

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Aperçu rapide des composants de base d’un `dataProvider` et de la façon d’obtenir votre code dans le bon ordre.\
Vous trouverez un exemple pratique du code utilisé dans la vidéo ici :
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Intégration à une API tierce

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un exemple plus réaliste, intégrant une API météorologique.\
Vous trouverez un exemple pratique du code utilisé dans la vidéo ici :
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Intégration à plusieurs fournisseurs

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Comment incorporer des données provenant de plusieurs fournisseurs dans votre [!DNL Target] demande globale.\
Vous trouverez un exemple pratique du code utilisé dans la vidéo ici :
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimiser l’impact du chargement de page

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Réduisez l’impact sur le temps de chargement des pages en stockant les données dans un objet d’enregistrement de session. Vous pouvez également transmettre les valeurs en tant que paramètres de profil à l’aide du `profile.` préfixe et simplement les transmettre dans la première [!DNL Target] requête de la session. Cependant, vous ne pouvez transmettre que cinquante paramètres de profil par requête.

Vous trouverez un exemple pratique du code utilisé dans la vidéo ici : [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Documents complémentaires

* [Utiliser des fournisseurs de données avec Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentation des fournisseurs de données](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)