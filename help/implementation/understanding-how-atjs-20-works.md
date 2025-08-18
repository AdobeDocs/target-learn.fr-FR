---
title: Comment fonctionne at.js 2.0 ?
description: Découvrez comment at.js 2.0 améliore la prise en charge d’Adobe Target pour les applications monopages (SPA) et s’intègre à d’autres solutions Experience Cloud.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Comprendre comment fonctionne Adobe Target at.js 2.0

`at.js` 2.0 améliore la prise en charge d’Adobe Target pour les applications monopages (SPA) et s’intègre à d’autres solutions Experience Cloud. Cette vidéo et les diagrammes qui l’accompagnent expliquent comment tout se combine.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammes d’architecture

![comportement d’at.js 2.0 au chargement de la page](assets/pageload.png)

1. L’appel renvoie l’Experience Cloud ID (ECID). Si l’utilisateur est authentifié, un autre appel synchronise l’ID client.

1. `at.js` bibliothèque se charge de manière synchrone et masque le corps du document (`at.js` pouvez également être chargé de manière asynchrone avec un fragment de code de masquage préalable facultatif implémenté sur la page).

1. La requête de chargement de page est effectuée, y compris tous les paramètres configurés, ECID, SDID et ID de client.

1. Les scripts de profil s’exécutent et sont intégrés au [!UICONTROL Profile Store]. Le magasin demande des audiences qualifiées au [!UICONTROL Audience Library] (par exemple, des audiences partagées depuis [!DNL Analytics], Audience Manager, etc.). [!UICONTROL Customer Attributes] sont envoyés à [!UICONTROL Profile Store] dans un traitement par lots.
1. En fonction de l’URL, des paramètres de requête et des données de profil, [!DNL Target] décide des activités et expériences à renvoyer au visiteur pour la page actuelle et les vues futures

1. Contenu ciblé renvoyé à la page, comprenant éventuellement des valeurs de profil pour une personnalisation supplémentaire.

   Le contenu ciblé sur la page active est révélé le plus rapidement possible sans scintillement du contenu par défaut.

   Contenu ciblé pour les futures vues d’une application monopage mise en cache dans le navigateur, afin qu’elle puisse être appliquée instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. (Voir le diagramme suivant pour connaître le comportement des `triggerView()`).

1. [!DNL Analytics] les données envoyées de la page aux serveurs [!UICONTROL Data Collection]
1. [!DNL Target] données sont mises en correspondance avec les données Analytics via le SDID et sont traitées dans le stockage de rapports [!DNL Analytics]. [!DNL Analytics] données peuvent ensuite être affichées dans [!DNL Analytics] et [!DNL Target] via les rapports A4T.

![comportement d’at.js 2.0 lorsque la fonction triggerView() est utilisée](assets/triggerview.png)

1. `adobe.target.triggerView()` est appelé dans l’application monopage
1. Le contenu ciblé pour la vue est lu à partir du cache.

1. Le contenu ciblé est révélé le plus rapidement possible sans scintillement du contenu par défaut

1. Une demande de notification est envoyée au [!DNL Target] [!UICONTROL Profile Store] pour comptabiliser le visiteur dans l’activité et incrémenter les mesures
1. [!DNL Analytics] données sont envoyées de la SPA vers les serveurs [!UICONTROL Data Collection]

1. [!DNL Target] données sont envoyées du serveur principal [!DNL Target] aux serveurs [!UICONTROL Data Collection]. [!DNL Target] données sont mises en correspondance avec les données [!DNL Analytics] via le SDID et sont traitées dans le stockage de rapports [!DNL Analytics]. [!DNL Analytics] données peuvent ensuite être affichées dans [!DNL Analytics] et [!DNL Target] via les rapports A4T.

## Ressources supplémentaires

* [Implémentation d’at.js 2.0 dans une application monopage](implement-atjs-20-in-a-single-page-application.md)
* [Utiliser le compositeur d’expérience visuelle d’Adobe Target pour les applications monopages (VEC SPA)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
