---
title: Mise en oeuvre d’Adobe Target at.js 2.0 dans une application monopage (SPA)
seo-title: Mise en oeuvre d’Adobe Target at.js 2.0 dans une application monopage (SPA)
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


# Mise en oeuvre d’Adobe Target at.js 2.0 dans une application monopage (SPA)

The newest version of `at.js` provides rich feature sets that equip your business to execute personalization on next-generation, client-side technologies. This new version is focused on upgrading `at.js` to have harmonious interactions with single page applications (SPAs).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implémentation d’at.js 2.0 dans une application d’une seule page

* Mettez en oeuvre la version `at.js` 2.0 dans le dossier &lt;head> de votre application d’une seule page.
* Mettez en oeuvre la `adobe.target.triggerView()` fonction chaque fois que la vue change dans votre application d’une seule page. Diverses techniques peuvent être utilisées pour ce faire, telles que l’écoute des modifications de hachage d’URL, l’écoute des événements personnalisés déclenchés par votre application d’une seule page d’accueil, ou l’incorporation directe du `triggerView()` code dans votre application. Choisissez l’option qui convient le mieux à votre application d’une seule page.
* Le nom de la vue est le premier paramètre de la `triggerView()` fonction. Utilisez des noms simples, clairs et uniques pour faciliter leur sélection dans le compositeur d’expérience visuelle de Cible.
* Vous pouvez déclencher des vues dans de petites modifications de vue, ainsi que dans des contextes autres que l’application d’une seule page (par exemple, à mi-chemin d’une page de défilement infini).
* `at.js` 2.0 et `triggerView()` peut être implémenté via une solution de gestion des balises, telle que Adobe Experience Platform Launch.

## Limites d’at.js 2.0

Veuillez tenir compte des restrictions suivantes de la version `at.js` 2.0 avant la mise à niveau :

* Le suivi inter-domaines n&#39;est pas pris en charge dans `at.js` 2.0
* Les paramètres mboxOverride.browserIp et mboxSession URL ne sont pas pris en charge dans la `at.js` version 2.0.
* Les fonctions héritées mboxCreate, mboxDefine, mboxUpdate sont obsolètes dans la `at.js` version 2.0. Le contenu par défaut s’affiche et aucune demande réseau n’est effectuée.

## Code de pied de page de bibliothèque utilisé dans la vidéo

Le code ci-dessous a été ajouté à la section Pied de page de la bibliothèque de la `at.js` bibliothèque pendant la vidéo. Il se déclenche lorsque l’application se charge pour la première fois, puis lors de toute modification de hachage dans l’application. Il utilise une version nettoyée du hachage comme nom de vue et &quot;home&quot; lorsque le hachage est vide. Notez que pour identifier l’application d’une seule page, le code recherche le texte &quot;réagir/&quot; dans l’URL, qui devra probablement être mis à jour sur votre site. N’oubliez pas non plus qu’il peut être plus approprié pour votre application d’une seule page d’accueil de se déclencher `triggerView()` des événements personnalisés ou d’incorporer directement le code dans votre application.

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
* [Utilisation du compositeur d’expérience visuelle d’Adobe Target pour les applications d’une seule page (compositeur d’expérience visuelle d’application monopage)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Mise à niveau de la documentation at.js 1.x vers at.js 2.0](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)