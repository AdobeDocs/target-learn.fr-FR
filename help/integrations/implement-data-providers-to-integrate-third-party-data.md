---
title: Comment mettre en oeuvre des fournisseurs de données pour intégrer des données tierces
description: Ce tutoriel fournit des détails de mise en oeuvre et des exemples d’utilisation de la fonction Fournisseurs de données Adobe Target pour récupérer les données de fournisseurs de données tiers et les transmettre dans la requête Target.
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
source-wordcount: '285'
ht-degree: 0%

---

# Mise en oeuvre [!UICONTROL Fournisseurs de données] pour intégrer des données tierces dans Adobe Target

Détails de mise en oeuvre et exemples d’utilisation d’Adobe Target [!UICONTROL Fournisseurs de données] pour récupérer des données de fournisseurs de données tiers et les transmettre dans la requête Target.

>[!NOTE]
>
>[!UICONTROL Fournisseurs de données] require `at.js` 1.3 ou version ultérieure

## Mise en oeuvre des composants de base des fournisseurs de données

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Présentation rapide des composants de base d’une `dataProvider` et comment obtenir votre code dans le bon ordre.\
Vous trouverez ici un exemple pratique avec le code utilisé dans la vidéo :
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Intégration à une API tierce

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Exemple plus réaliste, l’intégration d’une API météorologique.\
Vous trouverez ici un exemple pratique avec le code utilisé dans la vidéo :
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Intégration à plusieurs fournisseurs

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Comment incorporer des données de plusieurs fournisseurs dans votre global [!DNL Target] requête.\
Vous trouverez ici un exemple pratique avec le code utilisé dans la vidéo :
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimisation de l’impact de chargement de page

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Réduisez l’impact sur le délai de chargement des pages en stockant les données dans un objet de stockage de session. Vous pouvez également transmettre les valeurs en tant que paramètres de profil à l’aide de la variable `profile.` et transmettez-les simplement dans la première [!DNL Target] de la session. Cependant, vous êtes limité à la transmission de cinquante paramètres de profil par requête.

Vous trouverez ici un exemple pratique avec le code utilisé dans la vidéo : [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Supports

* [Utilisation des fournisseurs de données avec Adobe Target](use-data-providers-to-integrate-third-party-data.md)
