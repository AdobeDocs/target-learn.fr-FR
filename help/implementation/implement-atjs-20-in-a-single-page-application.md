---
title: Mise en œuvre d’at.js 2.0 dans une application d’une seule page (SPA)
description: Adobe Target at.js 2.0 fournit de riches ensembles de fonctionnalités qui permettent à votre entreprise d’exécuter de la personnalisation sur des technologies côté client de nouvelle génération. Pour implémenter at.js 2.0 dans une application d’une seule page (SPA), procédez comme suit.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Implémentation d’Adobe Target at.js 2.0 dans une application monopage (SPA)

Adobe Target `at.js` 2.0 fournit des ensembles de fonctionnalités riches qui permettent à votre entreprise d’exécuter une personnalisation sur des technologies côté client de nouvelle génération. Cette version se concentre sur la mise à niveau des `at.js` pour avoir des interactions harmonieuses avec les applications d’une seule page (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/34765?quality=12&captions=fre_fr)

## Mise en œuvre d’at.js 2.0 dans une SPA

* Mettez en œuvre `at.js` 2.0 dans &lt;head> de votre application d’une seule page.
* Implémentez la fonction `adobe.target.triggerView()` à chaque modification d’affichage dans votre SPA. Pour ce faire, différentes techniques peuvent être utilisées, telles que l’écoute des modifications de hachage d’URL, l’écoute des événements personnalisés déclenchés par votre SPA ou l’incorporation du code `triggerView()` directement dans votre application. Vous devez choisir l’option qui fonctionne le mieux pour votre application monopage spécifique.
* Le nom de la vue est le premier paramètre de la fonction `triggerView()`. Utilisez des noms simples, clairs et uniques pour les rendre faciles à sélectionner dans le compositeur d’expérience visuelle de Target.
* Vous pouvez déclencher des vues dans de petites modifications d’affichage, ainsi que dans des contextes non SPA, comme à mi-chemin d’une page de défilement infinie.
* `at.js` 2.0 et `triggerView()` peuvent être implémentés via une solution de gestion des balises, telle qu’Adobe Experience Platform Launch.

## Limites d’at.js 2.0

Avant la mise à niveau, tenez compte des limites suivantes d’`at.js` 2.0 :

* Le suivi interdomaines n’est pas pris en charge dans `at.js` 2.0
* Les paramètres d’URL mboxOverride.browserIp et mboxSession ne sont pas pris en charge dans `at.js` 2.0
* Les fonctions héritées mboxCreate, mboxDefine et mboxUpdate sont obsolètes dans `at.js` 2.0. Le contenu par défaut s’affiche et aucune demande réseau n’est effectuée.

## Code de pied de page de bibliothèque utilisé dans la vidéo

Le code ci-dessous a été ajouté à la section Pied de bibliothèque de la bibliothèque `at.js` pendant la vidéo. Il se déclenche lors du premier chargement de l’application, puis lors de toute modification de hachage dans l’application. Il utilise une version nettoyée du hachage comme nom de vue et « home » lorsque le hachage est vide. Notez que pour identifier la SPA, le code recherche le texte « react/ » dans l’URL, qui devra probablement être mis à jour sur votre site. Gardez également à l’esprit qu’il peut être plus approprié pour votre SPA de déclencher des `triggerView()` d’événements personnalisés ou d’incorporer le code directement dans votre application.

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
* [Utiliser le compositeur d’expérience visuelle d’Adobe Target pour les applications monopages (VEC SPA)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
