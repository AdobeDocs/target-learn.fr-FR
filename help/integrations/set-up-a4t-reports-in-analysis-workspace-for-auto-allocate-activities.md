---
title: Configuration des rapports A4T dans Analysis Workspace pour les activités d’affectation automatique
description: Une fois que vous avez mis en place votre intégration Analytics for Target (A4T) et que vous exécutez des activités d’affectation automatique, comment pouvez-vous vous assurer que vous interprétez correctement les résultats ? Suivez ces étapes pour configurer des rapports A4T dans Analysis Workspace afin d’obtenir les résultats escomptés lors de l’exécution d’activités d’affectation automatique.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 47ddfc9eeb5d4c1f5adf4f7d1fdb9fd031878e78
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Configuration de rapports A4T dans Analysis Workspace pour [!DNL Auto-Allocate] activités

Un [!DNL Auto-Allocate] activité identifie un gagnant parmi plusieurs expériences et réaffecte automatiquement du trafic supplémentaire vers le gagnant pendant que le test se poursuit et apprend. Intégration d’Analytics for Target (A4T) pour [!DNL Auto-Allocate] vous permet d’afficher vos données de création de rapports dans Adobe Analytics et vous pouvez même optimiser les événements personnalisés ou les mesures définies dans Adobe Analytics.

Bien que de riches fonctionnalités d’analyse soient disponibles dans Adobe Analytics Analysis Workspace, quelques modifications ont été apportées au **[!UICONTROL Analytics pour Target]** doivent être correctement interprétés. [!DNL Auto-Allocate] les activités, en raison des nuances de [critères d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

Ce tutoriel décrit les modifications recommandées pour l’analyse [!DNL Auto-Allocate] activités dans Workspace. Les concepts clés sont les suivants :

* Les visiteurs doivent toujours être utilisés comme mesure de normalisation dans [!DNL Auto-Allocate] activités.
* Lorsque la mesure est une mesure Adobe Analytics, le numérateur approprié pour le taux de conversion dépend du type de critère d’optimisation choisi lors de la configuration de l’activité.
   * Le critère d’optimisation du &quot;taux de conversion de visiteur unique maximal&quot; comporte un taux de conversion dont le numérateur est un nombre de visiteurs uniques avec une valeur positive de la mesure.
   * La &quot;valeur de mesure maximale par visiteur* comporte un taux de conversion dont le numérateur est la valeur de mesure standard dans Adobe Analytics. Elle est fournie par défaut dans la variable **[!UICONTROL Analytics pour Target]** dans Workspace.
* Lorsque votre mesure d’optimisation est une mesure de conversion définie par Target, la valeur par défaut **[!UICONTROL Analytics pour Target]** dans Workspace gère la configuration du panneau.
* Les nombres de confiance affichés dans Workspace ne reflètent pas la variable [statistiques plus conservatrices utilisées par l’affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629), et doivent donc être supprimés.


## Création d’A4T pour [!DNL Auto-Allocate] panneau dans Workspace

Pour créer A4T pour [!DNL Auto-Allocate] le rapport commence par **[!UICONTROL Analytics pour Target]** dans Workspace, comme illustré ci-dessous. Effectuez ensuite les sélections suivantes :

1. **[!UICONTROL Expérience de contrôle]**: Vous pouvez choisir n’importe quelle expérience
2. **[!UICONTROL Mesure de normalisation]**: Sélectionnez Visiteurs : l’affectation automatique normalise toujours les taux de conversion en fonction des visiteurs uniques.
3. **[!UICONTROL Mesures de succès]**: Sélectionnez la même mesure que celle utilisée lors de la création de l’activité. S’il s’agissait d’une mesure de conversion définie par Target, sélectionnez **Conversion des activités**. Sinon, sélectionnez la mesure Adobe Analytics que vous avez utilisée.

![AAFigure1.png](assets/AAFigure1.png)
*Figure 1 : Configuration du panneau Analytics for Target pour [!DNL Auto-Allocate] activités.*

>[!NOTE]
>
> Vous pouvez également obtenir une **[!UICONTROL Analytics pour Target]** si vous cliquez sur le lien de l’écran de rapport dans Adobe Target.

## Mesures de conversion Target ou mesures Analytics avec les critères d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;

Le panneau A4T par défaut gère les [!DNL Auto-Allocate] activités pour lesquelles la mesure d’objectif est soit une conversion cible, soit une mesure Analytics avec le critère d’optimisation &quot;Maximiser la valeur de mesure par visiteur&quot;.

Un exemple de ce panneau s’affiche pour la mesure Recettes, où &quot;Maximiser la valeur de mesure par visiteur&quot; a été sélectionné comme critère d’optimisation au moment de la création de l’activité. Comme mentionné précédemment, [!DNL Auto-Allocate] utilise des calculs de confiance plus conservateurs que ceux utilisés par la variable **[!UICONTROL Analytics pour Target]** du panneau. Il est donc recommandé de supprimer la mesure de confiance, ainsi que les mesures d’effet élévateur inférieur et supérieur associées.

![Figure2.png](assets/AAFigure2.png)
*Figure 2 : Le rapport recommandé pour [!DNL Auto-Allocate] activités avec une mesure Analytics Maximiser la valeur de mesure par critère d’optimisation du visiteur. Pour ces types de mesures, ainsi que les mesures de conversion définies par Target, la variable **[!UICONTROL Analytics pour Target]**dans workspace peut être utilisé.*


## Mesures Analytics avec critères d’optimisation &quot;Maximiser le taux de conversion des visiteurs uniques&quot;

Lorsqu’une mesure Adobe Analytics est utilisée avec un critère d’optimisation de *Maximiser le taux de conversion des visiteurs uniques*, la valeur par défaut **[!UICONTROL Analytics pour Target]** dans workspace doit être modifié.

La mesure de succès correspond désormais au nombre de visiteurs uniques pour lesquels la mesure de conversion était positive. Pour ce faire, créez un segment qui filtre les accès avec une valeur positive de la mesure. Créez ce segment comme suit :

1. Sélectionnez la **Composants** > **Créer un segment** dans la barre d’outils Workspace.
1. Faites glisser la mesure utilisée au moment de la création de l’activité du panneau de gauche vers le **Définition** de la zone du segment.
1. Sélectionnez les valeurs de la mesure qui sont **supérieur à** une valeur numérique de 0.
1. Dans la **Inclure** menu déroulant, sélectionnez **Visiteurs**
1. Attribuez un nom approprié à votre segment.

Un exemple de création de segment est illustré dans la figure ci-dessous, où nous sélectionnons les visiteurs pour lesquels le chiffre d’affaires est positif.

![Figure3.png](assets/AAFigure3.png)
*Tableau 3 : Création de segments pour les mesures Adobe Analytics avec des critères d’optimisation égaux à l’option Maximiser le taux de conversion des visiteurs uniques. Dans cet exemple, la mesure est Recettes et l’objectif d’optimisation est d’optimiser le nombre de visiteurs avec des recettes positives.*

Une fois le segment approprié créé, la valeur par défaut  **[!UICONTROL Analytics pour Target]** dans workspace peut être modifié.

1. Ajouter une seconde **Visiteurs uniques** à côté de la colonne de mesures des visiteurs existants
2. Faites glisser le segment que vous venez de créer sous la première colonne pour produire un panneau qui ressemble à l’illustration 4. Remarquez la différence : le nombre de visiteurs uniques avec des recettes positives représente une fraction du nombre total de visiteurs uniques affectés à chaque expérience.
   ![Figure4.png](assets/AAFigure4.png)
   *Tableau 4 : Filtrage des visiteurs uniques par segment nouvellement créé*
3. Un taux de conversion peut être [calculé rapidement](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) en mettant en surbrillance la première et la deuxième colonne, en cliquant avec le bouton droit de la souris, en sélectionnant **Créer une mesure d’après la sélection** > **Diviser**. Le taux de conversion par défaut doit être supprimé et remplacé par cette nouvelle mesure calculée, comme illustré dans l’image ci-dessous. Vous devrez peut-être modifier la mesure calculée nouvellement créée pour l’afficher sous la forme d’une **Format** > **Pourcentage** jusqu’à deux décimales, comme indiqué.
   ![Figure4.png](assets/AAFigure5.png)

   *Tableau 4 : Le panneau final Affectation automatique affiche les taux de conversion d’une mesure de conversion de recettes binaire*


## Conclusion

Les étapes ci-dessus ont démontré comment configurer correctement [!DNL Workspace] pour afficher des données de rapport d’affectation automatique. En résumé :

* Lorsque la mesure est une mesure de conversion définie par Target ou une mesure Adobe Analytics avec critère d’optimisation *Maximiser la valeur de mesure par visiteur*, le panneau de l’espace de travail par défaut configuré avec les visiteurs comme mesure de normalisation doit être utilisé.
* Lorsque la mesure est une mesure Adobe Analytics avec le critère d’optimisation &quot;Maximiser le taux de conversion des visiteurs uniques&quot;, vous devez utiliser un taux de conversion défini comme la fraction des visiteurs pour lesquels la mesure est positive. Pour ce faire, créez un segment correspondant qui filtre la mesure du visiteur unique.
