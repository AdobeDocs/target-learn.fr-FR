---
title: Récupération de Recommendations avec l'API de Diffusion
description: Cette partie du didacticiel guide les développeurs à travers les étapes requises pour récupérer le contenu des recommandations à l’aide de l’API Adobe Target Diffusion.
role: Développeur
level: Intermédiaire
topic: Personnalisation, administration, intégrations, développement
feature: API/SDK, Recommendations, Administration et configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: 2c371ea17ce38928bcf3655a0d604a69e29963a0
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---


# Récupération de [!DNL Recommendations] avec l&#39;API de Diffusion

Les API Adobe Target et Adobe Target [!DNL Recommendations] peuvent être utilisées pour fournir des réponses aux pages Web, mais peuvent également être utilisées dans des expériences non HTML, y compris les applications, écrans, consoles, courriels, kiosques et autres périphériques d’affichage. En d’autres termes, lorsque les bibliothèques [!DNL Target] et JavaScript ne peuvent pas être utilisées, l’API de Diffusion **[!DNL Target]** nous permet toujours d’accéder à la gamme complète de fonctionnalités [!DNL Target] pour fournir des expériences personnalisées.

>[!NOTE]
>
> Lorsque vous demandez du contenu contenant des recommandations réelles (produits ou éléments recommandés), utilisez l&#39;API de Diffusion [!DNL Target].

Pour récupérer les recommandations, envoyez un appel du POST de l’API Diffusion Adobe Target avec les informations contextuelles appropriées, qui peuvent inclure un ID utilisateur (à utiliser avec des recommandations spécifiques au profil, telles que les éléments récemment consultés par l’utilisateur), un nom de mbox approprié, des paramètres de mbox, des paramètres de profil ou d’autres attributs. La réponse inclura des entity.ids recommandés (et peut inclure d&#39;autres données d&#39;entité) au format JSON ou HTML, qui peuvent ensuite être affichés sur le périphérique.

L’[API de Diffusion](https://developers.adobetarget.com/api/delivery-api/) pour Adobe Target présente toutes les fonctionnalités existantes fournies par une requête [!DNL Target] standard.

>[!NOTE]
>L&#39;API de Diffusion :
>* Permet de récupérer des expériences ou des offres pour un emplacement et une audience de manière RESTful.
>* Ne nécessite aucune authentification.
>* Uniquement les publications.
>* Ne traite pas les cookies ou les appels de redirection.
>* Ne nécessite pas ou ne reconnaît pas les &quot;rôles utilisateur&quot;. Il récupère simplement le contenu ou les événements de rapports sur les serveurs Edge [!DNL Target].


Pour utiliser l’API de Diffusion pour diffuser [!DNL Target] expériences, y compris des recommandations, procédez comme suit :

1. Créez une activité [!DNL Target] (A/B, XT, AP ou [!DNL Recommendations]) à l’aide du compositeur d’après les formulaires (et non du compositeur d’expérience visuelle).
2. Utilisez l&#39;API de Diffusion pour obtenir une réponse aux requêtes générées par l&#39;activité [!DNL Target] que vous venez de créer.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Création d’une recommandation à l’aide du compositeur d’expérience d’après les formulaires

Pour créer des recommandations pouvant être utilisées avec l’API de Diffusion, utilisez le [compositeur basé sur les formulaires](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html).

1. Tout d’abord, créez et enregistrez une conception JSON à utiliser dans votre recommandation. Pour un exemple de fichier JSON, plus des informations d’arrière-plan sur la façon dont les réponses JSON peuvent être renvoyées lors de la configuration d’une activité basée sur un formulaire, consultez la documentation sur [Création de conceptions de recommandations](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html). Dans cet exemple, la conception est nommée *JSON simple.*

   ![côté serveur-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. Dans [!DNL Target], accédez à **[!UICONTROL Activités] > [!UICONTROL Créer une Activité] > [!UICONTROL Recommendations]**, puis sélectionnez **[!UICONTROL Formulaire]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Sélectionnez une propriété, puis cliquez sur **[!UICONTROL Suivant]**.
4. Définissez l’emplacement où vous souhaitez que les utilisateurs reçoivent la réponse de la recommandation. L’exemple ci-dessous utilise un emplacement nommé *api_charter*. Sélectionnez votre conception basée sur JSON, créée précédemment, nommée *JSON simple.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Enregistrez et activez la recommandation. Il produira des résultats. [Une fois les résultats prêts](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), vous pouvez utiliser l&#39;API de Diffusion pour les récupérer.

## Utilisation de l’API de Diffusion

La syntaxe de l&#39;[API de Diffusion](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) est la suivante :

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Notez que le code client est requis. Pour rappel, votre code client peut être trouvé en Adobe Target en accédant à **[!UICONTROL Recommendations] > [!UICONTROL Paramètres]**. Notez la valeur **[!UICONTROL Code client]** dans la section **[!UICONTROL Jeton API de recommandation]**.
   ![client-code.png](assets/client-code.png)
1. Une fois que vous disposez de votre code client, générez votre appel d’API de Diffusion. L’exemple ci-dessous commence par l’**[!UICONTROL appel de l’API de Diffusion des mbox Web liées]** fourni dans la [collection Postman de l’API de Diffusion ](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), en apportant les modifications appropriées. Par exemple :
   * les objets **browser** et **address** ont été supprimés du **Body**, car ils ne sont pas requis pour les cas d&#39;utilisation non HTML.
   * *api_* charteris est répertorié comme nom d’emplacement dans cet exemple.
   * entity.id est spécifié, car cette recommandation est basée sur la similarité de contenu, ce qui nécessite qu’une clé d’élément active soit transmise à [!DNL Target].
      ![server-side-Diffusion-API-call.](assets/server-side-delivery-api-call2.png)
pngSouvenez-vous de configurer correctement vos paramètres de requête. Par exemple, veillez à spécifier 
`{{CLIENT_CODE}}` si nécessaire. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envoyez la demande. Cette opération s’exécute par rapport à l’emplacement *api_charter*, sur lequel une recommandation principale est exécutée, défini avec votre conception JSON qui génère une liste d’entités recommandées.
1. Recevez une réponse basée sur la conception JSON.
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
pngLa réponse comprend l’identifiant de clé, ainsi que les identifiants d’entité des entités recommandées.

L’utilisation de l’API de Diffusion avec [!DNL Recommendations] permet ainsi d’effectuer des étapes supplémentaires avant d’afficher les recommandations au visiteur sur le périphérique non HTML. Par exemple, vous pouvez utiliser la réponse de l’API de Diffusion pour effectuer une recherche supplémentaire en temps réel des détails d’attribut d’entité (inventaire, prix, évaluation, etc.) à partir d’un autre système (tel qu’un CMS, un PIM ou une plateforme de commerce électronique), avant d’afficher les résultats finaux.

En suivant l&#39;approche décrite dans ce tutoriel, vous pouvez obtenir n&#39;importe quelle application pour tirer parti de la réponse de [!DNL Target] pour fournir des recommandations personnalisées !

## Exemple de mises en œuvre

Les ressources suivantes fournissent des exemples d’implémentations non axées sur HTML. Gardez à l’esprit que chaque implémentation sera unique en raison du système et des périphériques impliqués.

| Ressource | Détails |
| --- | --- |
| [Consommation d&#39;API RESTful dans AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Comment créer et déployer un lot Adobe Experience Manager OSGi qui consomme des données d’un service Web RESTful tiers. |
| [Adobe Target Everywhere - Mise en oeuvre côté serveur ou dans l’IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab qui fournit une expérience pratique pour une application React qui exploite les API côté serveur Adobe Target. |
| [Adobe Target dans une application mobile sans le SDK Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Ce guide vous explique comment configurer l’Adobe Target dans votre application mobile sans installer le Adobe SDK. Cette solution utilise la vue Web Tealium SDK et le module Commandes distantes pour envoyer et recevoir des requêtes à l’API Visiteur Adobe (Experience Cloud) et à l’API Adobe Target. |
| [Fonctionnement d’Adobe Target dans les applications mobiles](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Fonctionnement de [!DNL Target] avec le SDK mobile |
| [Configuration  [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] des API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Procédure de configuration de l&#39;extension [!DNL Target] dans l&#39;Experience Platform Launch, d&#39;ajout de l&#39;extension [!DNL Target] à votre application et d&#39;implémentation des API [!DNL Target] pour demander des activités, prérécupérer des offres et entrer en mode prévisualisation visuelle. |
| [Client de noeud Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Kit SDK Open-Source [!DNL Target] Node.js v1.0 |
| [Présentation côté serveur](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Informations sur les API de diffusion côté serveur Adobe Target, les API de Diffusion de lot côté serveur, le SDK Node.js et les API Adobe Target [!DNL Recommendations]. |
| [Recommendations de contenu Adobe Campaign par courriel](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog qui décrit comment exploiter les recommandations de contenu dans les courriels via Adobe Target et Adobe I/O Runtime à Adobe Campaign. |

## Gestion de la configuration [!DNL Recommendations] avec les API

La plupart du temps, les recommandations sont configurées dans l’interface utilisateur Adobe Target, puis utilisées ou accessibles via les API [!DNL Target], pour des raisons telles que celles mentionnées dans les sections ci-dessus. Cette coordination IU-API est courante. Cependant, il arrive parfois que les utilisateurs souhaitent exécuter toutes les actions par le biais d’API, à la fois par la configuration et l’utilisation des résultats. Bien que beaucoup moins courant, les utilisateurs peuvent absolument configurer, exécuter, *et* exploiter les résultats des recommandations entièrement à l’aide des API.

Nous avons appris dans une section [antérieure](manage-catalog.md) comment gérer les entités Recommendations Adobe Target et les diffuser côté serveur. De même, Adobe I/O vous permet de gérer les critères, les promotions, les collections et les modèles de conception sans avoir à vous connecter à Adobe Target. Une liste complète de toutes les API [!DNL Recommendations] se trouve [ici](http://developers.adobetarget.com/api/recommendations/), mais voici un résumé pour référence.

| Ressource | Détails |
| --- | --- |
| [Collections](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Liste, création, obtention, modification et suppression de collections. |
| [Critères](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Liste et obtenir des critères. |
| [Conceptions](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Liste, création, obtention, modification, suppression et validation de conceptions. |
| [Entités](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Enregistrez, supprimez et obtenez des entités. |
| [Promotions](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Liste, création, obtention, modification et suppression de promotions. |
| [Critères de catégorie](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Liste, créer, obtenir, modifier et supprimer des critères de catégorie. |
| [Critères personnalisés](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Liste, création, obtention, modification et suppression de critères personnalisés. |
| [Critères d&#39;article](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Liste, création, obtention, modification et suppression de critères d’élément. |
| [Critères de popularité](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Liste, créer, obtenir, modifier et supprimer des critères de popularité. |
| [Critères d’attribut de profil](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Liste, création, obtention, modification et suppression de critères d’attribut de profil. |
| [Critères récents](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Liste, créer, obtenir, modifier et supprimer des critères récents. |
| [Critères de séquence](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Liste, création, obtention, modification et suppression de critères de séquence. |

## Documentation de référence

* [Documentation de l’API Adobe Target](https://developers.adobetarget.com/api/#getting-started)
* [API Diffusion Adobe Target](https://developers.adobetarget.com/api/delivery-api/)
* [ [!DNL Recommendations] Intégrer par courrier électronique](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Résumé et révision

Félicitations ! En terminant ce didacticiel, vous avez appris à :
* [Gérer votre catalogue à l’aide de l’API Recommendations](manage-catalog.md)
* [Gérer les critères personnalisés à l’aide de l’API Recommendations](manage-custom-criteria.md)
* [Utilisation de l’API de Diffusion avec Recommendations](fetch-recs-server-side-delivery-api.md)
