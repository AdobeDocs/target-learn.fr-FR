---
title: Comment configurer des rapports A4T dans  [!DNL Analysis Workspace]  pour les activités [!UICONTROL Auto-Allocate]
description: Comment configurer les rapports [!UICONTROL Analytics for Target] (A4T) dans  [!DNL Adobe] [!DNL Analysis Workspace] lors de l’exécution d’activités [!UICONTROL Auto-Allocate].
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 190a67832f378e15090115420bfaf8a4af4b9cb9
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%

---

# Configurer des rapports A4T dans [!DNL Analysis Workspace] pour les activités [!DNL Auto-Allocate]

Une activité [[!UICONTROL Auto-Allocate] ](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html){target=_blank} dans [!DNL Adobe Target] identifie un gagnant parmi plusieurs expériences et réaffecte automatiquement le trafic des visiteurs au gagnant pendant que le test continue à s’exécuter et à apprendre. L’intégration [!UICONTROL Analytics for Target] (A4T) d’[!UICONTROL Auto-Allocate] vous permet d’afficher les données de rapports dans [!DNL Adobe Analytics] et d’optimiser les événements ou mesures personnalisés définis dans [!DNL Analytics].

Bien que des fonctionnalités d’analyse riches soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace], quelques modifications apportées au panneau de [!UICONTROL Analytics for Target] par défaut peuvent être nécessaires pour interpréter correctement les activités [!UICONTROL Auto-Allocate]. Ces modifications sont nécessaires en raison des nuances dans les [critères de mesure d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Chaque type de mesure d’optimisation nécessite une configuration de rapport différente dans A4T, comme suit :

* Utilisation d’une mesure [!DNL Analytics]

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* Utilisation d’une mesure de conversion définie par [!DNL Target]

Ce tutoriel présente les conseils généraux d’A4T et les étapes de configuration des rapports spécifiques à des critères.

## Mesures Analytics avec critères d’optimisation [!UICONTROL Maximize Metric Value Per Visitor]

**Définition** : (valeur de mesure globale) / (nombre de visiteurs)

Pour configurer le rapport, effectuez les modifications suivantes dans le rapport A4T :

| Modifications requises | rapport déclenché par [!DNL Target] | Rapport Panneau A4T |
| --- | --- | --- |
| Maximiser la valeur d’une mesure [!DNL Analytics] | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez les [!UICONTROL Lift (Low)] et les [!UICONTROL Lift (High)]. Reste [!UICONTROL Lift (Med)].</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li><li>Renommez la mesure Taux d’[!UICONTROL Conversion] en « Mesure / Visiteur ».</li></ul> | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez [!UICONTROL Lift (Low)] et [!UICONTROL Lift (High)] Conserver [!UICONTROL Lift (Med)].</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li><li>Renommez la mesure Taux d’[!UICONTROL Conversion] en « Mesure / Visiteur ».</li><li>Assurez-vous que les périodes et les heures correspondent aux valeurs affichées dans le rapport [!DNL Target]. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li></ul> |

![Maximiser la valeur de la mesure pour le chiffre d’affaires](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] des mesures avec des critères d’optimisation « [!UICONTROL Unique Visitor Conversion Rate] »

**Définition** : (nombre de visiteurs uniques avec une valeur positive de la mesure) / (nombre total de visiteurs uniques)

Exemple : supposons que la mesure d’optimisation soit [!UICONTROL Revenue]. L’activité comporte cinq visiteurs uniques, dont trois effectuent un achat. Dans cet exemple, cette valeur = (3 visiteurs pour lesquels [!UICONTROL Revenue] est positif) / (5 visiteurs uniques au total) = 0,6 = 60 %.

>[!NOTE]
>
>Le taux de conversion tel que référencé ici peut faire référence à des actions en dehors des commandes, telles que des clics, des impressions, etc. Dans ces cas, le critère consiste toujours à maximiser le nombre de visiteurs qui cliquent ou consultent la page, respectivement.

Pour configurer le rapport, effectuez les modifications suivantes dans le rapport A4T :

| Modifications requises | Rapport déclenché par Target | Rapport Panneau A4T |
| --- | --- | --- |
| Maximiser les conversions pour une mesure [!DNL Analytics] | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez les trois mesures [!UICONTROL Lift].</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li></ul> | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez les trois mesures [!UICONTROL Lift].</li><li>Créez un segment pour filtrer les visiteurs avec une valeur de mesure positive qui ont consulté l’activité analysée. Voir [Création d’un segment](#segment) ci-dessous.</li><li>Remplacez la mesure de [!UICONTROL Conversion Rate] automatiquement renseignée afin qu’indique la division entre les [!UICONTROL Unique visitors] avec une valeur de mesure positive et les visiteurs uniques. Voir [Mettre à jour la mesure Taux de conversion](#update-conversion-metric) ci-dessous.</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li><li>Assurez-vous que les périodes et les heures correspondent aux valeurs affichées dans le rapport [!DNL Target]. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li></ul> |

### Rapport par défaut du panneau A4T - conseils supplémentaires

Les sections suivantes contiennent des informations supplémentaires sur les conseils relatifs à la configuration de votre rapport par défaut du panneau A4T.

#### Création d’un segment {#segment}

1. Cliquez sur le signe **»+ »** en regard de **[!UICONTROL Segments]** dans le rail de gauche.

   ![Signe plus en regard de segments dans le rail de gauche.](/help/integrations/assets/plus-sign.png)

1. Nommez le segment « Visiteurs avec une valeur de mesure positive ».
1. Sous **[!UICONTROL Definition]**, en regard de **[!UICONTROL Include]**, sélectionnez **[!UICONTROL Visitor]**.
1. Sous **[!UICONTROL Definition]**, sélectionnez la mesure d’optimisation dans votre activité.

   Dans cet exemple, supposons que [!UICONTROL Revenue] soit la mesure d’optimisation.

1. Sélectionnez l’opérateur « [!UICONTROL is greater than] », puis spécifiez « 0 ».

   Ces paramètres filtrent pour tous les visiteurs avec une valeur de mesure positive.

1. Cliquez sur **[!UICONTROL Save]**.

   ![Valeur de mesure positive](/help/integrations/assets/positive-metric-value.png)

1. Ajoutez le segment nouvellement créé nommé « Visiteurs avec une valeur de mesure positive » au panneau A4T.
1. Faites glisser et déposez la mesure [!UICONTROL Unique Visitors] dans la même colonne que la mesure « Visiteurs avec une valeur de mesure positive ».

   Cette configuration crée un segment de tous les visiteurs uniques pour lesquels la valeur de la mesure est positive. Dans cet exemple, tous les visiteurs uniques dont le chiffre d’affaires était supérieur à zéro.

#### Mise à jour de la mesure [!UICONTROL Conversion Rate] {#update-conversion-metric}

1. Si vous ne l’avez pas déjà fait, supprimez la colonne [!UICONTROL Conversion Rate] existante du panneau, comme expliqué ci-dessous.
1. Ajoutez une mesure en cliquant sur le signe « + » en regard de la section **[!UICONTROL Metrics]** dans le rail de gauche.
1. Nommez la mesure « Taux de conversion » et définissez-la comme « ([!UICONTROL Unique Visitors] avec une valeur de mesure positive) » divisée par « Visiteurs uniques », comme illustré ci-dessous.

   Ajoutez le segment nouvellement créé (étapes définies ci-dessous) « Visiteurs avec une valeur de mesure positive », l’opérateur de division, la mesure « Visiteurs uniques » dans le numérateur et « Visiteurs uniques » comme dénominateur.

   ![Taux de conversion dans le panneau A4T.](/help/integrations/assets/conversion-rate.png)

1. Cliquez sur **[!UICONTROL Save]**.

1. Faites glisser et déposez votre nouvelle mesure « Taux de conversion » dans votre panneau existant.
1. Cliquez sur l’icône en forme d’engrenage, puis désélectionnez la case **[!UICONTROL Percent]**, car cette valeur peut prêter à confusion.

   La configuration correcte du rapport doit générer un résultat qui ressemble à l’illustration suivante :

   ![Taux de conversion des visites uniques dans le rapport du panneau A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## taux de conversion défini par l’[!DNL Target]

Pour configurer le rapport, effectuez les modifications suivantes dans le rapport A4T :

| Modifications requises | Rapport déclenché par Target | Rapport Panneau A4T |
| --- | --- | --- |
| [!DNL Analytics] de rapports avec [!DNL Target] mesure de conversion | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez les [!UICONTROL Lift (Low)] et les [!UICONTROL Lift (High)]. Maintenir l&#39;ascenseur (Med).</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li></ul> | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez les [!UICONTROL Lift (Low)] et les [!UICONTROL Lift (High)]. Reste [!UICONTROL Lift (Med)].</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li><li>Assurez-vous que les périodes et les heures correspondent aux valeurs affichées dans le rapport [!DNL Target]. Voir [Conseils généraux pour A4T](#guidance) ci-dessous.</li></ul> |

La configuration correcte du rapport doit générer un résultat qui ressemble à l’illustration suivante :

![Conversions d’activité](/help/integrations/assets/optimized-table.png)

## Conseils généraux pour A4T {#guidance}

Vous pouvez accéder à un panneau de [!UICONTROL Analytics for Target] préconfiguré en cliquant sur le lien de l’écran de rapport dans [!UICONTROL Target] (ce panneau est appelé « rapport déclenché par le [!DNL Target] » plus loin dans ce guide). Vous pouvez également créer le panneau A4T dans [!DNL Analytics] (les détails sont présentés plus loin dans cette section).

Les sections suivantes indiquent les configurations requises, en fonction de la méthode choisie. Toutefois, les étapes suivantes servent de guide général pour A4T :

* Supprimez les mesures de confiance du panneau A4T, quelle que soit la méthode de création du panneau (les deux sont détaillés ci-dessous). Au lieu de cela, référencez ces valeurs dans les rapports [!DNL Target]. De plus, les gagnants des activités peuvent être identifiés dans les rapports [!DNL Target]. Vous trouverez des détails sur l’identification de l’activité gagnante dans la section [Identifier l’activité gagnante](#winner) ci-dessous.
>>
* Pour éviter toute confusion, désélectionnez la présentation « [!UICONTROL Percent] » de la mesure [!UICONTROL Conversion Rate]. Voir [Masquer le pourcentage de la colonne [!UICONTROL Conversion Rate]](#hide-percentage) ci-dessous.
>>
* Si vous créez un panneau A4T, assurez-vous que les périodes et les heures correspondent à celles de votre rapport [!DNL Target]. Voir [Aligner la date et l’heure dans le panneau A4T](#aligning-date-and-time) ci-dessous.

### Masquer le pourcentage dans la colonne [!UICONTROL Conversion Rate] {#hide-percentage}

1. Cliquez sur l’icône **engrenage** en regard du titre de la colonne [!UICONTROL Conversion Rate].

   ![ Icône d’engrenage dans la colonne Taux de conversion ](/help/integrations/assets/coversion-rate-gear-icon.png)

   La boîte de dialogue [!UICONTROL Column] les paramètres s’affiche :

   ![Boîte de dialogue Paramètres des colonnes](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Décochez la case **[!UICONTROL Percent]** .

   Votre panneau A4T n’inclut désormais pas de pourcentages comme [!UICONTROL Conversion Rate] de [!DNL Target] et de correspondances, comme illustré ci-dessous :

   ![Colonne Taux de conversion n’affichant aucun pourcentage](/help/integrations/assets/no-percentages.png)

### Aligner la date et l’heure dans le panneau A4T {#aligning-date-and-time}

1. Sous chaque panneau, vérifiez la période référencée par le panneau pour vous assurer que la période correspond à celle du rapport [!DNL Target].

   ![Période dans le panneau A4T](/help/integrations/assets/date-range.png)

1. Dans [!DNL Analytics], définissez la plage temporelle sur 12 :00am 11 :59pm.

### Identifier le gagnant de l’activité {#winner}

Les [!DNL Auto-Allocate] gagnants de l’activité sont sélectionnés en cas de taux de conversion gagnant avec des valeurs de confiance supérieures ou égales à 95 %. Ces valeurs doivent être référencées dans les rapports de [!DNL Target], car les calculs de confiance reflètent les méthodes plus conservatrices que [!DNL Target] recommande pour les activités de [!UICONTROL Auto-Allocate]. Voir [Garanties statistiques de l’affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} dans la *[!UICONTROL Adobe Target Business Practitioner Guide]*.

>[!NOTE]
>
>Les badges « Pas encore de gagnant » et « Gagnant » ne sont pas disponibles dans le panneau A4T d’[!DNL Analysis Workspace]. En outre, le badge « étoile » gagnant affiché dans les rapports [!DNL Target] pour les activités [!UICONTROL Auto-Allocate] doit être ignoré. Consultez [ Affectation automatique ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} dans la section Prise en charge d’*A4T pour les activités d’affectation automatique et de ciblage automatique* dans la *[!UICONTROL Adobe Target Business Practitioner Guide]*.

### Créer A4T pour [!UICONTROL Auto-Allocate] panneau dans [!DNL Analysis Workspace]

1. Pour créer un panneau A4T pour un rapport d’activité [!UICONTROL Auto-Allocate], commencez par le panneau [!UICONTROL Analytics for Target] dans [!DNL Analysis Workspace], comme illustré ci-dessous.

   ![Rapport Analytics for Target - Affectation automatique](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Effectuez les sélections suivantes :

   * **[!UICONTROL Control Experience]** : choisissez n’importe quelle expérience.
   * **[!UICONTROL Normalizing Metric]** : sélectionnez **[!UICONTROL Visitors]** (inclus par défaut dans le panneau A4T). [!UICONTROL Auto-Allocate] normalise toujours les taux de conversion par visiteurs et visiteuses uniques.
   * **Mesures de succès** : sélectionnez la même mesure (d’optimisation) que celle utilisée lors de la création de l’activité. S’il s’agissait d’une mesure de conversion définie par [!DNL Target], sélectionnez **[!UICONTROL Activity Conversion]**. Sinon, sélectionnez la mesure [!DNL Adobe Analytics] que vous avez utilisée.









