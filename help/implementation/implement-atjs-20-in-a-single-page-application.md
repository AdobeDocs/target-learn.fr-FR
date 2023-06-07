---
title: Implémentation d’at.js 2.0 dans une application d’une seule page (SPA)
description: Adobe Target at.js 2.0 fournit des ensembles de fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies côté client de nouvelle génération. Procédez comme suit pour implémenter at.js 2.0 dans une application d’une seule page (SPA).
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Implémentation d’Adobe Target at.js 2.0 dans une application d’une seule page (SPA)

Adobe Target `at.js` La version 2.0 fournit des ensembles de fonctionnalités riches qui permettent à votre entreprise d’exécuter la personnalisation sur les technologies côté client de nouvelle génération. Cette version est axée sur la mise à niveau. `at.js` pour avoir des interactions harmonieuses avec les applications d’une seule page (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implémentation d’at.js 2.0 dans un SPA

* Mise en oeuvre `at.js` 2,0 dans la variable &lt;head> de votre application d’une seule page.
* Mettez en oeuvre le `adobe.target.triggerView()` à chaque fois que l’affichage change dans votre SPA. Diverses techniques peuvent être utilisées à cet effet, par exemple l’écoute des modifications de hachage d’URL, l’écoute des événements personnalisés déclenchés par votre SPA ou l’incorporation des `triggerView()` code directement dans votre application. Vous devez choisir l’option qui fonctionne le mieux pour votre application d’une seule page spécifique.
* Le nom de la vue est le premier paramètre de la variable `triggerView()` fonction . Utilisez des noms simples, clairs et uniques pour faciliter leur sélection dans le compositeur d’expérience visuelle de Target.
* Vous pouvez déclencher des vues dans des changements de petites vues, ainsi que dans des contextes autres que SPA, tels que la mi-chemin vers le bas d’une page de défilement infini.
* `at.js` 2.0 et `triggerView()` peut être implémenté par le biais d’une solution de gestion des balises, telle qu’Adobe Experience Platform Launch.

## Limites d’at.js 2.0

Gardez à l’esprit les limites suivantes de `at.js` 2.0 avant la mise à niveau :

* Le suivi inter-domaines n’est pas pris en charge dans `at.js` 2,0
* Les paramètres mboxOverride.browserIp et mboxSession URL ne sont pas pris en charge dans `at.js` 2,0
* Les fonctions héritées mboxCreate, mboxDefine, mboxUpdate sont obsolètes dans `at.js` 2.0. Le contenu par défaut s’affiche et aucune demande réseau n’est effectuée.

## Code de pied de page de bibliothèque utilisé dans la vidéo

Le code ci-dessous a été ajouté à la section Pied de page de bibliothèque du `at.js` pendant la vidéo. Il se déclenche lors du premier chargement de l’application, puis lors de toute modification de hachage dans l’application. Il utilise une version nettoyée du hachage comme nom d’affichage et &quot;home&quot; lorsque le hachage est vide. Notez que pour identifier le SPA, le code recherche le texte &quot;response/&quot; dans l’URL, qui devra probablement être mis à jour sur votre site. Gardez également à l’esprit qu’il peut être plus approprié pour votre SPA de déclencher `triggerView()` hors des événements personnalisés ou en incorporant le code directement dans votre application.

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

* [Fonctionnement d’at.js 2.0 (Diagrammes d’architecture)](understanding-how-atjs-20-works.md)
* [Utilisation du compositeur d’expérience visuelle Adobe Target pour les applications d’une seule page (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
