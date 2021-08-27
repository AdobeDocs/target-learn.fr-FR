---
title: Ajouter des paramètres aux requêtes
description: Dans cette leçon, nous allons ajouter des mesures de cycle de vie d’Adobe et des paramètres personnalisés aux requêtes Target ajoutées dans la leçon précédente. Ces mesures et paramètres seront utilisés ultérieurement dans le tutoriel pour créer des audiences personnalisées.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
exl-id: 0250e55f-a233-4060-84e1-86d1f88a6106
source-git-commit: ee58c7c85708722cf040cd9b039a2855dd390a16
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Ajouter des paramètres aux requêtes

Dans cette leçon, nous allons ajouter des mesures de cycle de vie d’Adobe et des paramètres personnalisés aux requêtes [!DNL Target] ajoutées dans la leçon précédente. Ces mesures et paramètres seront utilisés ultérieurement dans le tutoriel pour créer des audiences personnalisées.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Ajout des mesures de cycle de vie mobile Adobe
* Ajout de paramètres à une requête de prérécupération
* Ajout de paramètres à un emplacement dynamique
* Validation des paramètres des deux requêtes

## Ajout des paramètres de cycle de vie

Activez les [mesures de cycle de vie mobile d’Adobe](https://experienceleague.adobe.com/docs/mobile-services/android/metrics.html?lang=en). Cela permet d’ajouter des paramètres aux requêtes d’emplacement contenant des informations riches sur l’appareil de l’utilisateur et l’engagement avec l’application. Nous allons créer des audiences dans la leçon suivante en utilisant les données fournies par la requête de cycle de vie.

Pour activer les mesures de cycle de vie, ouvrez à nouveau le contrôleur HomeActivity et ajoutez `Config.collectLifecycleData(this);` à la fonction onResume() :

![Requête Lifecycle](assets/lifecycle_code.jpg)

### Validation des paramètres de cycle de vie de la requête de prérécupération

Exécutez l’émulateur et utilisez Logcat pour valider les paramètres de cycle de vie. Filtrez pour &quot;prérécupération&quot; afin de trouver la réponse de prérécupération et de rechercher les nouveaux paramètres :
![Validation du cycle de vie](assets/lifecycle_validation.jpg)

Bien que nous ayons uniquement ajouté `Config.collectLifecycleData()` au contrôleur HomeActivity, les mesures de cycle de vie envoyées avec la demande Target doivent également s’afficher sur votre écran de remerciement.

## Ajout du paramètre at_property à la requête de prérécupération

Les propriétés Adobe Target sont définies dans l’interface [!DNL Target] et sont utilisées pour établir des limites pour la personnalisation des applications et des sites web. Le paramètre at_property identifie la propriété spécifique sur laquelle vos offres et activités sont accessibles et gérées. Nous allons ajouter une propriété aux requêtes de prérécupération et d’emplacement actif.

>[!NOTE]
>
>Selon votre licence, les options Propriétés peuvent s’afficher ou non dans l’interface [!DNL Target]. Si vous ne disposez pas de ces options, ou si vous n’utilisez pas Propriétés dans votre entreprise, passez directement à la section suivante de cette leçon.

Vous pouvez récupérer votre valeur at_property dans l’interface [!DNL Target] sous [!UICONTROL Configuration] > [!UICONTROL Propriétés].  Pointez sur la propriété , sélectionnez l’icône de fragment de code et copiez la valeur `at_property` :

![Copier at_property](assets/at_property_interface.jpg)

Ajoutez-le en tant que paramètre pour chaque emplacement de la requête de prérécupération, comme suit :
![Ajouter le paramètre at_property](assets/params_at_property.jpg)
Voici le code mis à jour pour la fonction `targetPrefetchContent()` (veillez à mettre à jour la _[!UICONTROL valeur at_property , en cliquant ici]_ texte d’espace réservé!) :

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### Remarque À Propos Des Paramètres

Pour les futurs projets, vous souhaiterez peut-être implémenter des paramètres supplémentaires. La méthode `createTargetPrefetchObject()` permet trois types de paramètres : `locationParams`, `orderParams` et `productParams`. Pour [plus d’informations sur l’ajout de ces paramètres à la requête de prérécupération](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=en), consultez la documentation.

Notez également que différents paramètres d’emplacement peuvent être ajoutés à chaque emplacement dans la requête de prérécupération. Par exemple, vous pouvez créer une autre carte appelée param2, y placer un nouveau paramètre, puis définir param2 à un emplacement et param1 à l’autre emplacement. Voici un exemple :

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Validation du paramètre at_property dans la requête de prérécupération

Exécutez maintenant l’émulateur et utilisez Logcat pour vérifier que la propriété at_property s’affiche sur la requête et la réponse de prérécupération pour les deux emplacements :
![Validez le paramètre at_property](assets/parameters_at_property_validation.jpg)

## Ajout de paramètres personnalisés à la requête d’emplacement dynamique

La demande d’emplacement réel (wetravel_context_dest) a été ajoutée à la leçon précédente afin que nous puissions afficher une promotion appropriée sur l’écran de confirmation final du processus de réservation. Nous souhaitons personnaliser la promotion en fonction de la destination de l’utilisateur. Pour ce faire, nous l’ajouterons en tant que paramètre à la requête. Nous ajouterons également un paramètre pour l’origine trop et la valeur at_property.

Ajoutez les paramètres suivants à la fonction targetLoadRequest() du contrôleur ThankYouActivity :
![Ajouter des paramètres à la requête d’emplacement dynamique](assets/parameters_live_location.jpg)
Voici le code mis à jour pour la fonction targetLoadRequest() (veillez à mettre à jour le texte de l’espace réservé &quot;ajouter votre valeur at_property ici&quot;) :

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### Validation des paramètres personnalisés dans la requête d’emplacement dynamique

Exécutez l’émulateur et ouvrez Logcat. Filtrez l’un des paramètres pour vérifier que la requête contient les paramètres nécessaires :
![Validation des paramètres personnalisés dans la demande d’emplacement dynamique](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Requêtes et paramètres de confirmation de commande : Bien qu’il ne soit pas utilisé dans ce projet de démonstration, les détails de la commande sont généralement capturés dans une mise en oeuvre réelle. [!DNL Target] peut donc utiliser les détails de la commande comme mesures/dimensions. Reportez-vous à la documentation pour obtenir des instructions sur la [mise en oeuvre de la requête de confirmation de commande et des paramètres](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-target-methods.html?lang=en).

>[!NOTE]
>
>Analytics for Target (A4T) : Adobe Analytics peut être configuré comme source de création de rapports pour [!DNL Target]. Cela permet de visualiser toutes les mesures/dimensions collectées par le SDK Target dans Adobe Analytics. Pour plus d’informations, consultez la [Présentation d’A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=en) .

Beau travail ! Maintenant que les paramètres sont en place, nous sommes prêts à les utiliser pour créer des audiences et des offres dans Adobe Target.

**[SUIVANT : &quot;Créer des audiences et des offres&quot; >](create-audiences-and-offers.md)**
