---
title: Fonctionnement d’at.js 2.0
description: at.js 2.0 améliore la prise en charge Adobe Target des applications d’une seule page (SPA) et s’intègre à d’autres solutions Experience Cloud. Cette vidéo et les diagrammes qui l'accompagnent expliquent comment tout se rassemble.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 21%

---


# Fonctionnement de Adobe Target avec at.js 2.0

`at.js` La version 2.0 améliore la prise en charge des applications d’une seule page par Adobe Target (SPA) et s’intègre à d’autres solutions Experience Cloud. Cette vidéo et les diagrammes qui l&#39;accompagnent expliquent comment tout se rassemble.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammes d&#39;architecture

![comportement d’at.js 2.0 au chargement de la page](assets/pageload.png)

1. L’appel renvoie l’ID d’Experience Cloud (ECID). Si l’utilisateur est authentifié, un autre appel synchronise l’ID de client.

1. `at.js` se charge de manière synchrone et masque le corps du document (`at.js` peut également être chargé de manière asynchrone avec un extrait de code de masquage automatique en option implémenté sur la page).

1. La demande de chargement de page comprend tous les paramètres configurés, ECID, SDID et ID de client.

1. Les scripts de profil s’exécutent et sont insérés dans le [!UICONTROL Profil Store]. Le magasin demande des audiences qualifiées à la [!UICONTROL bibliothèque d&#39;Audiences] (par exemple, audiences partagées à partir de [!DNL Analytics], Audience Manager, etc.). [!UICONTROL Les ] attributs du client sont envoyés à  [!UICONTROL Profil ] Storein dans un traitement par lot.
1. En fonction de l’URL, des paramètres de requête et des données de profil, [!DNL Target] décide quelles Activités et expériences renvoyer au visiteur pour la page active et les futures vues.

1. Contenu ciblé renvoyé à la page, incluant éventuellement des valeurs de profil pour une personnalisation supplémentaire.

   Le contenu ciblé sur la page actuelle est affiché aussi rapidement que possible, sans scintillement du contenu par défaut.

   Le contenu ciblé pour les futures vues d’une application d’une seule page est mis en cache dans le navigateur, de sorte qu’il peut être immédiatement appliqué sans appel de serveur supplémentaire lorsque les vues sont déclenchées. (Voir le diagramme suivant pour le comportement de `triggerView()`).

1. [!DNL Analytics] données envoyées de la page aux serveurs de  [!UICONTROL collecte de ] données
1. [!DNL Target]Les données sont associées aux données par l’intermédiaire du SDID et sont traitées dans le magasin de rapports Analytics. [!DNL Analytics] [!DNL Analytics] les données peuvent ensuite être visualisées dans  [!DNL Analytics] et  [!DNL Target] via les rapports A4T.

![comportement d’at.js 2.0 lorsque la fonction triggerView() est utilisée](assets/triggerview.png)

1. `adobe.target.triggerView()` est appelé dans l’application d’une seule page
1. Le contenu ciblé pour la vue est lu à partir du cache

1. Le contenu ciblé s’affiche aussi rapidement que possible, sans scintillement du contenu par défaut

1. La demande de notification est envoyée au magasin de profils [!DNL Target] pour compter le visiteur dans l’activité et incrémenter les mesures
1. [!DNL Analytics] les données sont envoyées du SPA aux serveurs de  [!UICONTROL collecte de ] données

1. [!DNL Target] les données sont envoyées depuis l’ [!DNL Target] arrière-plan aux serveurs  [!UICONTROL de ] collecte de données. Les données [!DNL Target] sont associées aux données [!DNL Analytics] par l’intermédiaire du SDID et sont traitées dans le magasin de rapports [!DNL Analytics]. [!DNL Analytics] les données peuvent ensuite être visualisées dans  [!DNL Analytics] et  [!DNL Target] via les rapports A4T.

## Ressources supplémentaires

* [Mise en oeuvre d’at.js 2.0 dans une application d’une seule page](implement-atjs-20-in-a-single-page-application.md)
* [Utilisation du compositeur d’expérience visuelle Adobe Target pour les applications d’une seule page (SPA compositeur d’expérience visuelle)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Documentation du fonctionnement d’at.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)