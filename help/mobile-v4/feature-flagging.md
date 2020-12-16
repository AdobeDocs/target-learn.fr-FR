---
title: Marquage des fonctionnalités
seo-title: Marquage des fonctionnalités
description: Adobe Target peut être utilisé pour expérimenter des fonctionnalités UX telles que la couleur, la copie, les boutons, le texte et les images et fournir ces fonctionnalités à des audiences spécifiques.
seo-description: Adobe Target peut être utilisé pour expérimenter des fonctionnalités UX telles que la couleur, la copie, les boutons, le texte et les images et fournir ces fonctionnalités à des audiences spécifiques.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: 199fbde58696a0511623c5500cc6afbbcfdd67a3
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---


# Marquage des fonctionnalités

Les propriétaires de produits d&#39;applications mobiles ont besoin de la flexibilité nécessaire pour déployer de nouvelles fonctionnalités dans leur application sans avoir à investir dans plusieurs versions d&#39;applications. Ils peuvent également souhaiter déployer progressivement des fonctionnalités sur un pourcentage de la base d’utilisateurs afin de tester l’efficacité. Adobe Target peut être utilisé pour expérimenter des fonctionnalités UX telles que la couleur, la copie, les boutons, le texte et les images et fournir ces fonctionnalités à des audiences spécifiques.

Dans cette leçon, nous allons créer une offre &quot;indicateur de fonction&quot; qui peut être utilisée comme déclencheur pour activer des fonctionnalités spécifiques de l&#39;application.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pourrez :

* Ajouter un nouvel emplacement à la demande de prérécupération par lot
* Créer une activité [!DNL Target] avec une offre qui sera utilisée comme indicateur de fonctionnalité
* Charger et valider l’offre d’indicateur de fonction dans votre application

## Ajouter un nouvel emplacement à la demande de prérécupération sur l&#39;Activité d&#39;accueil

Dans l&#39;application de démonstration de nos leçons précédentes, nous allons ajouter un nouvel emplacement appelé &quot;wetravel_feature_flag_recs&quot; à la demande de prérécupération dans l&#39;Activité d&#39;accueil et la charger à l&#39;écran avec une nouvelle méthode Java.

>[!NOTE]
>
>L&#39;un des avantages de l&#39;utilisation d&#39;une requête de prérécupération est que l&#39;ajout d&#39;une nouvelle requête n&#39;ajoute pas de surcharge réseau supplémentaire ou ne provoque pas de charge supplémentaire puisque la requête est incluse dans la requête de prérécupération.

Tout d’abord, vérifiez que la constante wetravel_feature_flag_recs est ajoutée dans le fichier Constant.java :

![Constante d&#39;indicateur de fonction d&#39;Ajoute](assets/feature_flag_constant.jpg)

Voici le code :

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Ajoutez maintenant l’emplacement à la requête de prérécupération et chargez une nouvelle fonction appelée `processFeatureFlags()` :

![Code d’indicateur de fonction](assets/feature_flag_code.jpg)

Voici le code complet mis à jour :

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

### Valider la demande d&#39;indicateur de fonction

Une fois le code ajouté, exécutez l’émulateur sur l’Activité d’accueil et regardez Logcat pour obtenir la réponse mise à jour :

![Valider l’emplacement de l’indicateur de fonction](assets/feature_flag_code_logcat.jpg)

## Création d’une Offre JSON d’indicateur de fonction

Nous allons maintenant créer une simple offre JSON qui servira d&#39;indicateur ou de déclencheur pour une audience spécifique - l&#39;audience qui recevra le déploiement de la fonctionnalité dans son application. Dans l&#39;interface [!DNL Target], créez une offre :

![Créer une Offre JSON d’indicateur de fonction](assets/feature_flag_json_offer.jpg)

Nommons-le &quot;Feature Flag v1&quot; avec la valeur {&quot;enable&quot;:1}

![offre JSON feature_flag_v1](assets/feature_flag_json_name.jpg)

## Création d’une activité

Maintenant, créons une activité de test A/B avec cette offre. Pour obtenir des instructions détaillées sur la création d’une activité, reportez-vous à la leçon précédente. L&#39;activité n&#39;aura besoin que d&#39;une seule audience pour cet exemple. Dans un scénario dynamique, vous pouvez créer des audiences personnalisées spécifiques pour des déploiements de fonctionnalités spécifiques, puis définir l’activité pour utiliser ces audiences. Dans cet exemple, nous affecterons le trafic 50/50 (50 % aux visiteurs qui verraient les mises à jour des fonctionnalités et 50 % aux visiteurs qui verraient une expérience standard). Voici la configuration de l’activité :

1. Attribuez un nom à l’Activité &quot;Indicateur de fonction&quot;.
1. Sélectionnez l’emplacement &quot;wetravel_feature_flag_recs&quot;.
1. Remplacez le contenu par l’offre JSON &quot;Feature Flag v1&quot; (Indicateur de fonction v1).

   ![Configuration de l&#39;Activité d&#39;indicateur de fonction](assets/feature_flag_activity.jpg)

1. Cliquez sur **[!UICONTROL Ajouter l’expérience]** pour ajouter l’expérience B.
1. Laissez l’emplacement &quot;wetravel_feature_flag_recs&quot;
1. Conserver **[!UICONTROL Contenu par défaut]** pour le contenu
1. Cliquez sur **[!UICONTROL Suivant]** pour accéder à l’écran [!UICONTROL Ciblage].

   ![Configuration de l&#39;Activité d&#39;indicateur de fonction](assets/feature_flag_activity_2.jpg)

1. Dans l’écran [!UICONTROL Ciblage], vérifiez que la méthode [!UICONTROL Affectation du trafic] est définie sur le paramètre par défaut (Manuel) et que chaque expérience possède l’affectation par défaut de 50 %. Sélectionnez **[!UICONTROL Suivant]** pour passer à **[!UICONTROL Objectifs et paramètres]**.

   ![Configuration de l&#39;Activité d&#39;indicateur de fonction](assets/feature_flag_activity_3.jpg)

1. Définissez **[!UICONTROL Objectif Principal]** sur **[!UICONTROL Conversion]**.
1. Définissez l’action sur **[!UICONTROL Affichage d’une mbox]**. Nous utiliserons l&#39;emplacement &quot;wetravel_context_dest&quot; (puisque cet emplacement se trouve sur l&#39;écran de confirmation, nous pouvons l&#39;utiliser pour voir si la nouvelle fonctionnalité conduit à plus de conversions).
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   ![Configuration de l&#39;Activité d&#39;indicateur de fonction](assets/feature_flag_activity_4.jpg)

activer l’activité ;

## Valider l&#39;Activité d&#39;indicateur de fonction

Utilisez maintenant l’émulateur pour surveiller la demande. Puisque le ciblage est défini sur 50 % des utilisateurs, la réponse de l’indicateur de fonction contient la valeur `{enable:1}`.

![Validation des indicateurs de fonction](assets/feature_flag_validation.jpg)

Si vous ne voyez pas la valeur `{enable:1}`, cela signifie que vous n’avez pas été ciblé pour l’expérience. En tant que test temporaire, pour forcer l’offre à s’afficher, vous pouvez :

1. Désactivez l’activité.
1. Modifiez l’affectation du trafic à 100 % sur la nouvelle expérience de fonctionnalité.
1. Enregistrez et réactivez.
1. Essuyez les données de votre émulateur, puis redémarrez l’application.
1. L’offre doit maintenant renvoyer la valeur `{enable:1}`.

Dans un scénario en direct, la réponse `{enable:1}` peut être utilisée pour activer une logique plus personnalisée dans votre application afin d’afficher le jeu de fonctionnalités spécifique à afficher pour votre audience de cible.

## Conclusion

Bon travail ! Vous disposez désormais des compétences nécessaires pour déployer des fonctionnalités vers des audiences utilisateur spécifiques.
