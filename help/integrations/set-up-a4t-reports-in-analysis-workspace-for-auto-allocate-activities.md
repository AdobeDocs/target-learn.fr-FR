---
title: Configuration des rapports A4T dans [!DNL Analysis Workspace] pour [!UICONTROL Affectation automatique] Activités
description: Comment configurer [!UICONTROL Analytics pour Target] (A4T) dans [!DNL Adobe] [!DNL Analysis Workspace] en cours d’exécution [!UICONTROL Affectation automatique] activités.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 352f334e2ca8c1d0be3ff0f89482b97500685174
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 0%

---

# Configuration de rapports A4T dans [!DNL Analysis Workspace] pour [!DNL Auto-Allocate] activités

Un [!UICONTROL Affectation automatique] activité dans [!DNL Adobe Target] identifie un gagnant parmi plusieurs expériences et réaffecte automatiquement le trafic du visiteur vers le gagnant pendant que le test se poursuit et apprend. La variable [!UICONTROL Analytics pour Target] Intégration (A4T) pour [!UICONTROL Affectation automatique] permet d’afficher les données de reporting dans [!DNL Adobe Analytics]et vous pouvez optimiser les événements personnalisés ou les mesures définies dans [!DNL Analytics].

Bien que des fonctionnalités d’analyse complètes soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace], quelques modifications apportées à la valeur par défaut [!UICONTROL Analytics pour Target] peut être nécessaire pour interpréter correctement [!UICONTROL Affectation automatique] activités. Ces modifications sont nécessaires en raison des nuances de la section [critères de mesure d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Chaque type de mesure d’optimisation nécessite une configuration de rapport différente dans A4T, comme suit :

* Utilisation d’une [!DNL Analytics] metric

   * [!UICONTROL Maximiser la valeur de mesure par visiteur]
   * [!UICONTROL Maximiser le taux de conversion des visiteurs uniques]

* Utilisation d’une [!DNL Target]Mesure de conversion définie

Ce tutoriel couvre les instructions générales d’A4T et les étapes de configuration de rapports spécifiques aux critères.

## Mesures Analytics avec &quot;[!UICONTROL Maximiser la valeur de mesure par visiteur]&quot;critères d’optimisation

**Définition**: (valeur de mesure globale) / ( nombre de visiteurs)

Pour configurer le rapport, apportez les modifications suivantes au rapport A4T :

| Modifications requises | [!DNL Target]Rapport déclenché | Rapport Panneau A4T |
| --- | --- | --- |
| Maximiser la valeur de mesure pour une [!DNL Analytics] metric | <ul><li>[!UICONTROL Confiance] Les mesures doivent être supprimées.</li><li>[!UICONTROL Effet élévateur (faible)] et [!UICONTROL Effet élévateur (élevé)] doit être supprimé.</li><li>Décochez la présentation en pourcentage de la [!UICONTROL Taux de conversion] pour éviter toute confusion. Voir [Guide général](#guidance) ci-dessous</li><li>La mesure Taux de conversion doit être renommée &quot;Mesure / Visiteur&quot;.</li></ul> | <ul><li>[!UICONTROL Confiance] Les mesures doivent être supprimées.</li><li>[!UICONTROL Effet élévateur (faible)] et [!UICONTROL Effet élévateur (élevé)] doit être supprimé.</li><li>Décochez la présentation en pourcentage de la [!UICONTROL Taux de conversion] pour éviter toute confusion. Voir [Guide général](#guidance) ci-dessous</li><li>La mesure Taux de conversion doit être renommée &quot;Mesure / Visiteur&quot;.</li><li>Assurez-vous que les plages de dates et d’heures correspondent aux valeurs affichées dans la variable [!DNL Target] rapport. Voir [Guide général](#guidance) ci-dessous</li></ul> |

![Maximiser la valeur de mesure pour les recettes](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] mesures avec &quot;[!UICONTROL Taux de conversion des visiteurs uniques]&quot;critères d’optimisation

**Définition**: (nombre de visiteurs uniques avec une valeur positive de la mesure) / (nombre total de visiteurs uniques)

Exemple : supposons que votre mesure d’optimisation soit [!UICONTROL Recettes]. L’activité comporte cinq visiteurs uniques et trois d’entre eux effectuent un achat. Dans cet exemple, cette valeur = (3 visiteurs pour lesquels [!UICONTROL Recettes] est positif) / (5 visiteurs uniques au total) = 0,6 = 60 %.

>[!NOTE]
>
>Le taux de conversion comme référencé ici peut faire référence à des actions en dehors des commandes, telles que des clics, des impressions, etc. Dans ce cas, le critère maximise toujours le nombre de visiteurs qui cliquent ou affichent la page, respectivement.

Pour configurer le rapport, apportez les modifications suivantes au rapport A4T :

| Modifications requises | Rapport déclenché par Target | Rapport Panneau A4T |
| --- | --- | --- |
| Maximiser les conversions pour une [!DNL Analytics] metric | <ul><li>[!UICONTROL Confiance] Les mesures doivent être supprimées.</li><li>Tous [!UICONTROL Effet élévateur] Les mesures doivent être supprimées.</li><li>Décochez la présentation en pourcentage de la [!UICONTROL Taux de conversion] pour éviter toute confusion. Voir [Guide général](#guidance) ci-dessous</li></ul> | <ul><li>[!UICONTROL Confiance] Les mesures doivent être supprimées.</li><li>Tous [!UICONTROL Effet élévateur] Les mesures doivent être supprimées.</li><li>Créez un segment pour filtrer les visiteurs avec une valeur de mesure positive qui ont consulté l’activité analysée. Voir [Création d’un segment](#segment) ci-dessous</li><li>Remplacez la valeur auto-renseignée [!UICONTROL Taux de conversion] de sorte que représente la division entre [!UICONTROL Visiteurs uniques] avec une valeur de mesure positive et des visiteurs uniques. Voir [Mise à jour de la mesure Taux de conversion](#update-conversion-metric) ci-dessous</li><li>Décochez la présentation en pourcentage de la [!UICONTROL Taux de conversion] pour éviter toute confusion. Voir [Guide général](#guidance) ci-dessous</li><li>Assurez-vous que les plages de dates et d’heures correspondent aux valeurs affichées dans la variable [!DNL Target] rapport. Voir [Guide général](#guidance) ci-dessous</li></ul> |

### Rapport Panneau A4T par défaut - Conseils supplémentaires

Les sections suivantes contiennent des informations supplémentaires sur les conseils supplémentaires à suivre lors de la configuration du rapport Panneau A4T par défaut.

#### Création d’un segment {#segment}

1. Cliquez sur le bouton **signe &quot;+&quot;** en regard de **[!UICONTROL Segments]** dans le rail de gauche.

   ![Signe plus en regard des segments dans le rail de gauche.](/help/integrations/assets/plus-sign.png)

1. Titre du segment &quot;Visiteurs avec une valeur de mesure positive&quot;.
1. Sous **[!UICONTROL Définition]**, en regard de **[!UICONTROL Inclure]**, sélectionnez **[!UICONTROL Visiteur]**.
1. Sous **[!UICONTROL Définition]**, sélectionnez la mesure d’optimisation dans votre activité.

   Dans cet exemple, supposons que [!UICONTROL Recettes] comme mesure d’optimisation.

1. Sélectionnez le[!UICONTROL est supérieur à]&quot;, puis spécifiez &quot;0&quot;.

   Ces paramètres filtrent tous les visiteurs avec une valeur de mesure positive.

1. Cliquez sur **[!UICONTROL Enregistrer]**.

   ![Valeur de mesure positive](/help/integrations/assets/positive-metric-value.png)

1. Ajoutez le segment nouvellement créé nommé &quot;Visiteurs avec une valeur de mesure positive&quot; au panneau A4T.
1. Faites glisser et déposez le [!UICONTROL Visiteurs uniques] dans la même colonne que &quot;Visiteurs avec une valeur de mesure positive&quot;.

   Cette configuration crée un segment de tous les visiteurs uniques pour lesquels la valeur de mesure est positive. Dans cet exemple, tous les visiteurs uniques dont les recettes sont supérieures à zéro.

#### Mettez à jour le [!UICONTROL Taux de conversion] metric {#update-conversion-metric}

1. Si vous ne l’avez pas déjà fait, supprimez la [!UICONTROL Taux de conversion] , comme expliqué ci-dessous.
1. Ajoutez une mesure en cliquant sur le signe &quot;+&quot; en regard de l’événement **[!UICONTROL Mesures]** dans le rail de gauche.
1. Nommez la mesure &quot;Taux de conversion&quot; et définissez-la comme &quot;([!UICONTROL Visiteurs uniques] avec la valeur de mesure positive) divisée par &quot;Visiteurs uniques&quot;, comme illustré ci-dessous.

   Ajoutez le segment nouvellement créé (étapes définies ci-dessous) de &quot;Visiteurs avec une valeur de mesure positive&quot;, l’opérateur de division, la mesure &quot;Visiteurs uniques&quot; dans le numérateur et &quot;Visiteurs uniques&quot; comme dénominateur.

   ![Taux de conversion dans le panneau A4T.](/help/integrations/assets/conversion-rate.png)

1. Cliquez sur **[!UICONTROL Enregistrer]**.

1. Placez la mesure &quot;Taux de conversion&quot; que vous venez de créer dans le panneau existant.
1. Cliquez sur l’icône d’engrenage, puis désélectionnez la **[!UICONTROL Pourcentage]** , car cette valeur peut prêter à confusion.

   La configuration correcte du rapport doit générer un résultat qui ressemble à l’illustration suivante :

   ![Taux de conversion des visites uniques dans le rapport Panneau A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]taux de conversion défini

Pour configurer le rapport, apportez les modifications suivantes au rapport A4T :

| Modifications requises | Rapport déclenché par Target | Rapport Panneau A4T |
| --- | --- | --- |
| [!DNL Analytics] création de rapports avec [!DNL Target] mesure de conversion | <ul><li>[!UICONTROL Confiance] Les mesures doivent être supprimées.</li><li>[!UICONTROL Effet élévateur (faible)] et [!UICONTROL Effet élévateur (élevé)] doit être supprimé.</li><li>Décochez la présentation en pourcentage de la [!UICONTROL Taux de conversion] pour éviter toute confusion. Voir [Guide général](#guidance) ci-dessous</li></ul> | <ul><li>[!UICONTROL Confiance] Les mesures doivent être supprimées.</li><li>[!UICONTROL Effet élévateur (faible)] et [!UICONTROL Effet élévateur (élevé)] doit être supprimé.</li><li>Décochez la présentation en pourcentage de la [!UICONTROL Taux de conversion] pour éviter toute confusion. Voir [Guide général](#guidance) ci-dessous</li><li>Assurez-vous que les plages de dates et d’heures correspondent aux valeurs affichées dans la variable [!DNL Target] rapport. Voir [Guide général](#guidance) ci-dessous</li></ul> |

La configuration correcte du rapport doit générer un résultat qui ressemble à l’illustration suivante :

![Conversions des activités](/help/integrations/assets/optimized-table.png)

## Directives générales pour [!UICONTROL Analytics pour Target] (A4T) {#guidance}

Vous pouvez accéder à une [!UICONTROL Analytics pour Target] en cliquant sur le lien de l’écran de rapport dans [!UICONTROL Adobe Target] (désigné ultérieurement dans ce guide sous le nom de &quot;[!DNL Target]Rapport déclenché&quot;). Vous pouvez également créer le panneau A4T dans [!DNL Analytics] (détails plus loin dans cette section).

Les sections suivantes indiquent les configurations requises, selon l’une de ces méthodes. Toutefois, les étapes suivantes constituent des conseils généraux :

* Les mesures de confiance doivent être supprimées du panneau A4T, quelle que soit la méthode de création du panneau (les deux sont présentées ci-dessous). Vous pouvez référencer ces valeurs dans [!DNL Target] création de rapports. En outre, les gagnants d’activité peuvent être identifiés dans la variable [!DNL Target] création de rapports. Vous trouverez des informations détaillées sur l’identification des gagnants d’activité dans la section [Identification du gagnant de l’activité](#winner) ci-dessous.
>>
* Pour éviter toute confusion, désélectionnez le[!UICONTROL Pourcentage]&quot; présentation de la [!UICONTROL Taux de conversion] mesure. Voir [Masquer le pourcentage de la variable [!UICONTROL Taux de conversion] column](#hide-percentage) ci-dessous
>>
* Si vous créez un panneau A4T, assurez-vous que les plages de dates et d’heures correspondent à celles de votre [!DNL Target] rapport. Voir [Alignement de la date et de l’heure dans le panneau A4T](#aligning-date-and-time) ci-dessous

### Masquer le pourcentage de la variable [!UICONTROL Taux de conversion] column {#hide-percentage}

1. Cliquez sur le bouton **engrenage** en regard du titre de la propriété [!UICONTROL Taux de conversion] colonne .

   ![Icône d’engrenage dans la colonne Taux de conversion](/help/integrations/assets/coversion-rate-gear-icon.png)

   La variable [!UICONTROL Colonne] la boîte de dialogue settings s’affiche :

   ![Boîte de dialogue Paramètres de colonne](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Désélectionnez l’option **[!UICONTROL Pourcentage]** .

   Votre panneau A4T n’inclut désormais pas les pourcentages comme taux de conversion et ne correspond plus à [!DNL Target], comme illustré ci-dessous :

   ![Colonne Taux de conversion n’affichant aucun pourcentage](/help/integrations/assets/no-percentages.png)

### Alignement de la date et de l’heure dans le panneau A4T {#aligning-date-and-time}

1. sous chaque panneau, vérifiez la plage de dates à laquelle le panneau fait référence pour vous assurer que la plage de dates correspond à celle de [!DNL Target] rapport.

   ![Période dans le panneau A4T](/help/integrations/assets/date-range.png)

1. Dans [!DNL Analytics], définissez la période sur 00:00 - 23:59.

### Identification de l’activité gagnante {#winner}

[!DNL Auto-Allocate] les gagnants d’activité sont sélectionnés lorsqu’un taux de conversion gagnant est associé à des valeurs de confiance supérieures ou égales à 95 %. Ces valeurs doivent être référencées dans la variable [!DNL Target] , car les calculs de confiance reflètent les méthodes les plus conservatrices [!DNL Target] recommande pour [!UICONTROL Affectation automatique] activités. Voir [Garanties statistiques de l’affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} dans le *[!UICONTROL Guide du professionnel d’Adobe Target]*.

>[!NOTE]
>
Les badges &quot;Pas encore de gagnant&quot; et &quot;Gagnant&quot; ne sont pas disponibles dans le panneau A4T dans [!DNL Analysis Workspace]. En outre, le badge &quot;étoile&quot; gagnante s’affiche dans [!DNL Target] rapports pour [!UICONTROL Affectation automatique] Les activités doivent être ignorées. Voir [Affectation automatique](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} in *Prise en charge d’A4T pour les activités d’affectation automatique et de ciblage automatique* dans le *[!UICONTROL Guide du professionnel d’Adobe Target]*.

### Création d’A4T pour [!UICONTROL Affectation automatique] dans [!DNL Analysis Workspace]

1. Pour créer un panneau A4T pour une [!UICONTROL Affectation automatique] rapport d’activité, commencez par [!UICONTROL Analytics pour Target] dans [!DNL Analysis Workspace], comme illustré ci-dessous.

   ![Analytics for Target - Rapport d’affectation automatique](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Effectuez les sélections suivantes :

   * **[!UICONTROL Expérience de contrôle]**: sélectionnez une expérience.
   * **[!UICONTROL Mesure de normalisation]**: sélectionnez **[!UICONTROL Visiteurs]** (inclus dans le panneau A4T par défaut). [!UICONTROL Affectation automatique] normalise toujours les taux de conversion par visiteurs uniques.
   * **Mesures de succès**: sélectionnez la même mesure (optimisation) que celle utilisée lors de la création de l’activité. S’il s’agissait d’une [!DNL Target]mesure de conversion définie, sélectionnez **[!UICONTROL Conversion des activités]**. Sinon, sélectionnez la variable [!DNL Adobe Analytics] mesure que vous avez utilisée.









