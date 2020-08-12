---
title: Récupération de Recommendations avec l'API de Diffusion
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations comprend un ensemble dédié d'API qui vous permet de gérer votre catalogue de produits et/ou de contenu recommandés ; gérer vos algorithmes et campagnes de recommandations ; et diffuser des recommandations dans des objets JSON, HTML ou XML à afficher dans des canaux Web, mobiles, e-mail, IOT et autres.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 7265fd8611aacc94d1a66c10cd641c0644f2d43f
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 0%

---


# Récupération [!DNL Recommendations] avec l’API de Diffusion

Les [!DNL Recommendations] API Adobe Target et Adobe Target peuvent être utilisées pour fournir des réponses aux pages Web, mais aussi dans les expériences non HTML, y compris les applications, écrans, consoles, courriels, kiosques et autres périphériques d’affichage. En d’autres termes, lorsque [!DNL Target] les bibliothèques et JavaScript ne peuvent pas être utilisés, l’API **[!DNL Target]de **Diffusion nous permet toujours d’accéder à la gamme complète de fonctionnalités[!DNL Target]pour fournir des expériences personnalisées.

>[!NOTE]
>
> Lorsque vous demandez du contenu contenant des recommandations réelles (produits ou articles recommandés), utilisez l’API [!DNL Target] Diffusion.

Pour récupérer les recommandations, envoyez un appel du POST de l’API Diffusion Adobe Target avec les informations contextuelles appropriées, qui peuvent inclure un ID d’utilisateur (à utiliser avec les recommandations spécifiques au profil telles que les éléments récemment consultés par l’utilisateur), le nom de mbox approprié, les paramètres de mbox, les paramètres de profil ou d’autres attributs. La réponse inclura des entity.ids recommandés (et peut inclure d&#39;autres données d&#39;entité) au format JSON ou HTML, qui peuvent ensuite être affichés sur le périphérique.

L’API [de](https://developers.adobetarget.com/api/delivery-api/) Diffusion pour Adobe Target expose toutes les fonctionnalités existantes fournies par une [!DNL Target] requête standard.

>[!NOTE]
>L&#39;API de Diffusion :
>* Permet de récupérer des expériences ou des offres pour un emplacement et une audience de manière RESTful.
>* Ne nécessite aucune authentification.
>* Uniquement les publications.
>* Ne traite pas les cookies ou les appels de redirection.
>* Ne nécessite pas ou ne reconnaît pas les &quot;rôles utilisateur&quot;. Il récupère simplement le contenu ou les rapports de événements sur les serveurs [!DNL Target] périphériques.


Pour utiliser l’API de Diffusion pour diffuser des [!DNL Target] expériences, y compris des recommandations, procédez comme suit :

1. Créez une [!DNL Target] activité (A/B, XT, AP ou [!DNL Recommendations]) à l’aide du compositeur d’après les formulaires (et non du compositeur d’expérience visuelle).
2. Utilisez l’API de Diffusion pour obtenir une réponse aux requêtes générées par l’ [!DNL Target] activité que vous venez de créer.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Création d’une recommandation à l’aide du compositeur d’expérience d’après les formulaires

Pour créer des recommandations pouvant être utilisées avec l’API de Diffusion, utilisez le compositeur [basé sur](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)les formulaires.

1. Tout d’abord, créez et enregistrez une conception JSON à utiliser dans votre recommandation. Pour un exemple de fichier JSON, plus des informations d’arrière-plan sur la manière dont les réponses JSON peuvent être renvoyées lors de la configuration d’une activité basée sur un formulaire, consultez la documentation sur la [création de conceptions](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html)de recommandations. Dans cet exemple, la conception s’appelle *JSON simple.*

   ![côté serveur-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. Dans [!DNL Target], accédez à **[!UICONTROL Activités]>[!UICONTROL Créer une Activité]>[!UICONTROL Recommendations]**, puis sélectionnez Form.****

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Sélectionnez une propriété, puis cliquez sur **[!UICONTROL Suivant]**.
4. Définissez l’emplacement où vous souhaitez que les utilisateurs reçoivent la réponse de la recommandation. L’exemple ci-dessous utilise un emplacement nommé *api_charter*. Sélectionnez votre conception basée sur JSON, créée précédemment et nommée *JSON simple.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Enregistrez et activez la recommandation. Il produira des résultats. [Une fois les résultats prêts](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), vous pouvez utiliser l&#39;API de Diffusion pour les récupérer.

## Utilisation de l’API de Diffusion

The syntax for the [Delivery API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) is:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Notez que le code client est requis. Pour rappel, votre code client peut être trouvé dans Adobe Target en accédant à **[!UICONTROL Recommendations]>[!UICONTROL Paramètres]**. Notez la valeur Code **** client dans la section Jeton **[!UICONTROL API]** de recommandation.
   ![client-code.png](assets/client-code.png)
1. Une fois que vous disposez de votre code client, générez votre appel d’API de Diffusion. L’exemple ci-dessous commence par l’appel **[!UICONTROL de l’API de Diffusion Mbox]** WebBatched [fourni dans la collection](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)Postman de l’API deDiffusion, en apportant les modifications appropriées. Par exemple :
   * les objets **browser** et **address** ont été supprimés du **Body**, car ils ne sont pas requis pour les cas d&#39;utilisation non HTML.
   * *api_charter* est répertorié comme nom d&#39;emplacement dans cet exemple.
   * entity.id est spécifié, car cette recommandation est basée sur la similarité de contenu, ce qui nécessite la transmission d’une clé d’élément actuelle à [!DNL Target].
      ![server-side-Diffusion-API-call.png](assets/server-side-delivery-api-call2.png)Souvenez-vous de configurer correctement vos paramètres de requête. Par exemple, veillez à spécifier`{{CLIENT_CODE}}` si nécessaire. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envoyez la demande. Cette opération s’exécute par rapport à l’emplacement *api_charter* , sur lequel s’exécute une recommandation principale, définie avec votre conception JSON qui génère une liste d’entités recommandées.
1. Recevez une réponse basée sur la conception JSON.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)La réponse comprend l’identifiant de clé, ainsi que les identifiants d’entité des entités recommandées.

L’utilisation de l’API de Diffusion [!DNL Recommendations] ainsi permet d’effectuer des étapes supplémentaires avant d’afficher des recommandations au visiteur sur un périphérique non HTML. Par exemple, vous pouvez utiliser la réponse de l’API de Diffusion pour effectuer une recherche supplémentaire en temps réel des détails d’attribut d’entité (inventaire, prix, évaluation, etc.) à partir d’un autre système (tel qu’un CMS, un PIM ou une plateforme de commerce électronique), avant d’afficher les résultats finaux.

En suivant l&#39;approche décrite dans ce tutoriel, vous pouvez obtenir n&#39;importe quelle application pour tirer parti de la réponse de [!DNL Target] pour fournir des recommandations personnalisées !

## Exemple de mises en œuvre

Les ressources suivantes fournissent des exemples d’implémentations non axées sur HTML. Gardez à l’esprit que chaque implémentation sera unique en raison du système et des périphériques impliqués.

| Ressource | Détails |
| --- | --- |
| [Consommation d&#39;API RESTful dans AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Comment créer et déployer un lot Adobe Experience Manager OSGi qui consomme des données d’un service Web RESTful tiers. |
| [Adobe Target Everywhere - Mise en oeuvre côté serveur ou dans l’IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab qui fournit une expérience pratique pour une application React qui exploite les API côté serveur Adobe Target. |
| [Adobe Target dans une application mobile sans le SDK Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Ce guide vous explique comment configurer l’Adobe Target dans votre application mobile sans installer le Adobe SDK. Cette solution utilise la vue Web Tealium SDK et le module Commandes distantes pour envoyer et recevoir des requêtes à l’API Visiteur Adobe (Experience Cloud) et à l’API Adobe Target. |
| [Fonctionnement d’Adobe Target dans les applications mobiles](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Fonctionnement [!DNL Target] du kit SDK Mobile |
| [Configuration [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] des API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Cette section décrit la procédure à suivre pour configurer l’ [!DNL Target] extension dans l’Experience Platform Launch, ajouter l’ [!DNL Target] extension à votre application et mettre en oeuvre [!DNL Target] des API pour demander des activités, prérécupérer des offres et passer en mode prévisualisation visuel. |
| [Client de noeud Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | SDK Open-Source [!DNL Target] Node.js v1.0 |
| [Présentation côté serveur](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Informations sur les API de diffusion côté serveur Adobe Target, les API de Diffusion par lot côté serveur, le SDK Node.js et les API Adobe Target [!DNL Recommendations] s. |
| [Recommendations de contenu Adobe Campaign par courriel](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog qui décrit comment exploiter les recommandations de contenu dans les courriels via Adobe Target et Adobe I/O Runtime à Adobe Campaign. |

## Gestion de la [!DNL Recommendations] configuration à l&#39;aide des API

La plupart du temps, les recommandations sont configurées dans l’interface utilisateur Adobe Target, puis utilisées ou accessibles via les [!DNL Target] API, pour des raisons telles que celles mentionnées dans les sections ci-dessus. Cette coordination IU-API est courante. Cependant, il arrive parfois que les utilisateurs souhaitent exécuter toutes les actions par le biais d’API, à la fois par la configuration et l’utilisation des résultats. Bien que beaucoup moins courant, les utilisateurs peuvent absolument configurer, exécuter *et exploiter les* résultats de recommandations entièrement à l’aide des API.

Nous avons appris dans une section [](manage-catalog.md) précédente comment gérer les entités Adobe Target et les diffuser côté serveur. De même, les E/S d&#39;Adobe vous permettent de gérer les critères, les promotions, les collections et les modèles de conception sans avoir à vous connecter à Adobe Target. Une liste complète de toutes les [!DNL Recommendations] API se trouve [ici](http://developers.adobetarget.com/api/recommendations/), mais voici un résumé pour référence.

| Ressource | Détails |
| --- | --- |
| [Collections](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Liste, création, obtention, modification et suppression de collections. |
| [Critères](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Liste et obtenir des critères. |
| [Conceptions](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Liste, création, obtention, modification, suppression et validation de conceptions. |
| [Entités](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Enregistrez, supprimez et obtenez des entités. |
| [Promotions](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Liste, création, obtention, modification et suppression de promotions. |
| [Critères de Catégorie](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Liste, créer, obtenir, modifier et supprimer des critères de catégorie. |
| [Critères personnalisés](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Liste, création, obtention, modification et suppression de critères personnalisés. |
| [Critères d&#39;article](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Liste, création, obtention, modification et suppression de critères d’élément. |
| [Critères de popularité](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Liste, créer, obtenir, modifier et supprimer des critères de popularité. |
| [Critères d’attribut de Profil](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Liste, création, obtention, modification et suppression de critères d’attribut de profil. |
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