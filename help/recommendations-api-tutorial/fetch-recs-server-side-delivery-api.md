---
title: Comment récupérer Recommendations avec l’API de diffusion
description: Cette partie du tutoriel guide les développeurs à travers les étapes requises pour récupérer le contenu des recommandations à l’aide de l’API de diffusion Adobe Target.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 553d1208-647f-479d-acc7-d7760469d642
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 2%

---

# Récupération de [!DNL Recommendations] avec l’API de diffusion

Les API Adobe Target et Adobe Target [!DNL Recommendations] peuvent être utilisées pour envoyer des réponses aux pages web, mais également dans des expériences non HTMLS, y compris les applications, écrans, consoles, emails, kiosques et autres périphériques d’affichage. En d’autres termes, lorsque les bibliothèques [!DNL Target] et JavaScript ne peuvent pas être utilisés, l’ **[!DNL Target]API de diffusion** nous permet toujours d’accéder à l’ensemble des fonctionnalités [!DNL Target] pour offrir des expériences personnalisées.

>[!NOTE]
>
> Lorsque vous demandez du contenu contenant des recommandations réelles (produits ou éléments recommandés), utilisez l’API de diffusion [!DNL Target].

Pour récupérer les recommandations, envoyez un appel du POST de l’API de diffusion Adobe Target avec les informations contextuelles appropriées, qui peuvent inclure un ID utilisateur (à utiliser avec des recommandations spécifiques au profil telles que les éléments récemment consultés par l’utilisateur), le nom de mbox approprié, les paramètres de mbox, les paramètres de profil ou d’autres attributs. La réponse comprend les entity.ids recommandés (et peut inclure d’autres données d’entité) au format JSON ou HTML, qui peuvent ensuite être affichés sur l’appareil.

L’ [API de diffusion](https://developers.adobetarget.com/api/delivery-api/) pour Adobe Target expose toutes les fonctionnalités existantes fournies par une requête [!DNL Target] standard.

>[!NOTE]
>L’API de diffusion :
>* Permet de récupérer des expériences ou des offres pour un emplacement et une audience d’une manière RESTful.
>* Ne nécessite aucune authentification.
>* Publications uniquement.
>* Ne traite pas les cookies ni les appels de redirection.
>* Ne nécessite ni ne reconnaît les &quot;rôles utilisateur&quot;. Il récupère simplement du contenu ou signale des événements sur les serveurs Edge [!DNL Target].


Pour utiliser l’API de diffusion pour diffuser des [!DNL Target] expériences, y compris des recommandations, procédez comme suit :

1. Créez une activité [!DNL Target] (A/B, XT, AP ou [!DNL Recommendations]) à l’aide du compositeur d’après les formulaires (et non du compositeur d’expérience visuelle).
2. Utilisez l’API de diffusion pour obtenir une réponse aux requêtes générées par l’activité [!DNL Target] que vous venez de créer.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Création d’une recommandation à l’aide du compositeur d’expérience d’après les formulaires

Pour créer des recommandations qui peuvent être utilisées avec l’API de diffusion, utilisez le [compositeur d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

1. Tout d’abord, créez et enregistrez une conception basée sur JSON à utiliser dans votre recommandation. Pour obtenir un exemple de code JSON, ainsi que des informations d’arrière-plan sur la manière dont les réponses JSON peuvent être renvoyées lors de la configuration d’une activité basée sur les formulaires, consultez la documentation sur la [création de conceptions de recommandations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=en). Dans cet exemple, la conception est nommée *JSON simple.*

   ![côté serveur-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. Dans [!DNL Target], accédez à **[!UICONTROL Activités] > [!UICONTROL Créer une activité] > [!UICONTROL Recommendations]**, puis sélectionnez **[!UICONTROL Formulaire]**.

   ![côté serveur-create-recs.png](assets/server-side-create-recs.png)

3. Sélectionnez une propriété, puis cliquez sur **[!UICONTROL Suivant]**.
4. Définissez l’emplacement où vous souhaitez que les utilisateurs reçoivent la réponse de la recommandation. L’exemple ci-dessous utilise un emplacement nommé *api_charter*. Sélectionnez votre conception basée sur JSON, créée précédemment, nommée *JSON simple.*
   ![côté serveur-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Enregistrez et activez la recommandation. Cela produira des résultats. [Une fois les résultats prêts](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=en), vous pouvez utiliser l’API de diffusion pour les récupérer.

## Utilisation de l’API de diffusion

La syntaxe de l’[API de diffusion](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) est la suivante :

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Notez que le code client est requis. Pour rappel, votre code client se trouve dans Adobe Target en accédant à **[!UICONTROL Recommendations] > [!UICONTROL Paramètres]**. Notez la valeur **[!UICONTROL Code client]** dans la section **[!UICONTROL Jeton API de recommandation]** .
   ![client-code.png](assets/client-code.png)
1. Une fois que vous disposez de votre code client, créez votre appel API de diffusion. L’exemple ci-dessous commence par l’**[!UICONTROL appel de l’API de remise des mbox Web mise en cache]** fourni dans la [collection Postman de l’API de diffusion](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), en apportant des modifications pertinentes. Par exemple :
   * les objets **browser** et **address** ont été supprimés du **Body**, car ils ne sont pas nécessaires pour les cas d’utilisation non HTMLS.
   * *api_* charteris est répertorié comme nom de l’emplacement dans cet exemple
   * entity.id est spécifié, car cette recommandation est basée sur la similarité de contenu, ce qui nécessite qu’une clé d’élément actif soit transmise à [!DNL Target].
      ![server-side-Delivery-API-call.](assets/server-side-delivery-api-call2.png)
pngN’oubliez pas de configurer correctement vos paramètres de requête. Par exemple, veillez à spécifier 
`{{CLIENT_CODE}}` selon les besoins. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envoyez la requête. Cette opération s’exécute par rapport à l’emplacement *api_charter*, qui comporte une recommandation principale qui s’exécute dessus, définie avec votre conception JSON et qui génère une liste d’entités recommandées.
1. Recevez une réponse basée sur la conception JSON.
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
pngLa réponse inclut l’identifiant de clé, ainsi que les identifiants d’entité des entités recommandées.

L’utilisation de l’API de diffusion avec [!DNL Recommendations] permet ainsi d’effectuer des étapes supplémentaires avant d’afficher des recommandations au visiteur sur un périphérique autre que le périphérique HTML. Par exemple, vous pouvez utiliser la réponse de l’API de diffusion pour effectuer une recherche supplémentaire en temps réel des détails d’attribut d’entité (inventaire, prix, évaluation, etc.) à partir d’un autre système (tel qu’une plateforme CMS, PIM ou eCommerce), avant d’afficher les résultats finaux.

Grâce à l’approche décrite dans ce tutoriel, vous pouvez obtenir n’importe quelle application pour exploiter la réponse de [!DNL Target] afin de fournir des recommandations personnalisées.

## Exemple de mises en œuvre

Les ressources suivantes fournissent des exemples de différentes mises en oeuvre non axées sur les HTMLS. Gardez à l’esprit que chaque mise en oeuvre sera unique en raison du système et des périphériques impliqués.

| Ressource | Détails |
| --- | --- |
| [Adobe Target partout : implémentation côté serveur ou dans IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab qui offre une expérience pratique pour une application React qui tire parti des API côté serveur Adobe Target. |
| [Adobe Target dans une application mobile sans SDK Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Ce guide explique comment configurer Adobe Target dans votre application mobile sans installer le SDK Adobe. Cette solution utilise l’affichage web du SDK Tealium et le module Commandes distantes pour envoyer et recevoir des requêtes à l’API visiteur Adobe (Experience Cloud) et à l’API Adobe Target. |
| [Fonctionnement d’Adobe Target dans les applications mobiles](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html?lang=en) | Fonctionnement de [!DNL Target] avec le SDK Mobile |
| [Configuration  [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] des API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Étapes de configuration de l’extension [!DNL Target] dans Experience Platform Launch, ajout de l’extension [!DNL Target] à votre application et implémentation des API [!DNL Target] pour demander des activités, prérécupérer des offres et passer en mode aperçu visuel. |
| [Client de noeud Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | SDK Open Source [!DNL Target] Node.js v1.0 |
| [Présentation côté serveur](https://experienceleague.adobe.com/docs/target/using/implement-target/server-side/api-and-sdk-overview.html?lang=en) | Informations sur les API de diffusion côté serveur Adobe Target, les API de diffusion par lots côté serveur, le SDK Node.js et les API [!DNL Recommendations] Adobe Target. |
| [Recommendations de contenu Adobe Campaign dans Email](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog qui décrit comment exploiter les recommandations de contenu dans les emails via Adobe Target et Adobe I/O Runtime dans Adobe Campaign. |

## Gestion de la configuration [!DNL Recommendations] avec les API

La plupart du temps, les recommandations sont configurées dans l’interface utilisateur d’Adobe Target, puis utilisées ou accessibles via les API [!DNL Target], pour des raisons telles que celles mentionnées dans les sections ci-dessus. Cette coordination entre l’interface utilisateur et l’API est courante. Cependant, il arrive parfois que les utilisateurs souhaitent effectuer toutes les actions via les API (configuration, ainsi que l’utilisation des résultats). Bien que beaucoup moins courant, les utilisateurs peuvent absolument configurer, exécuter, *et* exploiter les résultats des recommandations entièrement à l’aide des API.

Nous avons appris dans une [section précédente](manage-catalog.md) comment gérer les entités Recommendations Adobe Target et les diffuser côté serveur. De même, Adobe I/O vous permet de gérer les critères, les promotions, les collections et les modèles de conception sans avoir à vous connecter à Adobe Target. Une liste complète de toutes les [!DNL Recommendations] API se trouve [ici](https://developers.adobetarget.com/api/recommendations/), mais voici un résumé à titre de référence.

| Ressource | Détails |
| --- | --- |
| [Collections](https://developers.adobetarget.com/api/recommendations/#tag/Collections) | Répertorier, créer, obtenir, modifier et supprimer des collections |
| [Critères](https://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Listez et obtenez des critères. |
| [Conceptions](https://developers.adobetarget.com/api/recommendations/#tag/Designs) | Répertorier, créer, obtenir, modifier, supprimer et valider des conceptions. |
| [Entités](https://developers.adobetarget.com/api/recommendations/#tag/Entities) | Enregistrez, supprimez et obtenez des entités. |
| [Promotions](https://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Répertorier, créer, obtenir, modifier et supprimer des promotions. |
| [Critères de catégorie](https://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères de catégorie. |
| [Critères personnalisés](https://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères personnalisés. |
| [Critères d’élément](https://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères d’élément. |
| [Critères de popularité](https://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères de popularité. |
| [Critères d’attribut de profil](https://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères d’attribut de profil. |
| [Critères récents](https://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Répertorier, créer, obtenir, modifier et supprimer des critères récents. |
| [Critères de séquence](https://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Lister, créer, obtenir, modifier et supprimer des critères de séquence. |

## Documentation de référence

* [Documentation de l’API Adobe Target](https://developers.adobetarget.com/api/#getting-started)
* [API de diffusion Adobe Target](https://developers.adobetarget.com/api/delivery-api/)
* [ [!DNL Recommendations] Intégration avec email](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html?lang=en)

## Résumé et révision

Félicitations ! En terminant ce tutoriel, vous avez appris à :
* [Gestion de votre catalogue à l’aide de l’API Recommendations](manage-catalog.md)
* [Gestion des critères personnalisés à l’aide de l’API Recommendations](manage-custom-criteria.md)
* [Utilisation de l’API de diffusion avec Recommendations](fetch-recs-server-side-delivery-api.md)
