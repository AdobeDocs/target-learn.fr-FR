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
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 21%

---

# Fonctionnement d’Adobe Target at.js 2.0

`at.js` La version 2.0 améliore la prise en charge d’Adobe Target pour les applications d’une seule page (SPA) et s’intègre à d’autres solutions Experience Cloud. Cette vidéo et les diagrammes qui l&#39;accompagnent expliquent comment tout s&#39;assemble.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagrammes d’architecture

![Comportement d’at.js 2.0 au chargement de la page](assets/pageload.png)

1. L’appel renvoie un ID d’Experience Cloud (ECID). Si l’utilisateur est authentifié, un autre appel synchronise l’ID de client.

1. `at.js` La bibliothèque se charge de manière synchrone et masque le corps du document (`at.js`  peut également être chargé de manière asynchrone avec un extrait de code de pré-masquage facultatif implémenté sur la page).

1. La requête de chargement de page est effectuée, y compris tous les paramètres configurés, ECID, SDID et ID de client.

1. Les scripts de profil s’exécutent et sont introduits dans la [!UICONTROL banque de profils]. Le magasin demande des audiences qualifiées auprès de la [!UICONTROL bibliothèque d’audiences] (par exemple, audiences partagées depuis [!DNL Analytics], Audience Manager, etc.). [!UICONTROL Les ] attributs du client sont envoyés dans le  [!UICONTROL magasin de ] profils par lots.
1. En fonction de l’URL, des paramètres de requête et des données de profil, [!DNL Target] décide quelles activités et expériences renvoyer au visiteur pour la page active et les futures vues.

1. Contenu ciblé renvoyé à la page, comprenant éventuellement des valeurs de profil pour une personnalisation supplémentaire.

   Le contenu ciblé sur la page actuelle est affiché aussi rapidement que possible, sans scintillement du contenu par défaut.

   Le contenu ciblé pour les futures vues d’une application d’une seule page est mis en cache dans le navigateur. Il peut donc être appliqué instantanément sans appel au serveur supplémentaire lorsque les vues sont déclenchées. (Voir le diagramme suivant pour connaître le comportement de `triggerView()`).

1. [!DNL Analytics] données envoyées de la page aux  [!UICONTROL serveurs de ] collecte de données
1. [!DNL Target]Les données sont associées aux données par l’intermédiaire du SDID et sont traitées dans le magasin de rapports Analytics. [!DNL Analytics] [!DNL Analytics] Les données peuvent ensuite être visualisées dans  [!DNL Analytics] et  [!DNL Target] via les rapports A4T.

![Comportement d’at.js 2.0 lorsque la fonction triggerView() est utilisée](assets/triggerview.png)

1. `adobe.target.triggerView()` est appelé dans l’application d’une seule page
1. Le contenu ciblé pour la vue est lu à partir du cache

1. Le contenu ciblé s’affiche aussi rapidement que possible, sans scintillement du contenu par défaut

1. La demande de notification est envoyée au magasin de profils [!DNL Target] pour compter le visiteur dans l’activité et incrémenter les mesures
1. [!DNL Analytics] Les données sont envoyées du SPA aux serveurs de   collecte de données

1. [!DNL Target] Les données sont envoyées du  [!DNL Target] serveur principal aux serveurs de  [!UICONTROL collecte de ] données. Les données [!DNL Target] sont associées aux données [!DNL Analytics] par l’intermédiaire du SDID et sont traitées dans le magasin de rapports [!DNL Analytics]. [!DNL Analytics] Les données peuvent ensuite être visualisées dans  [!DNL Analytics] et  [!DNL Target] via les rapports A4T.

## Ressources supplémentaires

* [Implémentation d’at.js 2.0 dans une application d’une seule page](implement-atjs-20-in-a-single-page-application.md)
* [Utilisation du compositeur d’expérience visuelle Adobe Target pour les applications d’une seule page (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Documentation du fonctionnement d’at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en)
