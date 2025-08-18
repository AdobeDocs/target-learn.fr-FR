---
title: Configuration des rapports A4T dans [!DNL Analysis Workspace] for [!DNL Auto-Target] Activities
description: Comment configurer les rapports A4T dans  [!DNL Analysis Workspace]  obtenir les résultats attendus lors de l’exécution d’activités [!UICONTROL Auto-Target] ?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=fr#premium newtab=true" tooltip="Voir ce qui est inclus dans Target Premium."
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 78e5b5f7fa8f4c1a08c06c6d2b0e1a5242cd464c
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 1%

---

# Configurer des rapports A4T dans [!DNL Analysis Workspace] pour les activités [!DNL Auto-Target]

>[!IMPORTANT]
>
>Pour [!UICONTROL Auto-Target] activités, vous devez vérifier les rapports dans [!DNL Analytics Workspace] et créer manuellement un panneau A4T.

L’intégration [!UICONTROL Analytics for Target] (A4T) pour les activités [!DNL Auto-Target] utilise les algorithmes de machine learning (ML) d’[!DNL Adobe Target] ensemble pour choisir la meilleure expérience pour chaque visiteur en fonction de son profil, de son comportement et du contexte, tout en utilisant une mesure d’objectif [!DNL Adobe Analytics].

Bien que des fonctionnalités d’analyse complètes soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace] **[!UICONTROL Analytics for Target]**, quelques modifications sont nécessaires pour interpréter correctement les activités de [!DNL Auto-Target], en raison des différences entre les activités d’expérimentation ([!UICONTROL A/B Test] et [!UICONTROL Auto-Allocate] manuels) et les activités de personnalisation ([!UICONTROL [!UICONTROL Auto-Target]]).

Ce tutoriel décrit les modifications recommandées pour l’analyse des activités [!UICONTROL Auto-Target] dans [!DNL Analysis Workspace], qui sont basées sur les concepts clés suivants :

* La dimension **[!UICONTROL Control vs Targeted]** peut être utilisée pour distinguer les expériences [!UICONTROL Control] de celles diffusées par l’algorithme ML d’ensemble [!UICONTROL Auto-Target].
* Les visites doivent être utilisées comme mesure de normalisation lors de l’affichage des répartitions de performances au niveau de l’expérience. En outre, la méthodologie de comptage par défaut d’[Adobe Analytics peut inclure des visites où l’utilisateur ne voit pas réellement le contenu de l’activité](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=fr#metrics){target=_blank} mais ce comportement par défaut peut être modifié en utilisant un segment de portée appropriée (détails ci-dessous).
* L’attribution étendue de la recherche en amont des visites, également appelée « fenêtre de recherche en amont des visites » sur le modèle d’attribution prescrit, est utilisée par les modèles ML [!DNL Adobe Target] pendant leurs phases d’entraînement. Le même modèle d’attribution (autre que celui par défaut) doit être utilisé lors de la répartition de la mesure d’objectif.

## Créer A4T pour [!UICONTROL Auto-Target] panneau dans [!DNL Analysis Workspace]

Pour créer un A4T pour [!UICONTROL Auto-Target] rapport, commencez par le panneau **[!UICONTROL Analytics for Target]** dans [!DNL Analysis Workspace], comme illustré ci-dessous, ou commencez par un tableau à structure libre. Effectuez ensuite les sélections suivantes :

1. **[!UICONTROL Control Experience]** : vous pouvez choisir n’importe quelle expérience, mais vous remplacerez ce choix ultérieurement. Notez que pour les activités de [!UICONTROL Auto-Target], l’expérience de contrôle est en fait une stratégie de contrôle, qui consiste soit à a) servir de manière aléatoire parmi toutes les expériences, soit b) servir une seule expérience (ce choix est fait au moment de la création de l’activité en [!DNL Adobe Target]). Même si vous avez opté pour le choix (b), votre activité [!UICONTROL Auto-Target] a désigné une expérience spécifique comme contrôle. Vous devez toujours suivre l’approche décrite dans ce tutoriel pour analyser A4T pour les activités [!UICONTROL Auto-Target].
2. **[!UICONTROL Normalizing Metric]** : sélectionnez [!UICONTROL Visits].
3. **[!UICONTROL Success Metrics]** : bien que vous puissiez sélectionner n’importe quelle mesure pour laquelle créer des rapports, vous devez généralement afficher les rapports sur la même mesure que celle choisie pour l’optimisation lors de la création de l’activité dans [!DNL Target].

   Configuration du panneau ![[!UICONTROL Analytics for Target] pour les activités [!UICONTROL Auto-Target].](assets/Figure1.png)

   *Figure 1 : configuration [!UICONTROL Analytics for Target] panneau pour les activités [!UICONTROL Auto-Target].*

>[!TIP]
>
>Pour configurer votre panneau [!UICONTROL Analytics for Target] pour les activités de [!UICONTROL Auto-Target], choisissez n’importe quelle expérience de contrôle, choisissez [!UICONTROL Visits] comme mesure de normalisation et choisissez la même mesure d’objectif qui a été choisie pour l’optimisation lors de la création de l’activité de [!DNL Target].

## Utilisez la dimension [!UICONTROL Control vs.Targeted] pour comparer le modèle ML d&#39;ensemble [!DNL Target] à votre contrôle

Le panneau A4T par défaut est conçu pour les activités classiques (manuelles) de [!UICONTROL A/B Test] ou de [!UICONTROL Auto-Allocate], où l’objectif est de comparer les performances d’expériences individuelles à celles de l’expérience de contrôle. Toutefois, dans [!UICONTROL Auto-Target] activités, la comparaison devrait se faire en premier lieu entre la *stratégie* de lutte et la *stratégie* ciblée. En d’autres termes, déterminer l’effet élévateur de la performance globale du modèle ML d’ensemble [!UICONTROL Auto-Target] sur la stratégie de contrôle.

Pour effectuer cette comparaison, utilisez la dimension **[!UICONTROL Control vs Targeted (Analytics for Target)]** . Effectuez un glisser-déposer pour remplacer la dimension **[!UICONTROL Target Experiences]** dans le rapport A4T par défaut.

Notez que ce remplacement invalide les calculs de [!UICONTROL Lift and Confidence] par défaut dans le panneau A4T. Pour éviter toute confusion, vous pouvez supprimer ces mesures du panneau par défaut et conserver le rapport suivant :

Panneau ![[!UICONTROL Experiences by Activity Conversions] dans [!DNL Analysis Workspace]](assets/Figure2.png)

*Figure 2 : rapport de référence recommandé pour les activités [!DNL Auto-Target]. Ce rapport a été configuré pour comparer le trafic ciblé (fourni par le modèle ML d’ensemble) à votre trafic de contrôle.*

>[!NOTE]
>
>Actuellement, les nombres [!UICONTROL Lift and Confidence] ne sont pas disponibles pour les dimensions [!UICONTROL Control vs Targeted] des rapports A4T pour [!UICONTROL Auto-Target]. Jusqu’à ce que la prise en charge soit ajoutée, [!UICONTROL Lift and Confidence] peut être calculée manuellement en téléchargeant le [calculateur de confiance](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=fr).

## Ajout de répartitions de mesures au niveau de l’expérience

Pour mieux comprendre les performances du modèle ML d’ensemble dans insight, vous pouvez examiner les répartitions au niveau de l’expérience de la dimension **[!UICONTROL Control vs Targeted]**. Dans [!DNL Analysis Workspace], faites glisser la dimension **[!UICONTROL Target Experiences]** sur votre rapport, puis répartissez séparément chacune des dimensions de contrôle et des dimensions ciblées.

Panneau ![[!UICONTROL Experiences by Activity Conversions] dans [!DNL Analysis Workspace]](assets/Figure3.png)

*Figure 3 : Répartition de la dimension ciblée par expériences cible*

Un exemple du rapport obtenu est illustré ici.

Panneau ![[!UICONTROL Experiences by Activity Conversions] dans [!DNL Analysis Workspace]](assets/Figure4.png)

*Figure 4 : rapport [!UICONTROL Auto-Target] standard avec des répartitions au niveau de l’expérience. Notez que votre mesure d’objectif peut être différente et votre stratégie de contrôle peut avoir une seule expérience.*

>[!TIP]
>
>Dans [!DNL Analysis Workspace], cliquez sur l’icône en forme d’engrenage pour masquer les pourcentages dans la colonne [!UICONTROL Conversion Rate] afin de garder le focus sur les taux de conversion d’expérience. Les taux de conversion seront alors formatés en décimales, mais interprétés comme des pourcentages en conséquence.

## Pourquoi « [!UICONTROL Visits] » est-il la mesure de normalisation correcte pour les activités [!UICONTROL Auto-Target] ?

Lors de l’analyse d’une activité de [!UICONTROL Auto-Target], choisissez toujours [!UICONTROL Visits] comme mesure de normalisation par défaut. [!UICONTROL Auto-Target] personnalisation sélectionne une expérience pour un visiteur une fois par visite (officiellement, une fois par session [!DNL Target]), ce qui signifie que l’expérience présentée à un visiteur peut changer à chaque visite. Ainsi, si vous utilisez [!UICONTROL Unique Visitors] comme mesure de normalisation, le fait qu’un seul utilisateur ou une seule utilisatrice puisse voir plusieurs expériences (sur différentes visites) conduirait à des taux de conversion déroutants.

Un exemple simple illustre ce point : prenons l’exemple d’un scénario dans lequel deux visiteurs rejoignent une campagne qui ne comporte que deux expériences. Le premier visiteur visite deux fois. Ils sont affectés à l’expérience A lors de la première visite, mais à l’expérience B lors de la deuxième visite (en raison de la modification de l’état de leur profil lors de cette deuxième visite). Après la deuxième visite, le visiteur effectue une conversion en passant une commande. La conversion est attribuée à l’expérience la plus récemment affichée (expérience B). Le deuxième visiteur visite également deux fois et voit l’expérience B les deux fois, mais ne se convertit jamais.

Comparons les rapports au niveau des visiteurs et au niveau des visites :

| Expérience | Visiteurs uniques | Visites | Conversions | Taux de conversion normalisé par le visiteur | Taux de conversion normalisé par les visites |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0 % | 0 % |
| B | 2 | 3 | 1 | 50 % | 33,3 % |
| Totaux | 2 | 4 | 1 | 50 % | 25 % |

*Tableau 1 : exemple de comparaison des rapports normalisés par le visiteur et normalisés par les visites pour un scénario dans lequel les décisions sont liées à une visite (et non à un visiteur, comme avec les tests A/B réguliers). Les mesures normalisées par le visiteur prêtent à confusion dans ce scénario.*

Comme le montre le tableau, il existe une incohérence évidente entre les nombres au niveau des visiteurs. Bien qu’il y ait au total deux visiteurs uniques, il ne s’agit pas d’une somme de visiteurs uniques individuels pour chaque expérience. Bien que le taux de conversion au niveau du visiteur ou de la visiteuse ne soit pas nécessairement faux, lorsqu’on compare des expériences individuelles, les taux de conversion au niveau des visites ont sans doute beaucoup plus de sens. Formellement, l’unité d’analyse (« visites ») est identique à l’unité de finesse des décisions, ce qui signifie que des répartitions de mesures au niveau de l’expérience peuvent être ajoutées et comparées.

## Filtrer les visites réelles sur l’activité

La méthodologie de comptage par défaut [!DNL Adobe Analytics] pour les visites d’une activité [!DNL Target] peut inclure des visites au cours desquelles l’utilisateur ou l’utilisatrice n’a pas interagi avec l’activité [!DNL Target]. Cela est dû à la manière dont les affectations d’activités [!DNL Target] sont conservées dans le contexte du visiteur [!DNL Analytics]. Par conséquent, le nombre de visites de l’activité [!DNL Target] peut parfois être exagéré, ce qui entraîne une baisse des taux de conversion.

Si vous préférez créer des rapports sur les visites au cours desquelles l’utilisateur a réellement interagi avec l’activité [!UICONTROL Auto-Target] (soit par le biais d’une entrée dans l’activité, d’un événement d’affichage ou de visite, ou d’une conversion), vous pouvez :

1. Créez un segment spécifique qui inclut les accès de l’activité de [!DNL Target] en question, puis
1. Filtrez la mesure [!UICONTROL Visits] à l’aide de ce segment.

**Pour créer le segment, procédez comme suit**

1. Sélectionnez l’option **[!UICONTROL Components > Create Segment]** dans la barre d’outils [!DNL Analysis Workspace].
2. Spécifiez un **[!UICONTROL Title]** pour votre segment. Dans l’exemple illustré ci-dessous, le segment est nommé [!DNL "Hit with specific Auto-Target activity"].
3. Faites glisser la dimension de **[!UICONTROL Target Activities]** vers la section de **[!UICONTROL Definition]** de segment.
4. Utilisez l’opérateur **[!UICONTROL equals]** .
5. Recherchez votre activité de [!DNL Target] spécifique.
6. Cliquez sur l’icône d’engrenage, puis sélectionnez **[!UICONTROL Attribution model > Instance]** comme illustré dans la figure ci-dessous.
7. Cliquez sur **[!UICONTROL Save]**.

![Segment dans [!DNL Analysis Workspace]](assets/Figure5.png)

*Figure 5 : utilisez un segment tel que celui illustré ici pour filtrer la mesure de [!UICONTROL Visits] dans votre A4T pour [!UICONTROL Auto-Target] rapport*

Une fois le segment créé, utilisez-le pour filtrer la mesure [!UICONTROL Visits], de sorte que la mesure [!UICONTROL Visits] inclut uniquement les visites au cours desquelles l’utilisateur a interagi avec l’activité [!DNL Target].

**Pour filtrer les [!UICONTROL Visits] à l’aide de ce segment :**

1. Faites glisser le segment nouvellement créé à partir de la barre d’outils des composants, puis passez le curseur sur la base du libellé de mesure de **[!UICONTROL Visits]** jusqu’à ce qu’une invite de **[!UICONTROL Filter by]** bleue s’affiche.
2. Libérez le segment. Le filtre est appliqué à cette mesure.

Le dernier panneau se présente comme suit :

Panneau ![[!UICONTROL Experiences by Activity Conversions] dans [!DNL Analysis Workspace]](assets/Figure6.png)

*Figure 6 : Panneau de création de rapports avec le segment « Accès avec une activité de ciblage automatique spécifique » appliqué à la mesure [!UICONTROL Visits]. Ce segment permet de s’assurer que seules les visites au cours desquelles un utilisateur ou une utilisatrice a réellement interagi avec l’activité de [!DNL Target] en question sont incluses dans le rapport.*

## Assurez-vous que la mesure d’objectif et l’attribution sont alignées avec votre critère d’optimisation

L’intégration A4T permet au modèle ML [!UICONTROL Auto-Target] d’être *entraîné* à l’aide des mêmes données d’événement de conversion que celles que [!DNL Adobe Analytics] utilise pour *générer des rapports de performances*. Cependant, certaines hypothèses doivent être utilisées pour interpréter ces données lors de l’entraînement des modèles ML, qui diffèrent des hypothèses par défaut faites pendant la phase de création de rapports en [!DNL Adobe Analytics].

Plus précisément, les modèles ML [!DNL Adobe Target] utilisent un modèle d’attribution à l’échelle des visites. En d’autres termes, les modèles ML supposent qu’une conversion doit se produire au cours de la même visite qu’un affichage du contenu de l’activité afin que la conversion soit « attribuée » à la décision prise par le modèle ML. Cela est nécessaire pour que [!DNL Target] garantisse une formation rapide de ses modèles. [!DNL Target] ne pouvez pas attendre jusqu’à 30 jours pour une conversion (la fenêtre d’attribution par défaut pour les rapports en [!DNL Adobe Analytics]) avant de l’inclure dans les données de formation de ses modèles.

Ainsi, la différence entre l’attribution utilisée par les modèles de [!DNL Target] (pendant l’entraînement) et l’attribution par défaut utilisée dans les requêtes de données (pendant la génération du rapport) peut entraîner des incohérences. Il peut même sembler que les modèles de ML ont de mauvaises performances, alors qu’en fait le problème réside dans l’attribution.

>[!TIP]
>
>Si les modèles ML effectuent une optimisation pour une mesure qui est attribuée différemment de celle des mesures que vous consultez dans un rapport, les modèles peuvent ne pas fonctionner comme prévu. Pour éviter cela, assurez-vous que les mesures d’objectif de votre rapport utilisent la même définition de mesure et la même attribution que celles utilisées par les modèles ML [!DNL Target].

La définition exacte de la mesure et les paramètres d’attribution dépendent du [critère d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=fr#supported){target=_blank} que vous avez spécifié lors de la création de l’activité.

### Conversions définies par Target ou mesures [!DNL Analytics] avec *Maximiser la valeur de mesure par visite*

Lorsque la mesure est une conversion [!DNL Target] ou une mesure [!DNL Analytics] avec **Maximiser la valeur de la mesure par visite**, la définition de la mesure d’objectif permet à plusieurs événements de conversion de se produire au cours de la même visite.

Pour afficher les mesures d’objectif avec la même méthodologie d’attribution que celle utilisée par les modèles ML [!DNL Target], procédez comme suit :

1. Pointez sur l’icône d’engrenage de la mesure d’objectif :

   ![gearicon.png](assets/gearicon.png)

1. Dans le menu qui s’affiche, faites défiler l’écran jusqu’à **[!UICONTROL Data settings]**.
1. Sélectionnez **[!UICONTROL Use non-default  attribution model]** (s’il n’est pas déjà sélectionné).

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Cliquez sur **[!UICONTROL Edit]**.
1. Sélectionnez **[!UICONTROL Model]** : **[!UICONTROL Participation]** et **[!UICONTROL Lookback window]** : **[!UICONTROL Visit]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. Cliquez sur **[!UICONTROL Apply]**.

Ces étapes garantissent que votre rapport attribue la mesure d’objectif à l’affichage de l’expérience, si l’événement de mesure d’objectif s’est produit *à tout moment* (« participation ») au cours de la même visite qu’une expérience a été affichée.

### [!DNL Analytics] des mesures avec des *taux de conversion de visites uniques*

**Définir la visite avec un segment de mesure positive**

Dans le scénario où vous avez sélectionné *Maximiser le taux de conversion des visites uniques* comme critère d’optimisation, la définition correcte du taux de conversion est la fraction des visites pour lesquelles la valeur de la mesure est positive. Pour ce faire, créez un segment en filtrant les visites sur une valeur positive de la mesure, puis en filtrant la mesure des visites.

1. Comme précédemment, sélectionnez l’option **[!UICONTROL Components > Create Segment]** dans la barre d’outils [!DNL Analysis Workspace].
2. Spécifiez un **[!UICONTROL Title]** pour votre segment.

   Dans l’exemple illustré ci-dessous, le segment est nommé [!DNL "Visits with an order"].

3. Faites glisser dans le segment la mesure de base que vous avez utilisée dans votre objectif d’optimisation.

   Dans l’exemple illustré ci-dessous, nous utilisons la mesure **commandes** afin que le taux de conversion mesure la fraction de visites où une commande est enregistrée.

4. Dans la partie supérieure gauche du conteneur de définition de segment, sélectionnez **[!UICONTROL Include]** **Visite**.
5. Utilisez l’opérateur **[!UICONTROL is greater than]** et définissez la valeur sur 0.

   La définition de la valeur sur 0 signifie que ce segment inclut les visites pour lesquelles la mesure Commandes est positive.

6. Cliquez sur **[!UICONTROL Save]**.

![Figure7.png](assets/Figure7.png)

*Figure 7 : filtrage de la définition de segment pour les visites avec un ordre positif. Selon la mesure d’optimisation de votre activité, vous devez remplacer les commandes par une mesure appropriée*

**Appliquer cette mesure aux visites dans la mesure filtrée par activité**

Ce segment peut désormais être utilisé pour filtrer les visites avec un nombre positif de commandes et l’endroit où l’activité de [!DNL Auto-Target] a eu un accès. La procédure de filtrage d’une mesure est similaire à la précédente. Après avoir appliqué le nouveau segment à la mesure de visite déjà filtrée, le panneau de rapport doit ressembler à la figure 8

![Figure8.png](assets/Figure8.png)

*Figure 8 : panneau de rapport contenant la mesure de conversion de visite unique correcte : le nombre de visites pour lesquelles un accès à l’activité a été enregistré et pour lesquelles la mesure de conversion (commandes dans cet exemple) était différente de zéro.*

## Étape finale : créez un taux de conversion qui capture la magie ci-dessus

Suite aux modifications apportées aux mesures d’[!UICONTROL Visit] et d’objectif dans les sections précédentes, la dernière modification que vous devez apporter à votre A4T par défaut pour [!DNL Auto-Target] panneau de création de rapports consiste à créer des taux de conversion correspondant au bon rapport (celui de la mesure d’objectif corrigée) par rapport à une mesure « Visites » filtrée de manière appropriée.

Pour ce faire, créez un [!UICONTROL Calculated Metric] en procédant comme suit :

1. Sélectionnez l’option **[!UICONTROL Components > Create Metric]** dans la barre d’outils [!DNL Analysis Workspace].
1. Spécifiez un **[!UICONTROL Title]** pour votre mesure. Par exemple, « Taux de conversion corrigé de la visite pour l’activité XXX ».
1. Sélectionnez **[!UICONTROL Format]** = Pourcentage et **[!UICONTROL Decimal Places]** = 2.
1. Faites glisser la mesure d’objectif appropriée pour votre activité (par exemple, [!UICONTROL Activity Conversions]) dans la définition, puis utilisez l’icône en forme d’engrenage sur cette mesure d’objectif pour ajuster le modèle d’attribution sur (Participation|Visite), comme décrit précédemment.
1. Sélectionnez **[!UICONTROL Add > Container]** dans le coin supérieur droit de la section **[!UICONTROL Definition]**.
1. Sélectionnez l’opérateur de division (÷) entre les deux conteneurs.
1. Faites glisser le segment précédemment créé, intitulé « Accès avec une activité de [!UICONTROL Auto-Target] spécifique », dans ce tutoriel pour cette activité de [!DNL Auto-Target] spécifique.
1. Faites glisser la mesure **[!UICONTROL Visits]** dans le conteneur de segments.
1. Cliquez sur **[!UICONTROL Save]**.

>[!TIP]
>
> Vous pouvez également créer cette mesure à l’aide de la [fonctionnalité de mesure calculée rapide](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=fr).

La définition complète de la mesure calculée s’affiche ici.

![Figure9.png](assets/Figure9.png)

*Figure 7 : définition de la mesure de taux de conversion du modèle corrigée de la visite et corrigée de l’attribution. (Notez que cette mesure dépend de votre mesure d’objectif et de votre activité. En d’autres termes, cette définition de mesure n’est pas réutilisable dans toutes les activités.)*

>[!IMPORTANT]
>
>La mesure de taux d’[!UICONTROL Conversion] du panneau A4T n’est pas liée à l’événement de conversion ou à la mesure de normalisation dans le tableau . Lorsque vous apportez les modifications suggérées dans ce tutoriel, le taux de [!UICONTROL Conversion] ne s’adapte pas automatiquement aux modifications. Par conséquent, si vous apportez la modification à l’attribution de l’événement de conversion ou à la mesure de normalisation (ou les deux), vous devez vous en souvenir comme d’une dernière étape pour modifier également le taux de [!UICONTROL Conversion], comme illustré ci-dessus.

## Résumé : Exemple de panneau de [!DNL Analysis Workspace] final pour les rapports [!UICONTROL Auto-Target]

En combinant toutes les étapes ci-dessus dans un seul panneau, la figure ci-dessous présente une vue complète du rapport recommandé pour les activités A4T [!UICONTROL Auto-Target]. Ce rapport est identique à celui utilisé par les modèles ML [!DNL Target] pour optimiser votre mesure d’objectif. Le rapport intègre toutes les nuances et recommandations abordées dans ce tutoriel. Ce rapport est également le plus proche des méthodes de comptage utilisées dans les activités de [!DNL Target] traditionnelles axées sur les rapports [!UICONTROL Auto-Target].

Cliquez pour développer l’image.

![Rapport A4T final dans [!DNL Analysis Workspace]](assets/Figure10.png "Rapport A4T dans Analysis Workspace"){width="600" zoomable="yes"}

*Figure 10 : rapport de [!UICONTROL Auto-Target] A4T final dans [!DNL Adobe Analytics] [!DNL Workspace], qui combine tous les ajustements des définitions de mesures décrits dans les sections précédentes de ce tutoriel.*
