---
title: Configuration des rapports A4T dans [!DNL Analysis Workspace] pour [!UICONTROL Affectation automatique] Activités
description: Comment configurer des rapports A4T dans [!DNL Analysis Workspace] pour obtenir les résultats attendus lors de l’exécution [!UICONTROL Affectation automatique] activités.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 99d49995ec7e3dd502a149376693e2770f3e2a9d
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 0%

---

# Configuration de rapports A4T dans [!DNL Analysis Workspace] pour [!DNL Auto-Allocate] activités

Un [!DNL Auto-Allocate] activité identifie un gagnant parmi plusieurs expériences et réaffecte automatiquement le trafic vers le gagnant pendant que le test continue à s’exécuter et à apprendre. La variable [!UICONTROL Analytics pour Target] Intégration (A4T) pour [!UICONTROL Affectation automatique] vous permet d’afficher vos données de création de rapports dans [!DNL Adobe Analytics]et vous pouvez même optimiser les événements personnalisés ou les mesures définies dans [!DNL Analytics].

Bien que des fonctionnalités d’analyse complètes soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace], quelques modifications apportées à la valeur par défaut **[!UICONTROL Analytics pour Target]** peut être nécessaire pour interpréter correctement [!DNL Auto-Allocate] les activités, en raison des nuances de [critères de mesure d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Ce tutoriel décrit les modifications recommandées pour l’analyse [!DNL Auto-Allocate] activités dans [!DNL Analysis Workspace]. Les concepts clés sont les suivants :

* [!UICONTROL Visiteurs] doit toujours être utilisé comme mesure de normalisation dans [!DNL Auto-Allocate] activités.
* Lorsque la mesure est une [!DNL Adobe Analytics] , le calcul du taux de conversion varie, selon le type de critère d’optimisation défini lors de la configuration de l’activité.
   * Le numérateur de taux de conversion &quot;maximiser le taux de conversion des visiteurs uniques&quot; est un nombre de visiteurs uniques. *avec une valeur positive de la mesure*.
   * Cette méthode ne nécessite pas de segment supplémentaire pour correspondre au taux de conversion affiché dans la variable [!DNL Target] Interface utilisateur.
* Le numérateur de taux de conversion &quot;valeur de mesure maximale par visiteur&quot; est la valeur de mesure régulière dans la variable [!DNL Adobe Analytics]. Cette mesure est fournie par défaut dans la variable [!DNL Analytics for Target] dans [!DNL Analysis Workspace].
   * Ce que cela signifie : optimise le nombre de visiteurs qui convertissent (&quot;count once per visitor&quot;).
   * Cette méthode nécessite la création d’un segment supplémentaire dans les rapports afin de correspondre au taux de conversion affiché dans la variable [!DNL Target] Interface utilisateur.
* Lorsque votre mesure d’optimisation est une [!DNL Target] mesure de conversion définie, la mesure par défaut **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace] gère la configuration du panneau.
* Pour tous [!UICONTROL Affectation automatique] activités créées avant la [!DNL Target Standard/Premium] Version 23.3.1 (30 mars 2023) [!DNL Analytics Workspace] et [!DNL Target] afficher la même valeur pour [!UICONTROL Confiance].

  Pour tous [!UICONTROL Affectation automatique] les activités créées après le 30 mars 2023, les valeurs de l’intervalle de confiance affichées dans [!DNL Analysis Workspace] ne reflètent pas la variable [statistiques plus conservatives utilisées par [!UICONTROL Affectation automatique]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} dans si ces activités ont des *both* des conditions suivantes :

   * [!DNL Analytics] comme source des rapports (A4T)
   * [!DNL Analytics] mesures d’optimisation

  Les mesures de confiance doivent être supprimées du panneau A4T. Vous pouvez référencer ces valeurs dans [!DNL Target] création de rapports.

## Création d’A4T pour [!DNL Auto-Allocate] dans [!DNL Analysis Workspace]

Pour créer un panneau A4T pour une [!DNL Auto-Allocate] le rapport commence par **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace], comme illustré ci-dessous. Effectuez ensuite les sélections suivantes :

1. **[!UICONTROL Expérience de contrôle]**: vous pouvez choisir n’importe quelle expérience.
1. **[!UICONTROL Mesure de normalisation]**: sélectionnez Visiteurs (par défaut, ils sont inclus dans le panneau A4T). [!DNL Auto-Allocate] normalise toujours les taux de conversion par visiteurs uniques.
1. **[!UICONTROL Mesures de succès]**: sélectionnez la même mesure que celle utilisée lors de la création de l’activité. S’il s’agissait d’une [!DNL Target] mesure de conversion définie, sélectionnez **Conversion des activités**. Sinon, sélectionnez la variable [!DNL Adobe Analytics] mesure que vous avez utilisée.

![[!UICONTROL Analytics pour Target] configuration du panneau pour [!DNL Auto-Allocate] activités.](assets/AAFigure1.png)

*Figure 1 : [!UICONTROL Analytics pour Target] configuration du panneau pour [!DNL Auto-Allocate] activités.*

Vous pouvez également obtenir une **[!UICONTROL Analytics pour Target]** si vous cliquez sur le lien de l’écran de rapport dans [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversion] mesures ou [!DNL Analytics] mesures avec les critères d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;

Lorsque la mesure d’objectif est :

* Une mesure de conversion Target
* Mesure Analytics avec le critère d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;

Le panneau A4T par défaut configure automatiquement le rapport.

Un exemple de ce panneau s’affiche pour la fonction [!UICONTROL Recettes] où &quot;Maximiser la valeur de mesure par visiteur&quot; a été sélectionnée comme critère d’optimisation au moment de la création de l’activité. Comme mentionné précédemment, [!DNL Auto-Allocate] utilise des calculs de confiance plus conservateurs que ceux utilisés dans la variable **[!UICONTROL Analytics pour Target]** du panneau. Adobe recommande de supprimer la mesure de confiance du panneau A4T, ainsi que les mesures d’effet élévateur inférieur et supérieur associées. référencez plutôt les valeurs de confiance dans [!DNL Target] création de rapports.

>[!NOTE]
>
>Les valeurs de confiance dans les rapports A4T sont moins conservatrices que [!DNL Target] création de rapports et peut indiquer de manière prématurée un gagnant pour une [!UICONTROL Affectation automatique] activité.


![[!UICONTROL Analytics for Target - Rapport d’affectation automatique] panel](assets/AAFigure2.png)

*Figure 2 : Rapport recommandé pour [!DNL Auto-Allocate] d’une [!DNL Analytics] mesure &quot;Maximiser la valeur de mesure par optimisation du visiteur&quot;. Pour ces types de mesures, ainsi que [!DNL Target] mesures de conversion définies, la valeur par défaut **[!UICONTROL Analytics pour Target]**dans [!DNL Analysis Workspace] peut être utilisé.*

## [!DNL Analytics] mesures avec les critères d’optimisation &quot;Maximiser les visiteurs uniques&quot;

Le critère d’optimisation &quot;Maximiser le visiteur unique avec le taux de conversion&quot; fait référence au nombre de visiteurs pour lesquels la valeur de mesure est positive. Si, par exemple, le taux de conversion est défini comme des recettes, le critère &quot;Maximiser le taux de conversion des visiteurs uniques avec le taux de conversion&quot; est optimisé en fonction du nombre de visiteurs uniques pour lesquels le chiffre d’affaires est supérieur à 0. En d’autres termes, ce critère optimise le nombre de visiteurs qui génèrent des recettes, plutôt que la valeur des recettes elles-mêmes.

>[!NOTE]
>
>Le taux de conversion comme référencé ici peut faire référence à des actions en dehors des commandes, telles que des clics, des impressions, etc. Dans ce cas, le critère maximise toujours le nombre de visiteurs qui cliquent ou affichent la page, respectivement.

La variable [!DNL Analytics for Target] dans [!DNL Analysis Workspace] doit être modifié si ce critère d’optimisation est utilisé avec un [!DNL Adobe Analytics] mesure.

Lorsque ce critère d’optimisation est utilisé, la mesure de succès est le nombre de visiteurs uniques pour lesquels la mesure de conversion était positive. Par conséquent, pour afficher cette valeur, un nouveau segment doit être créé pour filtrer les accès avec une valeur positive pour la mesure.

Créez ce segment comme suit :

1. Sélectionnez la variable **[!UICONTROL Composants]** > **[!UICONTROL Créer un segment]** dans le [!DNL Analysis Workspace] barre d’outils.
1. Faites glisser la mesure utilisée au moment de la création de l’activité du panneau de gauche vers le **[!UICONTROL Définition]** de la zone du segment.
1. Sélectionnez les valeurs de la mesure qui sont **supérieur à** une valeur numérique de 0.
1. Dans la **[!UICONTROL Inclure]** , sélectionnez **[!UICONTROL Visiteurs]**.
1. Attribuez un nom approprié à votre segment.

Un exemple de création de segment est illustré dans la figure ci-dessous, où la mesure de succès est [!UICONTROL Visiteurs avec des recettes positives].

![[!UICONTROL Visiteurs avec des recettes positives] segment dans [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figure 3 : Création de segments pour [!DNL Adobe Analytics] mesures dont les critères d’optimisation sont égaux à &quot;[!UICONTROL Maximiser le taux de conversion des visiteurs uniques].&quot; Dans cet exemple, la mesure est [!UICONTROL Recettes]et l’objectif d’optimisation est d’optimiser le nombre de visiteurs avec des recettes positives.*

Une fois le segment approprié créé, vous pouvez modifier le segment par défaut.  **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace] pour afficher les valeurs des critères d’optimisation. Pour ce faire, procédez comme suit :

1. Ajouter une seconde **Visiteurs uniques** à côté de la mesure existante [!UICONTROL Visiteurs] colonne des mesures.
2. Faites glisser le segment nouvellement créé sous la première colonne pour produire un panneau qui ressemble à l’illustration 4. Notez la différence de valeurs des colonnes : le nombre de visiteurs uniques avec des recettes positives doit être une fraction du nombre total de visiteurs uniques affectés à chaque expérience (comme illustré ci-dessous).

   ![Figure4.png](assets/AAFigure4.png)

   *Figure 4 : Filtrage [!UICONTROL Visiteurs uniques] par le segment nouvellement créé*

3. Un taux de conversion peut être [calculé rapidement](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) en mettant en surbrillance la première et la deuxième colonne, en cliquant avec le bouton droit de la souris, en sélectionnant **[!UICONTROL Créer une mesure d’après la sélection]** > **[!UICONTROL Diviser]**.

   Le taux de conversion par défaut doit être supprimé et remplacé par cette nouvelle mesure calculée, comme illustré dans l’image ci-dessous. Vous devrez peut-être modifier la mesure calculée nouvellement créée pour l’afficher sous la forme d’une **[!UICONTROL Format]** > **[!UICONTROL Pourcentage]** jusqu’à deux décimales, comme indiqué.

   ![Figure5.png](assets/AAFigure5.png)

   *Figure 5 : Le tableau final [!UICONTROL Affectation automatique] panneau affichant les taux de conversion d’une mesure de conversion de recettes binaire*

## Résumé

Les étapes de ce tutoriel ont démontré comment configurer correctement [!DNL Analysis Workspace] pour afficher [!UICONTROL Affectation automatique] données de reporting.

En résumé :

* Lorsque la mesure est une [!DNL Target] mesure de conversion définie ou [!DNL Adobe Analytics] avec le critère d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;, le panneau de l’espace de travail par défaut configuré avec les visiteurs comme mesure de normalisation doit être utilisé.
* Lorsque la mesure est une [!DNL Adobe Analytics] avec le critère d’optimisation &quot;Maximiser le taux de conversion des visiteurs uniques&quot;, vous devez déterminer la fraction de visiteurs avec une valeur de mesure positive par rapport au nombre total de visiteurs. Pour ce faire, créez un segment correspondant qui filtre la variable [!UICONTROL Visiteur unique] sur cette mesure.
