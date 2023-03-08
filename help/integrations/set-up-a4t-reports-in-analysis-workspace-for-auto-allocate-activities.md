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
source-git-commit: 14a362214dce9d698c78438c3a47424b59aa4632
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 0%

---

# Configuration de rapports A4T dans [!DNL Analysis Workspace] pour [!DNL Auto-Allocate] activités

Un [!DNL Auto-Allocate] activité identifie un gagnant parmi plusieurs expériences et réaffecte automatiquement du trafic supplémentaire vers le gagnant pendant que le test se poursuit et apprend. Le [!UICONTROL Analytics pour Target] Intégration (A4T) pour [!UICONTROL Affectation automatique] vous permet d’afficher vos données de création de rapports dans [!DNL Adobe Analytics]et vous pouvez même optimiser les événements personnalisés ou les mesures définies dans [!DNL Analytics].

Bien que des fonctionnalités d’analyse complètes soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace], quelques modifications apportées à la valeur par défaut **[!UICONTROL Analytics pour Target]** doivent être correctement interprétés. [!DNL Auto-Allocate] les activités, en raison des nuances de [critères d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

Ce tutoriel décrit les modifications recommandées pour l’analyse [!DNL Auto-Allocate] activités dans [!DNL Analysis Workspace]. Les concepts clés sont les suivants :

* [!UICONTROL Visiteurs] doit toujours être utilisé comme mesure de normalisation dans [!DNL Auto-Allocate] activités.
* Lorsque la mesure est une [!DNL Adobe Analytics] , le numérateur approprié pour le taux de conversion dépend du type de critère d’optimisation choisi lors de la configuration de l’activité.
   * Le critère d’optimisation du &quot;taux de conversion de visiteur unique maximal&quot; comporte un taux de conversion dont le numérateur est un nombre de visiteurs uniques avec une valeur positive de la mesure.
   * La &quot;valeur de mesure maximale par visiteur* a un taux de conversion dont le numérateur est la valeur de mesure régulière dans [!DNL Adobe Analytics]. Elle est fournie par défaut dans la variable **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace].
* Lorsque votre mesure d’optimisation est une [!DNL Target] mesure de conversion définie, la mesure par défaut **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace] gère la configuration du panneau.
* Le [!UICONTROL Confiance] nombres vus dans [!DNL Analysis Workspace] ne reflètent pas la variable [statistiques plus conservatives utilisées par [!UICONTROL Affectation automatique]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629), et doivent donc être supprimés.

## Création d’A4T pour [!DNL Auto-Allocate] dans [!DNL Analysis Workspace]

Pour créer A4T pour [!DNL Auto-Allocate] le rapport commence par **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace], comme illustré ci-dessous. Effectuez ensuite les sélections suivantes :

1. **[!UICONTROL Expérience de contrôle]**: Vous pouvez choisir n’importe quelle expérience.
2. **[!UICONTROL Mesure de normalisation]**: Sélectionnez Visiteurs. [!DNL Auto-Allocate] normalise toujours les taux de conversion par visiteurs uniques.
3. **[!UICONTROL Mesures de succès]**: Sélectionnez la même mesure que celle utilisée lors de la création de l’activité. S’il s’agissait d’une [!DNL Target] mesure de conversion définie, sélectionnez **Conversion des activités**. Sinon, sélectionnez la variable [!DNL Adobe Analytics] mesure que vous avez utilisée.

![[!UICONTROL Analytics pour Target] configuration du panneau pour [!DNL Auto-Allocate] activités.](assets/AAFigure1.png)

*Figure 1 : [!UICONTROL Analytics pour Target] configuration du panneau pour [!DNL Auto-Allocate] activités.*

>[!NOTE]
>
> Vous pouvez également obtenir une **[!UICONTROL Analytics pour Target]** si vous cliquez sur le lien de l’écran de rapport dans [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversion] mesures ou [!DNL Analytics] mesures avec les critères d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;

Le panneau A4T par défaut gère les [!DNL Auto-Allocate] activités dans lesquelles la mesure d’objectif est soit une [!DNL Target] conversion ou [!DNL Analytics] avec le critère d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;.

Un exemple de ce panneau s’affiche pour la fonction [!UICONTROL Recettes] où &quot;Maximiser la valeur de mesure par visiteur&quot; a été sélectionnée comme critère d’optimisation au moment de la création de l’activité. Comme mentionné précédemment, [!DNL Auto-Allocate] utilise des calculs de confiance plus conservateurs que ceux utilisés dans la variable **[!UICONTROL Analytics pour Target]** du panneau. Adobe recommande de supprimer la mesure de confiance, ainsi que les mesures d’effet élévateur inférieur et supérieur associées.

![[!UICONTROL Analytics for Target - Rapport d’affectation automatique] panel](assets/AAFigure2.png)

*Figure 2 : Le rapport recommandé pour [!DNL Auto-Allocate] d’une [!DNL Analytics] mesure &quot;Maximiser la valeur de mesure par optimisation du visiteur&quot;. Pour ces types de mesures, ainsi que [!DNL Target] mesures de conversion définies, la valeur par défaut **[!UICONTROL Analytics pour Target]**dans [!DNL Analysis Workspace] peut être utilisé.*

## [!DNL Analytics] mesures avec les critères d’optimisation &quot;Maximiser le taux de conversion des visiteurs uniques&quot;

Lorsqu’une [!DNL Adobe Analytics] est utilisée avec un critère d’optimisation de *Maximiser le taux de conversion des visiteurs uniques*, la valeur par défaut **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace] doivent être modifiées.

La mesure de succès correspond désormais au nombre de visiteurs uniques pour lesquels la mesure de conversion était positive. Pour ce faire, créez un segment qui filtre les accès avec une valeur positive de la mesure. Créez ce segment comme suit :

1. Sélectionnez la **[!UICONTROL Composants]** > **[!UICONTROL Créer un segment]** dans le [!DNL Analysis Workspace] de la barre d’outils.
1. Faites glisser la mesure utilisée au moment de la création de l’activité du panneau de gauche vers le **[!UICONTROL Définition]** de la zone du segment.
1. Sélectionnez les valeurs de la mesure qui sont **supérieur à** une valeur numérique de 0.
1. Dans la **[!UICONTROL Inclure]** menu déroulant, sélectionnez **[!UICONTROL Visiteurs]**.
1. Attribuez un nom approprié à votre segment.

Un exemple de création de segment est illustré dans la figure ci-dessous, où vous sélectionnez [!UICONTROL Visiteurs avec des recettes positives].

![[!UICONTROL Visiteurs avec des recettes positives] dans [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Tableau 3 : Création de segments pour [!DNL Adobe Analytics] mesures dont les critères d’optimisation sont égaux à &quot;[!UICONTROL Maximiser le taux de conversion des visiteurs uniques].&quot; Dans cet exemple, la mesure est [!UICONTROL Recettes]et l’objectif d’optimisation est d’optimiser le nombre de visiteurs avec des recettes positives.*

Une fois le segment approprié créé, la valeur par défaut  **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace] peut être modifié.

1. Ajouter une seconde **Visiteurs uniques** à côté de la mesure existante [!UICONTROL Visiteurs] colonne des mesures.
2. Faites glisser le segment nouvellement créé sous la première colonne pour produire un panneau qui ressemble à l’illustration 4. Remarquez la différence : le nombre de visiteurs uniques avec des recettes positives représente une fraction du nombre total de visiteurs uniques affectés à chaque expérience.

   ![Figure4.png](assets/AAFigure4.png)

   *Tableau 4 : Filtrage [!UICONTROL Visiteurs uniques] par le segment nouvellement créé*

3. Un taux de conversion peut être [calculé rapidement](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) en mettant en surbrillance la première et la deuxième colonne, en cliquant avec le bouton droit de la souris, en sélectionnant **[!UICONTROL Créer une mesure d’après la sélection]** > **[!UICONTROL Diviser]**.

   Le taux de conversion par défaut doit être supprimé et remplacé par cette nouvelle mesure calculée, comme illustré dans l’image ci-dessous. Vous devrez peut-être modifier la mesure calculée nouvellement créée pour l’afficher sous la forme d’une **[!UICONTROL Format]** > **[!UICONTROL Pourcentage]** jusqu’à deux décimales, comme indiqué.

   ![Figure5.png](assets/AAFigure5.png)

   *Figure 5 : La finale [!UICONTROL Affectation automatique] panneau affichant les taux de conversion d’une mesure de conversion de recettes binaire*

## Résumé

Les étapes de ce tutoriel ont démontré comment configurer correctement [!DNL Analysis Workspace] pour afficher [!UICONTROL Affectation automatique] données de création de rapports.

En résumé :

* Lorsque la mesure est une [!DNL Target] mesure de conversion définie ou [!DNL Adobe Analytics] avec le critère d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;, le panneau de l’espace de travail par défaut configuré avec les visiteurs comme mesure de normalisation doit être utilisé.
* Lorsque la mesure est une [!DNL Adobe Analytics] avec le critère d’optimisation &quot;Maximiser le taux de conversion des visiteurs uniques&quot;, vous devez utiliser un taux de conversion défini comme la fraction des visiteurs pour lesquels la mesure est positive. Pour ce faire, créez un segment correspondant qui filtre la variable [!UICONTROL Visiteur unique] mesure.
