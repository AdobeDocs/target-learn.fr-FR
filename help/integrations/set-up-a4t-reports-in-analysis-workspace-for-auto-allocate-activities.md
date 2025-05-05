---
title: Configuration des rapports A4T dans  [!DNL Analysis Workspace]  pour les activités [!UICONTROL Auto-Allocate]
description: Comment configurer des rapports [!UICONTROL Analytics for Target] (A4T) dans  [!DNL Adobe] [!DNL Analysis Workspace] lors de l’exécution d’activités [!UICONTROL Auto-Allocate].
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 190a67832f378e15090115420bfaf8a4af4b9cb9
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 0%

---

# Configuration de rapports A4T dans [!DNL Analysis Workspace] pour les activités [!DNL Auto-Allocate]

Une [[!UICONTROL Auto-Allocate] activité ](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=fr){target=_blank} dans [!DNL Adobe Target] identifie un gagnant parmi plusieurs expériences et réaffecte automatiquement le trafic du visiteur vers le gagnant pendant que le test se poursuit et apprend. L&#39;intégration [!UICONTROL Analytics for Target] (A4T) pour [!UICONTROL Auto-Allocate] vous permet d&#39;afficher les données de création de rapports dans [!DNL Adobe Analytics] et vous pouvez optimiser les événements personnalisés ou les mesures définies dans [!DNL Analytics].

Bien que de riches fonctionnalités d&#39;analyse soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace], quelques modifications du panneau par défaut [!UICONTROL Analytics for Target] peuvent être nécessaires pour interpréter correctement les activités [!UICONTROL Auto-Allocate]. Ces modifications sont nécessaires en raison des nuances des [critères de mesure d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=fr#supported){target=_blank}.

Chaque type de mesure d’optimisation nécessite une configuration de rapport différente dans A4T, comme suit :

* Utilisation d’une mesure [!DNL Analytics]

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* Utilisation d’une mesure de conversion définie par [!DNL Target]

Ce tutoriel couvre les instructions générales d’A4T et les étapes de configuration de rapports spécifiques aux critères.

## Mesures Analytics avec critères d’optimisation &quot;[!UICONTROL Maximize Metric Value Per Visitor]&quot;

**Définition** : (valeur de mesure globale) / ( nombre de visiteurs)

Pour configurer le rapport, apportez les modifications suivantes au rapport A4T :

| Modifications requises | Rapport déclenché par [!DNL Target] | Rapport Panneau A4T |
| --- | --- | --- |
| Maximiser la valeur de mesure pour une mesure [!DNL Analytics] | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimer [!UICONTROL Lift (Low)] et [!UICONTROL Lift (High)]. Conserver [!UICONTROL Lift (Med)].</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li><li>Renommez la mesure de taux [!UICONTROL Conversion] en &quot;Mesure / Visiteur&quot;.</li></ul> | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez [!UICONTROL Lift (Low)] et [!UICONTROL Lift (High)] Conserver [!UICONTROL Lift (Med)].</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li><li>Renommez la mesure de taux [!UICONTROL Conversion] en &quot;Mesure / Visiteur&quot;.</li><li>Assurez-vous que les plages de dates et d’heures correspondent aux valeurs affichées dans le rapport [!DNL Target]. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li></ul> |

![Maximiser la valeur de mesure pour les recettes](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] mesures avec critères d’optimisation &quot;[!UICONTROL Unique Visitor Conversion Rate]&quot;

**Définition** : ( nombre de visiteurs uniques avec une valeur positive de la mesure) / (nombre total de visiteurs uniques)

Exemple : supposons que votre mesure d’optimisation soit [!UICONTROL Revenue]. L’activité comporte cinq visiteurs uniques et trois d’entre eux effectuent un achat. Dans cet exemple, cette valeur = (3 visiteurs pour lesquels [!UICONTROL Revenue] est positif) / (5 visiteurs uniques au total) = 0,6 = 60 %.

>[!NOTE]
>
>Le taux de conversion comme référencé ici peut faire référence à des actions en dehors des commandes, telles que des clics, des impressions, etc. Dans ce cas, le critère maximise toujours le nombre de visiteurs qui cliquent ou affichent la page, respectivement.

Pour configurer le rapport, apportez les modifications suivantes au rapport A4T :

| Modifications requises | Rapport déclenché par Target | Rapport Panneau A4T |
| --- | --- | --- |
| Maximiser les conversions pour une mesure [!DNL Analytics] | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez les trois mesures [!UICONTROL Lift] .</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li></ul> | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimez les trois mesures [!UICONTROL Lift] .</li><li>Créez un segment pour filtrer les visiteurs avec une valeur de mesure positive qui a consulté l’activité analysée. Voir [Création d’un segment](#segment) ci-dessous.</li><li>Remplacez la mesure [!UICONTROL Conversion Rate] auto-renseignée de sorte qu’il s’agisse de la division entre [!UICONTROL Unique visitors] avec une valeur de mesure positive et les visiteurs uniques. Voir [Mise à jour de la mesure Taux de conversion](#update-conversion-metric) ci-dessous.</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li><li>Assurez-vous que les plages de dates et d’heures correspondent aux valeurs affichées dans le rapport [!DNL Target]. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li></ul> |

### Rapport Panneau A4T par défaut - Conseils supplémentaires

Les sections suivantes contiennent des informations supplémentaires sur les conseils supplémentaires à suivre lors de la configuration du rapport Panneau A4T par défaut.

#### Création d’un segment {#segment}

1. Cliquez sur le signe **&quot;+&quot;** en regard de **[!UICONTROL Segments]** dans le rail de gauche.

   ![Signe plus en regard des segments dans le rail de gauche.](/help/integrations/assets/plus-sign.png)

1. Titre du segment &quot;Visiteurs avec une valeur de mesure positive&quot;.
1. Sous **[!UICONTROL Definition]**, en regard de **[!UICONTROL Include]**, sélectionnez **[!UICONTROL Visitor]**.
1. Sous **[!UICONTROL Definition]**, sélectionnez la mesure d’optimisation dans votre activité.

   Dans cet exemple, supposons que [!UICONTROL Revenue] soit la mesure d’optimisation.

1. Sélectionnez l’opérateur &quot;[!UICONTROL is greater than]&quot;, puis spécifiez &quot;0&quot;.

   Ces paramètres filtrent tous les visiteurs avec une valeur de mesure positive.

1. Cliquez sur **[!UICONTROL Save]**.

   ![Valeur de mesure positive](/help/integrations/assets/positive-metric-value.png)

1. Ajoutez le segment nouvellement créé nommé &quot;Visiteurs avec une valeur de mesure positive&quot; au panneau A4T.
1. Faites glisser et déposez la mesure [!UICONTROL Unique Visitors] dans la même colonne que &quot;Visiteurs avec une valeur de mesure positive&quot;.

   Cette configuration crée un segment de tous les visiteurs uniques pour lesquels la valeur de mesure est positive. Dans cet exemple, tous les visiteurs uniques dont les recettes sont supérieures à zéro.

#### Mise à jour de la mesure [!UICONTROL Conversion Rate] {#update-conversion-metric}

1. Si vous ne l’avez pas déjà fait, supprimez la colonne [!UICONTROL Conversion Rate] existante du panneau, comme expliqué ci-dessous.
1. Ajoutez une mesure en cliquant sur le signe &quot;+&quot; en regard de la section **[!UICONTROL Metrics]** dans le rail de gauche.
1. Nommez la mesure &quot;Taux de conversion&quot; et définissez-la comme &quot;([!UICONTROL Unique Visitors] avec une valeur de mesure positive)&quot; divisée par &quot;Visiteurs uniques&quot;, comme illustré ci-dessous.

   Ajoutez le segment nouvellement créé (étapes définies ci-dessous) de &quot;Visiteurs avec une valeur de mesure positive&quot;, l’opérateur de division, la mesure &quot;Visiteurs uniques&quot; dans le numérateur et &quot;Visiteurs uniques&quot; comme dénominateur.

   ![Taux de conversion dans le panneau A4T.](/help/integrations/assets/conversion-rate.png)

1. Cliquez sur **[!UICONTROL Save]**.

1. Placez la mesure &quot;Taux de conversion&quot; que vous venez de créer dans le panneau existant.
1. Cliquez sur l’icône d’engrenage, puis désélectionnez la case à cocher **[!UICONTROL Percent]**, car cette valeur peut prêter à confusion.

   La configuration correcte du rapport doit générer un résultat qui ressemble à l’illustration suivante :

   ![Taux de conversion des visites uniques dans le rapport Panneau A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## Taux de conversion défini par [!DNL Target]

Pour configurer le rapport, apportez les modifications suivantes au rapport A4T :

| Modifications requises | Rapport déclenché par Target | Rapport Panneau A4T |
| --- | --- | --- |
| Création de rapports [!DNL Analytics] avec la mesure de conversion [!DNL Target] | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimer [!UICONTROL Lift (Low)] et [!UICONTROL Lift (High)]. Conserver l’effet élévateur (Med).</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li></ul> | <ul><li>Supprimez les mesures [!UICONTROL Confidence].</li><li>Supprimer [!UICONTROL Lift (Low)] et [!UICONTROL Lift (High)]. Conserver [!UICONTROL Lift (Med)].</li><li>Décochez la présentation en pourcentage de la colonne [!UICONTROL Conversion Rate] pour éviter toute confusion. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li><li>Assurez-vous que les plages de dates et d’heures correspondent aux valeurs affichées dans le rapport [!DNL Target]. Voir [Directives générales pour A4T](#guidance) ci-dessous.</li></ul> |

La configuration correcte du rapport doit générer un résultat qui ressemble à l’illustration suivante :

![Conversions des activités](/help/integrations/assets/optimized-table.png)

## Conseils généraux pour A4T {#guidance}

Vous pouvez accéder à un panneau [!UICONTROL Analytics for Target] prédéfini en cliquant sur le lien à partir de l’écran du rapport dans [!UICONTROL Target] (ce que l’on désigne plus loin dans ce guide sous le nom de &quot;[!DNL Target] rapport déclenché&quot;). Vous pouvez également créer le panneau A4T dans [!DNL Analytics] (détails plus loin dans cette section).

Les sections suivantes indiquent les configurations requises, selon l’une de ces méthodes. Toutefois, les étapes suivantes constituent des conseils généraux pour A4T :

* Supprimez les mesures de confiance du panneau A4T, quelle que soit la méthode de création du panneau (les deux sont présentées ci-dessous). À la place, référencez ces valeurs dans les rapports [!DNL Target]. En outre, les gagnants d’activité peuvent être identifiés dans les rapports [!DNL Target]. Vous trouverez des informations détaillées sur l’identification des gagnants d’activité dans la section [Identification de l’gagnant de l’activité](#winner) ci-dessous.
&#x200B;>>
* Pour éviter toute confusion, désélectionnez la présentation &quot;[!UICONTROL Percent]&quot; de la mesure [!UICONTROL Conversion Rate]. Voir [Masquer le pourcentage de la colonne [!UICONTROL Conversion Rate]](#hide-percentage) ci-dessous.
&#x200B;>>
* Si vous créez un panneau A4T, assurez-vous que les plages de dates et d’heures correspondent à celles de votre rapport [!DNL Target]. Voir [Aligner la date et l’heure dans le panneau A4T](#aligning-date-and-time) ci-dessous.

### Masquer le pourcentage de la colonne [!UICONTROL Conversion Rate] {#hide-percentage}

1. Cliquez sur l’icône **engrenage** en regard du titre de la colonne [!UICONTROL Conversion Rate].

   ![Icône d’engrenage dans la colonne Taux de conversion](/help/integrations/assets/coversion-rate-gear-icon.png)

   La boîte de dialogue de paramètres [!UICONTROL Column] s’affiche :

   ![Boîte de dialogue Paramètres de colonne](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Décochez la case **[!UICONTROL Percent]** .

   Votre panneau A4T n’inclut désormais pas les pourcentages comme [!UICONTROL Conversion Rate] et correspond à [!DNL Target], comme illustré ci-dessous :

   ![Colonne Taux de conversion n’affichant aucun pourcentage](/help/integrations/assets/no-percentages.png)

### Alignement de la date et de l’heure dans le panneau A4T {#aligning-date-and-time}

1. Sous chaque panneau, vérifiez la période référencée par le panneau pour vous assurer que la période correspond à celle du rapport [!DNL Target].

   ![Période dans le panneau A4T](/help/integrations/assets/date-range.png)

1. Dans [!DNL Analytics], définissez la plage horaire sur 12h00 - 23h59.

### Identification de l’activité gagnante {#winner}

Les gagnants de l’activité [!DNL Auto-Allocate] sont sélectionnés en cas de taux de conversion gagnant avec des valeurs de confiance supérieures ou égales à 95 %. Ces valeurs doivent être référencées dans les rapports [!DNL Target], car les calculs de confiance reflètent les méthodes plus conservatrices recommandées par [!DNL Target] pour les activités [!UICONTROL Auto-Allocate]. Voir [Garanties statistiques de l’affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html?lang=fr#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} dans *[!UICONTROL Adobe Target Business Practitioner Guide]*.

>[!NOTE]
>
>Les badges &quot;Pas encore de gagnant&quot; et &quot;Gagnant&quot; ne sont pas disponibles dans le panneau A4T dans [!DNL Analysis Workspace]. En outre, le badge &quot;étoile&quot; gagnante affiché dans les rapports [!DNL Target] pour les activités [!UICONTROL Auto-Allocate] doit être ignoré. Voir [Affectation automatique](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=fr#aa){target=_blank} dans la *Prise en charge d’A4T pour les activités d’affectation automatique et de ciblage automatique* dans le *[!UICONTROL Adobe Target Business Practitioner Guide]*.

### Créez le panneau A4T pour [!UICONTROL Auto-Allocate] dans [!DNL Analysis Workspace]

1. Pour créer un panneau A4T pour un rapport d’activité [!UICONTROL Auto-Allocate], commencez par le panneau [!UICONTROL Analytics for Target] dans [!DNL Analysis Workspace], comme illustré ci-dessous.

   ![Analytics for Target - Rapport d’affectation automatique](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Effectuez les sélections suivantes :

   * **[!UICONTROL Control Experience]** : choisissez n’importe quelle expérience.
   * **[!UICONTROL Normalizing Metric]** : sélectionnez **[!UICONTROL Visitors]** (inclus par défaut dans le panneau A4T). [!UICONTROL Auto-Allocate] normalise toujours les taux de conversion par visiteurs uniques.
   * **Mesures de succès** : sélectionnez la même mesure (optimisation) que celle utilisée lors de la création de l’activité. S’il s’agissait d’une mesure de conversion définie par [!DNL Target], sélectionnez **[!UICONTROL Activity Conversion]**. Sinon, sélectionnez la mesure [!DNL Adobe Analytics] que vous avez utilisée.









