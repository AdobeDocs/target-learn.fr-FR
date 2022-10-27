---
title: Configuration des rapports A4T dans Analysis Workspace pour les activités de ciblage automatique
description: Une fois que vous avez mis en place votre intégration Analytics for Target (A4T) et que vous exécutez des activités de ciblage automatique, comment pouvez-vous vous assurer que vous interprétez correctement les résultats ? Suivez ces étapes pour configurer des rapports A4T dans Analysis Workspace afin d’obtenir les résultats escomptés lors de l’exécution d’activités de ciblage automatique.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: e1acb84970b967625e0b6c7495067ed6456a6aa3
workflow-type: tm+mt
source-wordcount: '2653'
ht-degree: 1%

---

# Configuration de rapports A4T dans Analysis Workspace pour [!DNL Auto-Target] activités

Intégration d’Analytics for Target (A4T) pour [!DNL Auto-Target] Les activités utilisent les algorithmes d’apprentissage automatique (ML) d’ensemble d’Adobe Target pour choisir la meilleure expérience pour chaque visiteur en fonction de son profil, de son comportement et de son contexte, tout en utilisant une mesure d’objectif Adobe Analytics.

Bien que de riches fonctionnalités d’analyse soient disponibles dans Adobe Analytics Analysis Workspace, quelques modifications ont été apportées au **[!UICONTROL Analytics pour Target]** doivent être correctement interprétés. [!DNL Auto-Target] en raison des différences entre les activités d’expérimentation (A/B manuel et affectation automatique) et les activités de personnalisation ([!DNL Auto-Target]).

Ce tutoriel décrit les modifications recommandées pour l’analyse [!DNL Auto-Target] dans Workspace, qui reposent sur les concepts clés suivants :

* Le **[!UICONTROL Comparaison du contrôle et du ciblage]** peut être utilisée pour distinguer les expériences de contrôle de celles diffusées par la variable [!DNL Auto-Target] algorithme ML d’ensemble.
* Les visites doivent être utilisées comme mesure de normalisation lors de l’affichage des ventilations de performances au niveau de l’expérience. En outre, [La méthodologie de comptage par défaut d’Adobe Analytics peut inclure les visites pour lesquelles l’utilisateur ne voit pas réellement le contenu de l’activité.](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), mais ce comportement par défaut peut être modifié à l’aide d’un segment à portée appropriée (détails ci-dessous).
* L’attribution portée sur la recherche en amont des visites (également appelée &quot;intervalle de recherche en amont des visites&quot; sur le modèle d’attribution prescrit) est utilisée par les modèles ML d’Adobe Target pendant leurs phases de formation, et le même modèle d’attribution (autre que celui par défaut) doit être utilisé lors de la ventilation de la mesure d’objectif.

## Création d’A4T pour [!DNL Auto-Target] panneau dans Workspace

Pour créer A4T pour [!DNL Auto-Target] , commencez par la variable **[!UICONTROL Analytics pour Target]** dans Workspace, comme illustré ci-dessous, ou commencez par un tableau à structure libre. Effectuez ensuite les sélections suivantes :

1. **[!UICONTROL Expérience de contrôle]**: Vous pouvez choisir n’importe quelle expérience ; toutefois, vous remplacerez ce choix ultérieurement. Notez que pour [!DNL Auto-Target] , l’expérience de contrôle est en fait une stratégie de contrôle, qui consiste soit à : a) diffuser de manière aléatoire parmi toutes les expériences, soit b) diffuser une seule expérience (ce choix est effectué au moment de la création de l’activité dans Adobe Target). Même si vous avez choisi (b), votre [!DNL Auto-Target] activité désignée comme expérience spécifique pour le contrôle. Vous devez tout de même suivre l’approche décrite dans ce tutoriel pour l’analyse d’A4T pour [!DNL Auto-Target] activités.
2. **[!UICONTROL Mesure de normalisation]**: Sélectionnez Visites.
3. **[!UICONTROL Mesures de succès]**: Bien que vous puissiez sélectionner une ou plusieurs mesures sur lesquelles générer des rapports, vous devez généralement afficher les rapports sur la même mesure que celle choisie pour l’optimisation lors de la création de l’activité dans Adobe Target.

![Figure1.png](assets/Figure1.png)
*Figure 1 : Configuration du panneau Analytics for Target pour [!DNL Auto-Target] activités.*

>[!NOTE]
>
>Pour configurer le panneau Analytics for Target pour les activités de ciblage automatique, choisissez n’importe quelle expérience de contrôle, choisissez Visites comme mesure de normalisation et choisissez la même mesure d’objectif que celle choisie pour l’optimisation lors de la création de l’activité Target.

## Utilisez la dimension Contrôle / Ciblé pour comparer le modèle ML d’ensemble d’Adobe Target à votre contrôle.

Le panneau A4T par défaut est conçu pour les tests A/B classiques (manuels) ou les activités d’affectation automatique dans le but de comparer les performances de chaque expérience par rapport à l’expérience de contrôle. Dans [!DNL Auto-Target] Toutefois, la première comparaison de commande doit se faire entre les activités de contrôle *stratégie* et le *stratégie* (en d’autres termes, déterminer l’effet élévateur de la performance globale de la fonction [!DNL Auto-Target] modèle ML d’ensemble sur la stratégie de contrôle).

Pour effectuer cette comparaison, utilisez le **[!UICONTROL Comparaison du contrôle et du ciblage (Analytics pour Target)]** dimension. Effectuez un glisser-déposer pour remplacer le **[!UICONTROL Expériences Target]** dans le rapport A4T par défaut.

Notez que ce remplacement invalide les calculs de l’effet élévateur et du degré de confiance par défaut sur le panneau A4T. Pour éviter toute confusion, vous pouvez supprimer ces mesures du panneau par défaut, en laissant le rapport suivant :

![Figure2.png](assets/Figure2.png)
*Figure 2 : Rapport de base recommandé pour [!DNL Auto-Target] activités. Ce rapport a été configuré pour comparer le trafic ciblé (traité par le modèle ML d’ensemble) à votre trafic de contrôle.*

>[!NOTE]
>
>Actuellement, les numéros Effet élévateur et Degré de confiance ne sont pas disponibles pour les dimensions de contrôle et les dimensions ciblées des rapports A4T pour le ciblage automatique. Tant que la prise en charge n’est pas ajoutée, l’effet élévateur et le degré de confiance peuvent être calculés manuellement en téléchargeant la variable [calculateur de confiance](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Ajout de ventilations de mesures au niveau de l’expérience

Pour mieux comprendre les performances du modèle ML d’ensemble, vous pouvez examiner les ventilations au niveau de l’expérience de la variable **[!UICONTROL Comparaison du contrôle et du ciblage]** dimension. Dans Workspace, faites glisser le **[!UICONTROL Expériences Target]** sur votre rapport, puis ventilez séparément chacune des dimensions de contrôle et de ciblage.

![Figure3.png](assets/Figure3.png)
*Tableau 3 : Ventilation de la dimension ciblée par expérience Target*

Un exemple du rapport obtenu est présenté ici.

![Figure4.png](assets/Figure4.png)
*Tableau 4 : Un standard [!DNL Auto-Target] rapport avec des ventilations au niveau de l’expérience. Notez que votre mesure d’objectif peut être différente et que votre stratégie de contrôle peut comporter une seule expérience.*

>[!TIP]
>
>Dans Workspace, cliquez sur l’icône d’engrenage pour masquer les pourcentages dans la colonne Taux de conversion afin de vous concentrer sur les taux de conversion de l’expérience. Notez que les taux de conversion seront alors formatés sous forme de décimales, mais interprétés comme des pourcentages en conséquence.

## Pourquoi &quot;Visites&quot; est la mesure de normalisation correcte pour [!DNL Auto-Target] activités

Lors de l’analyse d’une [!DNL Auto-Target] , choisissez toujours Visites comme mesure de normalisation par défaut. [!DNL Auto-Target] la personnalisation sélectionne une expérience pour un visiteur une fois par visite (officiellement, une fois par session Adobe Target), ce qui signifie que l’expérience présentée à un utilisateur peut changer à chaque visite. Par conséquent, si vous utilisez Visiteurs uniques comme mesure de normalisation, le fait qu’un seul utilisateur puisse voir plusieurs expériences (au cours de différentes visites) peut entraîner des taux de conversion déroutants.

Voici un exemple simple : imaginez un scénario dans lequel deux visiteurs entrent dans une campagne qui ne comporte que deux expériences. Le premier visiteur effectue deux visites. Elles sont affectées à l’expérience A lors de la première visite, mais à l’expérience B lors de la seconde visite (en raison de la modification de leur état de profil lors de cette deuxième visite). Après la deuxième visite, le visiteur effectue une conversion en passant une commande. La conversion est attribuée à l’expérience la plus récemment affichée (expérience B). Le deuxième visiteur se rend également deux fois sur le site et affiche l’expérience B à chaque fois, mais ne procède jamais à une conversion.

Comparons les rapports au niveau des visiteurs et des visites :

| Expérience | Visiteurs uniques | Visites | Conversions | Norme du visiteur. Conv. clics publicitaires | Standard des visites. Conv. clics publicitaires |
| --- | --- | --- | --- | --- | --- |
| Une | 1 | 1 | - | 0% | 0 % |
| B | 2 | 3 | 1 | 50 % | 33,3 % |
| Totaux | 2 | 4 | 1 | 50 % | 25 % |

*Tableau 1 : Exemple de comparaison des rapports normalisés par les visiteurs et normalisés par les visites pour un scénario dans lequel les décisions sont liées à une visite (et non aux visiteurs, comme avec les tests A/B standard). Dans ce scénario, les mesures normalisées par les visiteurs sont déroutantes.*

Comme le montre le tableau, les nombres au niveau du visiteur présentent une incongruité évidente. Bien qu’il existe deux visiteurs uniques au total, il ne s’agit pas de la somme des visiteurs uniques individuels pour chaque expérience. Bien que le taux de conversion au niveau du visiteur ne soit pas nécessairement incorrect, lorsqu’on compare des expériences individuelles, les taux de conversion au niveau du visiteur ont sans doute beaucoup plus de sens. Officiellement, l’unité d’analyse (&quot;visites&quot;) est identique à l’unité d’attractivité de décision, ce qui signifie que des ventilations de mesures au niveau de l’expérience peuvent être ajoutées et comparées.

## Filtre pour les visites réelles de l’activité

La méthodologie de comptage par défaut d’Adobe Analytics pour les visites d’une activité Target peut inclure les visites pour lesquelles l’utilisateur n’a pas interagi avec l’activité Target. Cela est dû à la manière dont les affectations d’activité Target sont conservées dans le contexte du visiteur Analytics. Par conséquent, le nombre de visites de l’activité Target peut parfois être exagéré, ce qui entraîne une dépression des taux de conversion.

Si vous préférez créer un rapport sur les visites au cours desquelles l’utilisateur a réellement interagi avec l’activité de ciblage automatique (soit par l’entrée de l’activité, soit par un événement d’affichage/de visite, soit par une conversion), vous pouvez :

1. Créez un segment spécifique qui comprend les accès provenant de l’activité Target en question, puis
1. Filtrez la mesure Visites à l’aide de ce segment.

**Pour créer le segment :**

1. Sélectionnez la **[!UICONTROL Composants > Créer un segment]** dans la barre d’outils Workspace.
2. Saisissez un **[!UICONTROL Titre]** pour votre segment. Dans l’exemple ci-dessous, le segment est nommé [!DNL "Hit with specific Auto-Target activity"].
3. Faites glisser le **[!UICONTROL Activités Target]** dimension au segment **[!UICONTROL Définition]** .
4. Utilisez la variable **[!UICONTROL est égal à]** de l’opérateur.
5. Recherchez votre activité Target spécifique.
6. Sélectionnez l’icône d’engrenage, puis cliquez sur **[!UICONTROL Modèle d’attribution > Instance]** comme illustré dans la figure ci-dessous.
7. Cliquez sur **[!UICONTROL Enregistrer]**.

![Figure5.png](assets/Figure5.png)
*Figure 5 : Utilisez un segment tel que celui présenté ici pour filtrer la mesure Visites dans A4T pour [!DNL Auto-Target] rapport*

Une fois le segment créé, utilisez-le pour filtrer la mesure Visites. Par conséquent, la mesure Visites inclut uniquement les visites où l’utilisateur a interagi avec l’activité Target.

**Pour filtrer les Visites à l’aide de ce segment :**

1. Faites glisser le segment nouvellement créé à partir de la barre d’outils des composants, puis survolez la base de la **[!UICONTROL Visites]** libellé de mesure jusqu’à ce qu’un bleu **[!UICONTROL Filtrer par]** s’affiche.
2. Relâchez le segment. Le filtre sera appliqué à cette mesure.

Le panneau final s’affiche comme suit.

![Figure6.png](assets/Figure6.png)
*Tableau 6 : Panneau de création de rapports avec le segment &quot;Accès avec activité de ciblage automatique spécifique&quot; appliqué au [!UICONTROL Visites] mesure. Ainsi, seules les visites où un utilisateur a réellement interagi avec l’activité Target en question sont incluses dans le rapport.*

## Assurez-vous que la mesure et l’attribution de l’objectif sont alignées sur votre critère d’optimisation.

L’intégration A4T permet [!DNL Auto-Target]Le modèle ML de s doit être *formé* en utilisant les mêmes données d’événement de conversion que celles utilisées par Adobe Analytics pour *génération de rapports de performances*. Cependant, certaines hypothèses doivent être utilisées pour interpréter ces données lors de la formation des modèles ML, qui diffèrent des hypothèses par défaut faites lors de la phase de création de rapports dans Adobe Analytics.

Plus précisément, les modèles ML d’Adobe Target utilisent un modèle d’attribution à portée de visite. En d’autres termes, ils supposent qu’une conversion doit avoir lieu au cours de la même visite qu’un affichage du contenu pour l’activité, afin que la conversion soit &quot;attribuée&quot; à la décision prise par le modèle ML. Cela est nécessaire pour que Target puisse garantir une formation rapide de ses modèles. Target ne peut pas attendre jusqu’à 30 jours pour une conversion (la fenêtre d’attribution par défaut des rapports dans Adobe Analytics) avant de l’inclure dans les données d’entraînement de ses modèles.

Ainsi, la différence entre l’attribution utilisée par les modèles de Target (pendant la formation) et l’attribution par défaut utilisée dans l’interrogation des données (pendant la génération du rapport) peut entraîner des incohérences. Il peut même sembler que les modèles ML sont peu performants, alors qu&#39;en fait le problème réside dans l&#39;attribution.


>[!TIP]
>
>Si les modèles ML optimisent une mesure attribuée différemment des mesures que vous affichez dans un rapport, les modèles peuvent ne pas fonctionner comme prévu. Pour éviter cela, assurez-vous que les mesures d’objectif de votre rapport utilisent la même définition de mesure et la même attribution utilisées par les modèles ML de Target.

La définition de mesure exacte et les paramètres d’attribution dépendent de [critère d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported) vous avez spécifié lors de la création de l’activité.


### Conversions définies par Target ou mesures Analytics avec *Maximiser la valeur de mesure par visite*

Lorsque la mesure est une conversion Target ou une mesure Analytics avec **Maximiser la valeur de mesure par visite**, la définition de mesure d’objectif permet à plusieurs événements de conversion de se produire au cours d’une même visite.
Pour afficher les mesures d’objectif qui ont la même méthodologie d’attribution utilisée par les modèles ML Adobe Target, procédez comme suit :

1. Passez la souris sur l’icône d’engrenage de la mesure d’objectif :
   ![gearicon.png](assets/gearicon.png)
1. Dans le menu qui s’affiche, faites défiler l’écran jusqu’à **[!UICONTROL Paramètres des données]**.
1. Sélectionner **[!UICONTROL Utilisation d’un modèle d’attribution différent du modèle par défaut]** (s’il n’est pas déjà sélectionné) :
   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)
1. Cliquez sur **[!UICONTROL Modifier]**.
1. Sélectionner **[!UICONTROL Modèle]**: **[!UICONTROL Participation]**, et **[!UICONTROL Intervalle de recherche en amont]**: **[!UICONTROL Visite]**.
   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)
1. Cliquez sur **[!UICONTROL Appliquer]**.

Ces étapes garantissent que votre rapport attribuera la mesure d’objectif à l’affichage de l’expérience, si l’événement de mesure d’objectif s’est produit. *à tout moment* (&quot;participation&quot;) lors de la même visite que celle où une expérience a été affichée.

### Mesures Analytics avec *Taux de conversion de visites uniques*

**Définition de la visite avec un segment de mesure positif**

Dans le scénario où vous avez sélectionné *Maximiser le taux de conversion des visites uniques* comme critère d’optimisation, la définition correcte du taux de conversion est la fraction des visites pour lesquelles la valeur de mesure est positive. Pour ce faire, vous pouvez créer un segment en filtrant les visites par rapport aux visites avec une valeur positive de la mesure, puis en filtrant la mesure Visites.


1. Comme avant, sélectionnez la variable **[!UICONTROL Composants > Créer un segment]** dans la barre d’outils Workspace.
2. Saisissez un **[!UICONTROL Titre]** pour votre segment. Dans l’exemple ci-dessous, le segment est nommé [!DNL "Visits with an order"].
3. Faites glisser la mesure de base que vous avez utilisée dans votre objectif d’optimisation dans le segment . Dans l’exemple ci-dessous, nous utilisons la méthode **commandes** afin que le taux de conversion mesure la fraction des visites pour lesquelles une commande est enregistrée.
4. En haut à gauche du conteneur de définitions de segment, sélectionnez **[!UICONTROL Inclure]** **Visite**.
5. Utilisez la variable **[!UICONTROL est supérieur à]** et définissez la valeur sur 0 (c’est-à-dire que ce segment inclut les visites pour lesquelles la mesure des commandes est positive).
6. Cliquez sur **[!UICONTROL Enregistrer]**.

![Figure7.png](assets/Figure7.png)
*Figure 7 : Filtrage de la définition de segment pour les visites avec un ordre positif. Selon la mesure d’optimisation de votre activité, vous devrez remplacer les commandes par une mesure appropriée.*

**Appliquez-le aux visites dans la mesure filtrée de l’activité.**

Ce segment peut désormais être utilisé pour filtrer les visites avec un nombre positif de commandes, et lorsqu’un accès a eu lieu pour le [!DNL Auto-Target]activité. La procédure de filtrage d’une mesure est similaire à la procédure précédente. Après avoir appliqué le nouveau segment à la mesure de visite déjà filtrée, le panneau du rapport doit ressembler à la figure 8.

![Figure8.png](assets/Figure8.png)
*Figure 8 : Le panneau du rapport avec la mesure de conversion de visites uniques correcte : c’est-à-dire le nombre de visites au cours desquelles un accès de l’activité a été enregistré et où la mesure de conversion (commandes dans cet exemple) était non nulle.*


## Étape finale : Créer un taux de conversion qui capture la magie ci-dessus

Avec les modifications apportées aux mesures Visite et Objectif des sections précédentes, la dernière modification que vous devez apporter à votre A4T par défaut pour [!DNL Auto-Target] le panneau de création de rapports permet de créer des taux de conversion correspondant au bon ratio (celui de la mesure d’objectif corrigée), par rapport à une mesure &quot;Visites&quot; correctement filtrée.

Pour ce faire, créez une mesure calculée en procédant comme suit :

1. Sélectionnez la **[!UICONTROL Composants > Créer une mesure]** dans la barre d’outils Workspace.
1. Saisissez un **[!UICONTROL Titre]** pour votre mesure. Par exemple, &quot;Taux de conversion corrigé des visites pour l’activité XXX&quot;.
1. Sélectionner **[!UICONTROL Format]** = Pourcentage et **[!UICONTROL Nombre de décimales]** = 2.
1. Faites glisser la mesure d’objectif appropriée pour votre activité (par exemple, Conversions d’activité) dans la définition, puis utilisez l’icône en forme d’engrenage sur cette mesure d’objectif pour ajuster le modèle d’attribution à (Participation|Visite), comme décrit précédemment.
1. Sélectionner **[!UICONTROL Ajouter > Conteneur]** en haut à droite de l’objet **[!UICONTROL Définition]** .
1. Sélectionnez l&#39;opérateur de division (÷) entre les deux conteneurs.
1. Faites glisser le segment précédemment créé, nommé &quot;Accès avec des [!DNL Auto-Target] &quot;activity&quot; dans ce tutoriel, pour ce [!DNL Auto-Target] activité.
1. Faites glisser le **[!UICONTROL Visites]** dans le conteneur de segments.
1. Cliquez sur **[!UICONTROL Enregistrer]**.

>[!TIP]
>
> Vous pouvez également créer cette mesure à l’aide de la variable [fonctionnalité de mesure calculée rapide](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en).

La définition de mesure calculée complète s’affiche ici.

![Figure9.png](assets/Figure9.png)
*Figure 9 : Définition de la mesure de taux de conversion de modèle corrigée pour les visites et l’attribution. (Notez que cette mesure dépend de votre mesure d’objectif et de votre activité. En d’autres termes, cette définition de mesure n’est pas réutilisable entre les activités.)*

>[!IMPORTANT]
>
>La mesure Taux de conversion du panneau A4T n’est pas liée à l’événement de conversion ou à la mesure de normalisation dans le tableau. Lorsque vous effectuez les modifications suggérées dans ce tutoriel, le taux de conversion ne s’adapte pas automatiquement aux modifications. Par conséquent, si vous apportez la modification à l’une (ou aux deux) des attributions d’événement de conversion et à la mesure de normalisation, vous devez vous souvenir d’une étape finale pour modifier également le taux de conversion, comme illustré ci-dessus.

## Résumé : Exemple final de panneau Workspace pour [!DNL Auto-Target] rapports

En combinant toutes les étapes ci-dessus dans un seul panneau, la figure ci-dessous présente une vue complète du rapport recommandé pour [!DNL Auto-Target] Activités d’A4T. Ce rapport est identique à celui utilisé par les modèles d’apprentissage automatique de Target pour optimiser la mesure de vos objectifs. Il incorpore toutes les nuances et recommandations abordées dans ce tutoriel. Ce rapport est également plus proche des méthodologies de comptage utilisées dans les rapports Target traditionnels [!DNL Auto-Target] activités.

![Figure10.png](assets/Figure10.png)
*Figure 10 : A4T final [!DNL Auto-Target] dans Adobe Analytics Workspace, qui combine tous les ajustements aux définitions de mesures décrits dans les sections précédentes de ce document.*
