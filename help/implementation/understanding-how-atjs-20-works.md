---
title: Fonctionnement d’at.js 2.0
description: at.js 2.0 améliore la prise en charge d’Adobe Target pour les applications d’une seule page (SPA) et s’intègre à d’autres solutions Experience Cloud. Cette vidéo et les diagrammes qui l'accompagnent expliquent comment tout s'assemble.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Fonctionnement d’Adobe Target at.js 2.0

`at.js` 2.0 améliore la prise en charge d’Adobe Target pour les applications d’une seule page (SPA) et s’intègre à d’autres solutions Experience Cloud. Cette vidéo et les diagrammes qui l&#39;accompagnent expliquent comment tout s&#39;assemble.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammes d’architecture

![Comportement at.js 2.0 au chargement de la page](assets/pageload.png)

1. L’appel renvoie un ID d’Experience Cloud (ECID). Si l’utilisateur est authentifié, un autre appel synchronise l’ID de client.

1. La bibliothèque `at.js` se charge de manière synchrone et masque le corps du document (`at.js` peut également être chargé de manière asynchrone avec un extrait de code de pré-masquage facultatif implémenté sur la page).

1. La requête de chargement de page est effectuée, y compris tous les paramètres configurés, ECID, SDID et ID de client.

1. Les scripts de profil s’exécutent et sont introduits dans le [!UICONTROL Profile Store]. Le magasin demande des audiences qualifiées auprès de [!UICONTROL Audience Library] (par exemple, audiences partagées depuis [!DNL Analytics], Audience Manager, etc.). [!UICONTROL Customer Attributes] sont envoyés à [!UICONTROL Profile Store] dans un traitement par lot.
1. En fonction de l’URL, des paramètres de requête et des données de profil, [!DNL Target] décide quelles activités et expériences renvoyer au visiteur pour la page active et les futures vues.

1. Contenu ciblé renvoyé à la page, comprenant éventuellement des valeurs de profil pour une personnalisation supplémentaire.

   Le contenu ciblé sur la page active est affiché aussi rapidement que possible, sans scintillement du contenu par défaut.

   Le contenu ciblé pour les futures vues d’une application d’une seule page est mis en cache dans le navigateur. Il peut donc être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. (Voir le diagramme suivant pour le comportement de `triggerView()`).

1. [!DNL Analytics] données envoyées de la page aux serveurs [!UICONTROL Data Collection]
1. [!DNL Target] les données sont associées aux données Analytics via le SDID et sont traitées dans le stockage de rapports [!DNL Analytics]. Les données [!DNL Analytics] peuvent ensuite être visualisées dans [!DNL Analytics] et [!DNL Target] au moyen de rapports A4T.

![Comportement at.js 2.0 lorsque la fonction triggerView() est utilisée](assets/triggerview.png)

1. `adobe.target.triggerView()` est appelé dans l’application monopage
1. Le contenu ciblé pour la vue est lu à partir du cache.

1. Le contenu ciblé est affiché aussi rapidement que possible sans scintillement du contenu par défaut.

1. La demande de notification est envoyée à [!DNL Target] [!UICONTROL Profile Store] pour compter le visiteur dans l’activité et incrémenter les mesures.
1. [!DNL Analytics] les données sont envoyées du SPA aux serveurs [!UICONTROL Data Collection]

1. Les données [!DNL Target] sont envoyées du serveur principal [!DNL Target] aux serveurs [!UICONTROL Data Collection]. Les données [!DNL Target] sont associées aux données [!DNL Analytics] via le SDID et sont traitées dans le stockage de rapports [!DNL Analytics]. Les données [!DNL Analytics] peuvent ensuite être visualisées dans [!DNL Analytics] et [!DNL Target] au moyen de rapports A4T.

## Ressources supplémentaires

* [Implémentation d’at.js 2.0 dans une application d’une seule page](implement-atjs-20-in-a-single-page-application.md)
* [Utilisation du compositeur d’expérience visuelle Adobe Target pour les applications d’une seule page (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
