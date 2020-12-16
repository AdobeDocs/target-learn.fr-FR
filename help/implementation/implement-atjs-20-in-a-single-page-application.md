---
title: Mise en oeuvre de Adobe Target avec at.js 2.0 dans une application d’une seule page (SPA)
seo-title: Mise en oeuvre de Adobe Target avec at.js 2.0 dans une application d’une seule page (SPA)
description: La dernière version d’at.js propose des ensembles de fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies de nouvelle génération côté client. Cette nouvelle version vise à mettre à niveau at.js afin d’établir des interactions harmonieuses avec les applications monopages (SPA).
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 8%

---


# Mise en oeuvre de Adobe Target avec at.js 2.0 dans une application d’une seule page (SPA)

La nouvelle version de `at.js` fournit des ensembles de fonctionnalités riches qui permettent à votre entreprise d&#39;exécuter la personnalisation sur des technologies de nouvelle génération côté client. Cette nouvelle version se concentre sur la mise à niveau de `at.js` afin d’avoir des interactions harmonieuses avec les applications d’une seule page (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implémentation d’at.js 2.0 dans un SPA

* Implémentez `at.js` 2.0 dans l’&lt;head> de votre application d’une seule page.
* Mettez en oeuvre la fonction `adobe.target.triggerView()` chaque fois que la vue change dans votre SPA. Diverses techniques peuvent être utilisées pour ce faire, telles que l’écoute des modifications de hachage d’URL, l’écoute des événements personnalisés déclenchés par votre SPA ou l’incorporation directe du code `triggerView()` dans votre application. Choisissez l’option qui convient le mieux à votre application d’une seule page.
* Le nom de la vue est le premier paramètre de la fonction `triggerView()`. Utilisez des noms simples, clairs et uniques pour faciliter leur sélection dans le compositeur d’expérience visuelle de Cible.
* Vous pouvez déclencher des vues dans de petites modifications de vue, ainsi que dans des contextes non SPA, tels que la demi-descente d’une page de défilement infini.
* `at.js` 2.0 et  `triggerView()` peut être implémenté via une solution de gestion des balises, telle que Adobe Experience Platform Launch.

## Limites d’at.js 2.0

Tenez compte des limitations suivantes de `at.js` 2.0 avant la mise à niveau :

* Le suivi inter-domaines n&#39;est pas pris en charge dans `at.js` 2.0
* Les paramètres mboxOverride.browserIp et mboxSession URL ne sont pas pris en charge dans `at.js` 2.0
* Les fonctions héritées mboxCreate, mboxDefine, mboxUpdate sont obsolètes dans `at.js` 2.0. Le contenu par défaut s’affiche et aucune demande réseau n’est effectuée.

## Code de pied de page de bibliothèque utilisé dans la vidéo

Le code ci-dessous a été ajouté à la section Pied de page de bibliothèque de la bibliothèque `at.js` pendant la vidéo. Il se déclenche lorsque l’application se charge pour la première fois, puis lors de toute modification de hachage dans l’application. Il utilise une version nettoyée du hachage comme nom de vue et &quot;home&quot; lorsque le hachage est vide. Notez que pour identifier le SPA, le code recherche le texte &quot;response/&quot; dans l’URL, qui devra probablement être mis à jour sur votre site. N’oubliez pas non plus qu’il peut être plus approprié que votre SPA se déclenche `triggerView()` hors des événements personnalisés ou en incorporant directement le code dans votre application.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## Ressources supplémentaires

* [Fonctionnement d’at.js 2.0 (diagrammes d’architecture)](understanding-how-atjs-20-works.md)
* [Utilisation du compositeur d’expérience visuelle Adobe Target pour les applications d’une seule page (SPA compositeur d’expérience visuelle)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Mise à niveau de la documentation at.js 1.x vers at.js 2.0](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)