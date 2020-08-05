---
title: Présentation de l’API Adobe Target
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations comprend un ensemble dédié d'API qui vous permet de gérer votre catalogue de produits et/ou de contenu recommandés ; gérer vos algorithmes et campagnes de recommandations ; et diffuser des recommandations dans des objets JSON, HTML ou XML à afficher dans des canaux Web, mobiles, e-mail, IOT et autres.
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Présentation de l’API Adobe Target

Les API Adobe Target peuvent être regroupées en fonction du type.

| Type d’API | Ce qu&#39;il vous permet de faire | Lien de téléchargement |
| --- | --- | --- |
| Administration | Créez, modifiez et supprimez des activités, des audiences, des offres et d’autres objets (y compris [!DNL Recommendations] des entités, des critères, des conceptions, etc.). Les [!DNL Recommendations] API sont un type d’API d’administration.) | <UL><li>[Cible Admin API Collection Postman](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Collection Postman de l&#39;API Recommendations](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| Livraison | Récupérez du contenu optimisé et personnalisé pour [!DNL Target] la diffusion à un utilisateur final. | [Cible Diffusion API Collection Postman](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| Création de rapports | Exporter les résultats des activités et d’autres résultats de rapports. | Les API de Rapports sont incluses dans la collection [Postman de l&#39;API d&#39;administration de](https://developers.adobetarget.com/api/#admin-postman-collection)Cible. |
| Profil | Récupérez et modifiez les profils d’utilisateur stockés dans Adobe Target. | [Cible Profil API Collection Postman](https://developers.adobetarget.com/api/#profiles) |

Notez la distinction entre les API **** d’administration (y compris les [!DNL Recommendations] API), qui vous permettent de configurer divers aspects d’Adobe Target, et les API **** diffusion, qui vous permettent de récupérer du contenu. Les API d’administration nécessitent une authentification, contrairement aux API de diffusion.

Pour utiliser les API d’administration Adobe Target, vous devez d’abord configurer l’authentification à l’aide des E/S d’Adobe.

[Suivant : Configurer l’authentification >](configure-io-target-integration.md)
