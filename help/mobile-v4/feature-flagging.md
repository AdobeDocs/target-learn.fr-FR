---
title: Indicateur de fonctionnalité
description: Adobe Target peut être utilisé pour tester des fonctionnalités d’expérience utilisateur telles que la couleur, la copie, les boutons, le texte et les images, et fournir ces fonctionnalités à des audiences spécifiques.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 034d13f2-63b1-44b0-b3dc-867efe37672f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# Indicateur de fonctionnalité

Les propriétaires d’applications mobiles ont besoin de davantage de flexibilité pour déployer de nouvelles fonctionnalités dans leur application sans avoir à investir dans plusieurs versions d’application. Ils peuvent également vouloir déployer les fonctionnalités progressivement jusqu’à un pourcentage de la base d’utilisateurs, afin de tester l’efficacité. Adobe Target peut être utilisé pour tester des fonctionnalités d’expérience utilisateur telles que la couleur, la copie, les boutons, le texte et les images, et fournir ces fonctionnalités à des audiences spécifiques.

Dans cette leçon, nous allons créer une offre d’« indicateur de fonctionnalité » qui peut être utilisée comme déclencheur pour activer des fonctionnalités d’application spécifiques.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Ajouter un nouvel emplacement à la requête de prérécupération par lots
* Créez une activité de [!DNL Target] avec une offre qui sera utilisée comme indicateur de fonctionnalité
* Charger et valider l’offre d’indicateur de fonctionnalité dans votre application

## Ajoutez un nouvel emplacement à la requête de prérécupération de l’activité d’accueil

Dans l’application de démonstration de nos leçons précédentes, nous allons ajouter un nouvel emplacement appelé « wetravel_feature_flag_recs » à la requête de prérécupération dans l’activité d’accueil et le charger à l’écran avec une nouvelle méthode Java.

>[!NOTE]
>
>L’un des avantages de l’utilisation d’une requête de prérécupération est que l’ajout d’une nouvelle requête n’ajoute pas de surcharge réseau supplémentaire ni ne cause de travail de charge supplémentaire, car la requête est incluse dans la requête de prérécupération

Tout d&#39;abord, vérifiez que la constante wetravel_feature_flag_recs est ajoutée dans le fichier Constant.java :

![Ajouter une constante d’indicateur de fonctionnalité](assets/feature_flag_constant.jpg)

Voici le code :

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Ajoutez maintenant l’emplacement à la requête de prérécupération et chargez une nouvelle fonction appelée `processFeatureFlags()` :

![Code d’indicateur de fonctionnalité](assets/feature_flag_code.jpg)

Voici le code mis à jour complet :

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();

    Map<String, Object> params1;
    params1 = new HashMap<String, Object>();
    params1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");

    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_feature_flag_recs, params1));

    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    engageMessage();
                    processFeatureFlags();
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}

public void processFeatureFlags() {
    Target.loadRequest(Constant.wetravel_feature_flag_recs, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Feature Flags : " + s);
                            if(s != null && !s.isEmpty()) {
                                //enable or disable features
                            }
                        }
                    });
                }
            });
}
```

### Valider la demande d’indicateur de fonctionnalité

Une fois le code ajouté, exécutez l’émulateur sur l’activité d’accueil et observez Logcat pour la réponse mise à jour :

![Valider l’emplacement de l’indicateur de fonctionnalité](assets/feature_flag_code_logcat.jpg)

## Créer une offre JSON d’indicateur de fonctionnalité

Nous allons maintenant créer une offre JSON simple qui agira comme indicateur ou déclencheur pour une audience spécifique : l’audience qui recevra le déploiement de la fonctionnalité dans son application. Dans l’interface [!DNL Target], créez une offre :

![Créer une offre JSON d’indicateur de fonctionnalité](assets/feature_flag_json_offer.jpg)

Appelons-le « Indicateur de fonctionnalité v1 » avec la valeur {« enable »:1}

![feature_flag_v1 Offre JSON](assets/feature_flag_json_name.jpg)

## Création d’une activité

Créons maintenant une activité de test A/B avec cette offre. Pour obtenir des instructions détaillées sur la création d’une activité, reportez-vous à la leçon précédente. L’activité n’aura besoin que d’une seule audience pour cet exemple. Dans un scénario en direct, vous pouvez créer des audiences personnalisées spécifiques pour des déploiements de fonctionnalités spécifiques, puis définir l’activité pour utiliser ces audiences. Dans cet exemple, nous allons simplement attribuer le trafic 50/50 (50 % aux visiteurs qui verraient les mises à jour des fonctionnalités et 50 % aux visiteurs qui verraient une expérience standard). Voici le paramétrage de l&#39;activité :

1. Nommez l’activité « Indicateur de fonctionnalité ».
1. Sélectionnez l’emplacement « wetravel_feature_flag_recs »
1. Modifiez le contenu en offre JSON « Indicateur de fonctionnalité v1 »

   ![Configuration de l’activité d’indicateur de fonctionnalité](assets/feature_flag_activity.jpg)

1. Cliquez sur **[!UICONTROL Add Experience]** pour ajouter l’expérience B.
1. Laissez l’emplacement « wetravel_feature_flag_recs »
1. Laisser **[!UICONTROL Default Content]** pour le contenu
1. Cliquez sur **[!UICONTROL Next]** pour accéder à l’écran [!UICONTROL Targeting]

   ![Configuration de l’activité d’indicateur de fonctionnalité](assets/feature_flag_activity_2.jpg)

1. Sur l’écran [!UICONTROL Targeting], vérifiez que la méthode [!UICONTROL Traffic Allocation] est définie sur le paramètre par défaut (Manuel) et que chaque expérience dispose de l’affectation de 50 % par défaut. Sélectionnez **[!UICONTROL Next]** pour passer à la **[!UICONTROL Goals & Settings]**.

   ![Configuration de l’activité d’indicateur de fonctionnalité](assets/feature_flag_activity_3.jpg)

1. Définissez la **[!UICONTROL Primary Goal]** sur **[!UICONTROL Conversion]**.
1. Définissez l’action sur **[!UICONTROL Viewed an Mbox]**. Nous utiliserons l’emplacement « wetravel_context_dest » (cet emplacement se trouvant sur l’écran de confirmation, nous pouvons l’utiliser pour voir si la nouvelle fonctionnalité entraîne plus de conversions).
1. Cliquez sur **[!UICONTROL Save & Close]**.

   ![Configuration de l’activité d’indicateur de fonctionnalité](assets/feature_flag_activity_4.jpg)

activer l’activité ;

## Validation de l’activité d’indicateur de fonctionnalité

Utilisez maintenant l’émulateur pour surveiller la requête. Puisque nous avons défini le ciblage sur 50 % des utilisateurs, vous verrez que la réponse de l’indicateur de fonctionnalité contient la valeur `{enable:1}`.

![Validation des indicateurs de fonctionnalité](assets/feature_flag_validation.jpg)

Si vous ne voyez pas la valeur `{enable:1}`, cela signifie que vous n’avez pas été ciblé pour l’expérience. À titre de test temporaire, pour forcer l’affichage de l’offre, vous pouvez :

1. Désactivez l’activité.
1. Définissez l’affectation du trafic sur 100 % sur la nouvelle expérience de fonctionnalité.
1. Enregistrez et réactivez.
1. Effacez les données sur votre émulateur, puis redémarrez l’application.
1. L’offre doit maintenant renvoyer la valeur `{enable:1}`.

Dans un scénario en direct, la réponse `{enable:1}` peut être utilisée pour activer une logique plus personnalisée dans votre application afin d’afficher le jeu de fonctionnalités spécifique que vous souhaitez afficher à votre audience cible.

## Conclusion

Beau travail ! Vous disposez désormais des compétences nécessaires pour déployer des fonctionnalités vers des audiences d’utilisateurs spécifiques.
