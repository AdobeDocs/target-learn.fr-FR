---
title: Ajout de requêtes Adobe Target
description: Le SDK Mobile Services Adobe (v4) fournit des méthodes et fonctionnalités Adobe Target qui vous permettent de personnaliser votre application avec différentes expériences pour différents utilisateurs.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 88a5be3f-d61f-43e7-997a-574ef56122ed
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# Ajout de requêtes Adobe Target

Le SDK Mobile Services Adobe (v4) fournit des méthodes et fonctionnalités Adobe Target qui vous permettent de personnaliser votre application avec différentes expériences pour différents utilisateurs. En règle générale, une ou plusieurs demandes sont envoyées de l’application à Adobe Target pour récupérer le contenu personnalisé et mesurer l’impact de ce contenu.

Dans cette leçon, vous préparerez l’application We.Travel pour la personnalisation en implémentant des requêtes [!DNL Target].

## Conditions préalables

Veillez à [télécharger et mettre à jour l’exemple d’application](download-and-update-the-sample-app.md).

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Mettre en cache plusieurs offres [!DNL Target] (c’est-à-dire du contenu personnalisé) à l’aide d’une requête de prérécupération par lots
* Charger les emplacements [!DNL Target] prérécupérés
* Charger un emplacement [!DNL Target] en temps réel (non prérécupéré)
* Effacer les emplacements prérécupérés du cache
* Validation des requêtes prérécupérées et en temps réel

## Terminologie 

Vous trouverez ci-dessous quelques-uns des termes clés de Target que nous utiliserons dans le reste de ce tutoriel.

* **Demander :** une requête réseau aux serveurs Adobe Target
* **Offre :** : fragment de code ou autre contenu textuel, défini dans l’interface utilisateur de [!DNL Target] (ou avec l’API), qui est fourni dans la réponse. Généralement, JSON est utilisé dans les applications mobiles natives lorsque [!DNL Target] est utilisé.
* **Emplacement :** nom défini par l’utilisateur donné à une requête, utilisé dans l’interface [!DNL Target] pour associer des offres à des requêtes spécifiques
* **Requête par lot :** une requête unique qui comprend plusieurs emplacements
* **Requête de prérécupération :** requête unique qui récupère les offres et les met en cache en mémoire pour une utilisation ultérieure dans l’application.
* **Requête de prérécupération par lots :** demande unique qui prérécupère les offres pour plusieurs emplacements
* **Audience :** groupe de visiteurs défini dans l’interface [!DNL Target] ou partagé avec [!DNL Target] à partir d’autres applications d’Adobe (par exemple, &quot;Visiteurs iPhone X&quot;, &quot;Visiteurs en Californie&quot;, &quot;Première ouverture d’application&quot;)
* **Activité :** un concept [!DNL Target], défini dans l’interface utilisateur de [!DNL Target] (ou avec l’API) qui relie des emplacements, des offres et des audiences pour créer une expérience personnalisée.

## Ajout d’une requête de prérécupération par lots

La première requête que nous allons implémenter dans We.Travel est une requête de prérécupération par lots avec deux emplacements [!DNL Target] sur l’écran d’accueil. Dans une leçon ultérieure, nous configurerons des offres pour ces emplacements qui affichent des messages afin de guider les nouveaux utilisateurs tout au long du processus de réservation.

Une requête de prérécupération récupère le contenu [!DNL Target] aussi minimalement que possible en mettant en cache la réponse du serveur Adobe Target (offre). Une requête de prérécupération par lots récupère et met en cache plusieurs offres, chacune étant associée à un emplacement différent. Tous les emplacements prérécupérés sont mis en cache sur le périphérique en vue d’une utilisation ultérieure dans la session utilisateur. En prérécupérant plusieurs emplacements sur l’écran d’accueil, nous pouvons récupérer les offres à utiliser ultérieurement lorsque le visiteur parcourt l’application. Pour plus d’informations sur les méthodes de prérécupération, reportez-vous à la [documentation de prérécupération](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=en) .

### Ajout de la requête de prérécupération par lots

Mettons à jour le contrôleur HomeActivity (le code source de l’écran d’accueil), qui se trouve sous app > main > java > com.wetravel > Controller. Nous ajouterons les deux blocs de code affichés en rouge :

Commençons par le contrôleur HomeActivity (le code source de l’écran d’accueil), qui se trouve sous app > main > java > com.wetravel > Controller.

Nous ajouterons les deux blocs de code affichés en rouge :

![Code de prérécupération HomeActivity](assets/homeactivity.jpg)

Faites défiler l’écran jusqu’à la fin du code HomeActivity et ajoutez le code fourni ci-dessous après la fonction `setHeader()` et *en remplaçant* la fonction `onResume()` actuelle :

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

Votre IDE vous avertira probablement que vous n’avez pas les classes [!DNL Target] importées dans le fichier. Veillez à importer les classes [!DNL Target] en haut du contrôleur HomeActivity, comme illustré en rouge ci-dessous :

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importation des classes Target](assets/import.jpg)

Vous verrez probablement également des erreurs pour &quot;la variable de symbole wetravel_engage_home est introuvable&quot; et &quot;la variable de symbole wetravel_engage_search est introuvable&quot;. Ajoutez-les au fichier `Constant.java` (dans app > src > main > java > com > wetravel > Utils) :

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Ajoutez les noms des emplacements au fichier Constant.java](assets/constants.jpg)

### Explication du code de requête de prérécupération par lots

| Code | Description |
|--- |--- |
| `targetPrefetchContent()` | Fonction définie par l’utilisateur (ne faisant pas partie du SDK) qui utilise des méthodes [!DNL Target] pour récupérer et mettre en cache deux emplacements [!DNL Target]. |
| `prefetchContent()` | Méthode du SDK [!DNL Target] qui envoie la requête de prérécupération |
| `Constant.wetravel_engage_home` | Nom de l’emplacement [!DNL Target] prérécupéré qui affiche le contenu de son offre sur l’écran d’accueil |
| `Constant.wetravel_engage_search` | Nom de l’emplacement [!DNL Target] prérécupéré qui affichera le contenu de son offre dans l’écran Résultats de la recherche. Puisqu’il s’agit d’un second emplacement dans la prérécupération, cette requête de prérécupération est appelée &quot;requête de prérécupération par lots&quot;. |
| setUp() | Fonction définie par l’utilisateur qui effectue le rendu de l’écran d’accueil de l’application après la prérécupération des offres [!DNL Target]. |

### À propos de l’asynchrone ou du synchrone

Avec le code que nous venons de mettre en oeuvre, la requête de prérécupération est effectuée sous la forme d’un appel de blocage synchrone, juste avant le rendu de l’écran d’accueil. Lorsque nous avons collé le nouveau code dans le contrôleur HomeActivity, nous avons déplacé l’exécution de la fonction `setUp()` de la fonction `onResume()` jusqu’à après la requête Target. Cela peut s’avérer bénéfique dans les cas où vous souhaitez personnaliser le contenu à l’ouverture initiale de l’application, car cela garantit que le contenu personnalisé provenant des serveurs Target est renvoyé (ou expiré) avant le premier rendu de l’écran. Pour autoriser le chargement asynchrone des requêtes (en arrière-plan), appelez simplement `setUp()` dans la fonction `onCreate()` à la place.

### Validation de la requête de prérécupération par lots

Recréez l’application et ouvrez l’émulateur Android. (Les captures d’écran suivantes utilisent Pixel 2 sur Android Q version 9+, API niveau 29). La réponse de prérécupération doit se lire &quot;réponse de prérécupération reçue&quot; :

Lors du rendu de l’écran d’accueil, la requête de prérécupération doit être chargée. Avec Logcat, filtrez pour [!DNL "Target"] afin d’afficher la requête et la réponse :

![Validez les requêtes sur l’écran d’accueil](assets/prefetch_validation.jpg)

Si vous ne voyez pas de réponse réussie, vérifiez les paramètres du fichier `ADBMobileConfig.json` et la syntaxe du code dans le fichier HomeActivity.

Deux emplacements sont désormais mis en cache sur l’appareil. Les noms des emplacements seront bientôt chargés de manière différée dans l’interface [!DNL Target], où ils peuvent être sélectionnés dans divers menus déroulants lorsque vous les utilisez dans une activité.

### Ajout de requêtes de chargement pour chaque emplacement mis en cache

Maintenant que les emplacements sont prérécupérés et que leurs réponses sont mises en cache sur l’appareil, ajoutons la méthode `Target.loadRequest()` qui récupère le contenu de l’offre du cache afin que vous puissiez l’utiliser pour mettre à jour votre application. Nous allons ajouter une nouvelle méthode personnalisée appelée `engageMessage()` qui s’exécutera avec la requête de prérécupération. `engageMessage()` appellera `Target.loadRequest()`. `engageMessage()` s’exécute avant `setUp()` pour s’assurer que la requête de chargement est appelée avant la configuration de l’écran.

Tout d’abord, ajoutez l’appel `engageMessage()` et la méthode pour l’emplacement wetravel_engage_home dans HomeActivity :

![Ajouter la première requête de chargement](assets/wetravel_engage_home_loadRequest.jpg)

Voici le code mis à jour :

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
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

Ajoutez maintenant la méthode `engageMessage()` call &amp; pour l’emplacement wetravel_engage_search dans SearchBusActivity. Notez que l’appel `engageMessage()` est défini dans la méthode `onResume()` avant l’appel à `setUpSearch()`, il s’exécute donc avant la configuration de l’écran :

![Ajouter une seconde requête de chargement](assets/wetravel_engage_search_loadRequest.jpg)

Voici le code mis à jour :

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

Puisque vous venez d’ajouter des méthodes Target à SearchBusActivity, veillez à importer les classes [!DNL Target] :

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Ajout d’une requête en temps réel

La prochaine requête que nous allons ajouter à l’application sera une requête en temps réel sur l’écran de remerciement. Par &quot;temps réel&quot;, nous voulons dire que la requête sera faite et que la réponse sera appliquée immédiatement (et non mise en cache pour plus tard). Dans une leçon ultérieure, nous créerons une expérience à l’aide de cette requête, personnalisée en fonction de la destination de voyage de l’utilisateur.

Ajoutons donc une requête en temps réel sur l’écran de remerciement. Dans le fichier ThankYouActivity , les modifications affichées en rouge sont :
![Ajouter un emplacement en temps réel sur l’écran de remerciement](assets/thankyou.jpg)

Faites défiler l’écran jusqu’à la fin du fichier ThankYouActivity . Mettez en commentaire les trois lignes de la fonction `getRecommandations()` et ajoutez l’appel de la fonction `targetLoadRequest()` :

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Ajoutez cette ligne de code à la fonction `getRecommandations()` :

```java
targetLoadRequest(recommandation.recommandations);
```

Maintenant, nous devons définir la fonction `targetLoadRequest()` :
![ Ajout d’un emplacement en temps réel sur l’écran de remerciement](assets/thankyou2.jpg)

Ajoutez ce bloc de code après la fonction `filterRecommendationBasedOnOffer()` :

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}
```

Puisque vous venez d’ajouter des méthodes Target à l’activité de remerciement, veillez à importer les classes Target :

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest() Explication du code

| Code | Description |
|--- |--- |
| `targetLoadRequest()` | Fonction définie par l’utilisateur (ne faisant pas partie du SDK) qui déclenche `Target.loadRequest()` qui charge et affiche l’emplacement wetravel_context_dest |
| `Target.loadRequest()` | Méthode du SDK qui émet la requête au serveur Target |
| Constant.wetravel_context_dest | Nom de l’emplacement affecté à la requête que nous utiliserons ultérieurement lorsque nous créerons l’activité dans l’interface [!DNL Target]. |
| `filterRecommendationBasedOnOffer()` | Fonction définie par l’utilisateur dans l’application qui extrait l’offre de l’emplacement de la réponse Target et décide de la manière dont l’application doit changer en fonction du contenu de l’offre. |
| `recommandations.addAll()` | Fonction définie par l’utilisateur dans l’application qui s’exécutait par défaut lors du chargement de l’écran de remerciement, mais qui s’exécute maintenant après réception et analyse de la réponse Target par `filterRecommendationBasedOnOffer()`. |

Il s’agit d’une mise à jour plus sophistiquée que nous avons faite à l’application, puis avec la demande que nous avons ajoutée à l’écran d’accueil. Prenons quelques instants pour examiner ce que nous avons fait :

1. Nous avons interrompu le comportement précédent de l’application en affichant trois promotions par défaut, en commentant les lignes de code.
1. Nous avons demandé à l’application d’exécuter une nouvelle fonction, que nous avons appelée de manière arbitraire targetLoadRequest
1. Nous avons défini la fonction `targetLoadRequest` pour envoyer une requête à Target à l’aide de la méthode Target.loadRequest et exécuter immédiatement la fonction `filterRecommendationBasedOnOffer()` lorsque la réponse de l’offre [!DNL Target] est reçue.
1. La fonction `filterRecommendationBasedOnOffer()` interprète la réponse et décide quelles promotions doivent être appliquées à l’écran.

Il s’agit d’un modèle d’utilisation très courant lors de l’utilisation de [!DNL Target] dans des applications mobiles.  Il est à la fois très puissant, dans la mesure où vous pouvez personnaliser presque tous les aspects de votre application mobile. Cela nécessite également une coordination entre le code de l’application et les offres que nous définirons ultérieurement dans l’interface [!DNL Target]. En raison de cette coordination, certains cas d’utilisation de la personnalisation peuvent nécessiter que vous mettiez à jour votre application dans la boutique d’applications afin de lancer l’activité.

### Validation de la requête en temps réel

Ouvrez l’émulateur Android et suivez toutes les étapes pour réserver un voyage : Accueil > Résultats de recherche de bus > Sélection de siège, options de paiement (toute option de paiement avec des données vides fonctionnera).

Sur l’écran de remerciement final, regardez Logcat pour la réponse. La réponse doit se lire &quot;Le contenu par défaut a été renvoyé pour &quot;wetravel_context_dest&quot; :

![Ajouter un emplacement en temps réel sur l’écran de remerciement](assets/thankyou_validation.jpg)

## Effacement des emplacements prérécupérés du cache

Il peut arriver que des emplacements prérécupérés doivent être effacés au cours d’une session. Par exemple, lorsqu’une réservation se produit, il est logique d’effacer les emplacements mis en cache, car l’utilisateur est désormais &quot;engagé&quot; et comprend le processus de réservation. S’ils réservent un autre voyage au cours de leur session, ils n’auront pas besoin des emplacements d’origine sur l’écran d’accueil ni de l’écran des résultats de recherche pour guider leur réservation. Il serait plus logique d’effacer les emplacements du cache et de prérécupérer les nouvelles offres pour peut-être une deuxième réservation à rabais ou un autre scénario pertinent. La logique peut être ajoutée à l’écran d’accueil et à l’écran des résultats de recherche pour prérécupérer de nouveaux emplacements si une réservation a eu lieu au cours de la session.

Pour cet exemple, nous allons simplement effacer les emplacements prérécupérés de la session lorsqu’une réservation a lieu. Pour ce faire, appelez la fonction `Target.clearPrefetchCache()` . Définissez la fonction dans la fonction `targetLoadRequest()` comme illustré ci-dessous :

```java
Target.clearPrefetchCache()
```

![Effacer les emplacements prérécupérés du cache](assets/clearPrefetch.jpg)

Félicitations ! Votre application dispose désormais de la structure pour la personnalisation. Dans la leçon suivante, nous améliorerons nos capacités de personnalisation en ajoutant des paramètres à ces emplacements.

**[NEXT : &quot;Ajouter des paramètres&quot; >](add-parameters.md)**
