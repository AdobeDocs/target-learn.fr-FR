---
title: Comment configurer des rapports A4T dans [!DNL Analysis Workspace] pour [!DNL Auto-Target] Activités
description: Comment configurer des rapports A4T dans  [!DNL Analysis Workspace] pour obtenir les résultats escomptés lors de l’exécution d’activités [!UICONTROL Auto-Target] ?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=fr#premium newtab=true" tooltip="Découvrez les fonctionnalités incluses dans Target Premium."
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

# Configuration de rapports A4T dans [!DNL Analysis Workspace] pour les activités [!DNL Auto-Target]

>[!IMPORTANT]
>
>Pour les activités [!UICONTROL Auto-Target], vous devez vérifier les rapports dans [!DNL Analytics Workspace] et créer manuellement un panneau A4T.

L’intégration [!UICONTROL Analytics for Target] (A4T) pour les activités [!DNL Auto-Target] utilise les algorithmes d’apprentissage automatique d’ensemble [!DNL Adobe Target] pour choisir la meilleure expérience pour chaque visiteur en fonction de son profil, de son comportement et de son contexte, tout en utilisant une mesure d’objectif [!DNL Adobe Analytics].

Bien que de riches fonctionnalités d&#39;analyse soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace], quelques modifications du panneau par défaut **[!UICONTROL Analytics for Target]** sont nécessaires pour interpréter correctement les activités [!DNL Auto-Target], en raison de différences entre les activités d&#39;expérimentation (manuelles [!UICONTROL A/B Test] et [!UICONTROL Auto-Allocate]) et les activités de personnalisation ([!UICONTROL [!UICONTROL Auto-Target]]).

Ce tutoriel décrit les modifications recommandées pour l’analyse des activités [!UICONTROL Auto-Target] dans [!DNL Analysis Workspace], basées sur les concepts clés suivants :

* La dimension **[!UICONTROL Control vs Targeted]** peut être utilisée pour faire la distinction entre les expériences [!UICONTROL Control] et celles diffusées par l’algorithme ML d’ensemble [!UICONTROL Auto-Target].
* Les visites doivent être utilisées comme mesure de normalisation lors de l’affichage des ventilations de performances au niveau de l’expérience. En outre, la méthodologie de comptage par défaut d’ [ Adobe Analytics peut inclure des visites pour lesquelles l’utilisateur ne voit pas réellement le contenu de l’activité ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=fr#metrics){target=_blank}, mais ce comportement par défaut peut être modifié à l’aide d’un segment de portée appropriée (détails ci-dessous).
* L’attribution étendue de la recherche en amont des visites, également appelée &quot;intervalle de recherche en amont des visites&quot; sur le modèle d’attribution prescrit, est utilisée par les modèles ML [!DNL Adobe Target] pendant leurs phases de formation, et le même modèle d’attribution (autre que celui par défaut) doit être utilisé lors de la ventilation de la mesure d’objectif.

## Créez le panneau A4T pour [!UICONTROL Auto-Target] dans [!DNL Analysis Workspace]

Pour créer un rapport A4T pour [!UICONTROL Auto-Target], commencez par le panneau **[!UICONTROL Analytics for Target]** dans [!DNL Analysis Workspace], comme illustré ci-dessous, ou commencez par un tableau à structure libre. Effectuez ensuite les sélections suivantes :

1. **[!UICONTROL Control Experience]** : vous pouvez choisir n’importe quelle expérience ; vous remplacerez toutefois ce choix ultérieurement. Notez que pour les activités [!UICONTROL Auto-Target], l’expérience de contrôle est en fait une stratégie de contrôle, qui consiste soit à a) diffuser de manière aléatoire parmi toutes les expériences, soit b) diffuser une seule expérience (ce choix est effectué au moment de la création de l’activité dans [!DNL Adobe Target]). Même si vous avez choisi (b), votre activité [!UICONTROL Auto-Target] a désigné une expérience spécifique comme contrôle. Suivez toujours l’approche décrite dans ce tutoriel pour analyser A4T pour les activités [!UICONTROL Auto-Target].
2. **[!UICONTROL Normalizing Metric]** : sélectionnez [!UICONTROL Visits].
3. **[!UICONTROL Success Metrics]** : bien que vous puissiez sélectionner n’importe quelle mesure sur laquelle créer un rapport, vous devez généralement afficher les rapports sur la même mesure que celle choisie pour l’optimisation lors de la création de l’activité dans [!DNL Target].

   ![[!UICONTROL Analytics for Target] configuration du panneau pour les activités [!UICONTROL Auto-Target].](assets/Figure1.png)

   *Figure 1 : [!UICONTROL Analytics for Target] configuration du panneau pour les activités [!UICONTROL Auto-Target].*

>[!TIP]
>
>Pour configurer votre panneau [!UICONTROL Analytics for Target] pour les activités [!UICONTROL Auto-Target], choisissez n’importe quelle expérience de contrôle, choisissez [!UICONTROL Visits] comme mesure de normalisation et choisissez la même mesure d’objectif que celle choisie pour l’optimisation lors de la création de l’activité [!DNL Target].

## Utilisez la dimension [!UICONTROL Control vs.Targeted] pour comparer le modèle ML d’ensemble [!DNL Target] à votre contrôle.

Le panneau A4T par défaut est conçu pour les activités classiques (manuelles) [!UICONTROL A/B Test] ou [!UICONTROL Auto-Allocate] dont l’objectif est de comparer les performances des expériences individuelles à l’expérience de contrôle. Dans les activités [!UICONTROL Auto-Target], cependant, la première comparaison de commande doit être entre le contrôle *stratégie* et la *stratégie* ciblée. En d’autres termes, déterminer l’effet élévateur des performances globales du modèle ML d’ensemble [!UICONTROL Auto-Target] par rapport à la stratégie de contrôle.

Pour effectuer cette comparaison, utilisez la dimension **[!UICONTROL Control vs Targeted (Analytics for Target)]**. Effectuez un glisser-déposer pour remplacer la dimension **[!UICONTROL Target Experiences]** dans le rapport A4T par défaut.

Notez que ce remplacement invalide les calculs [!UICONTROL Lift and Confidence] par défaut sur le panneau A4T. Pour éviter toute confusion, vous pouvez supprimer ces mesures du panneau par défaut, en laissant le rapport suivant :

![[!UICONTROL Experiences by Activity Conversions] panel dans [!DNL Analysis Workspace]](assets/Figure2.png)

*Figure 2 : Rapport de base recommandé pour les activités [!DNL Auto-Target]. Ce rapport a été configuré pour comparer le trafic ciblé (traité par le modèle ML d’ensemble) à votre trafic de contrôle.*

>[!NOTE]
>
>Actuellement, les nombres [!UICONTROL Lift and Confidence] ne sont pas disponibles pour les dimensions [!UICONTROL Control vs Targeted] des rapports A4T pour [!UICONTROL Auto-Target]. Tant que la prise en charge n&#39;est pas ajoutée, [!UICONTROL Lift and Confidence] peut être calculé manuellement en téléchargeant le [calculateur de confiance](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=fr).

## Ajout de ventilations de mesures au niveau de l’expérience

Pour mieux comprendre les performances du modèle ML d’ensemble, vous pouvez examiner les ventilations au niveau de l’expérience de la dimension **[!UICONTROL Control vs Targeted]**. Dans [!DNL Analysis Workspace], faites glisser la dimension **[!UICONTROL Target Experiences]** sur votre rapport, puis ventilez séparément chaque dimension de contrôle et dimension ciblée.

![[!UICONTROL Experiences by Activity Conversions] panel dans [!DNL Analysis Workspace]](assets/Figure3.png)

*Figure 3 : Ventilation de la dimension ciblée par expériences Target*

Un exemple du rapport obtenu est présenté ici.

![[!UICONTROL Experiences by Activity Conversions] panel dans [!DNL Analysis Workspace]](assets/Figure4.png)

*Figure 4 : Rapport [!UICONTROL Auto-Target] standard avec ventilations au niveau de l’expérience. Notez que la mesure de votre objectif peut être différente et que votre stratégie de contrôle peut comporter une seule expérience.*

>[!TIP]
>
>Dans [!DNL Analysis Workspace], cliquez sur l’icône représentant un engrenage pour masquer les pourcentages dans la colonne [!UICONTROL Conversion Rate] afin de vous concentrer sur les taux de conversion de l’expérience. Les taux de conversion seront alors formatés sous forme de décimales, mais interprétés comme des pourcentages en conséquence.

## Pourquoi &quot;[!UICONTROL Visits]&quot; est la mesure de normalisation correcte pour les activités [!UICONTROL Auto-Target]

Lors de l’analyse d’une activité [!UICONTROL Auto-Target], choisissez toujours [!UICONTROL Visits] comme mesure de normalisation par défaut. La personnalisation [!UICONTROL Auto-Target] sélectionne une expérience pour un visiteur une fois par visite (officiellement, une fois par session [!DNL Target]), ce qui signifie que l’expérience présentée à un visiteur peut changer à chaque visite. Par conséquent, si vous utilisez [!UICONTROL Unique Visitors] comme mesure de normalisation, le fait qu’un utilisateur unique puisse voir plusieurs expériences (au cours de différentes visites) peut entraîner des taux de conversion déroutants.

Un exemple simple illustre ce point : imaginez un scénario dans lequel deux visiteurs entrent dans une campagne qui ne comporte que deux expériences. Le premier visiteur effectue deux visites. Elles sont affectées à l’expérience A lors de la première visite, mais à l’expérience B lors de la seconde visite (en raison de la modification de leur état de profil lors de cette deuxième visite). Après la deuxième visite, le visiteur effectue une conversion en passant une commande. La conversion est attribuée à l’expérience la plus récemment affichée (expérience B). Le deuxième visiteur se rend également deux fois sur le site et affiche l’expérience B à chaque fois, mais ne procède jamais à une conversion.

Comparons les rapports au niveau des visiteurs et des visites :

| Expérience | Visiteurs uniques | Visites | Conversions | Taux de conversion normalisé par les visiteurs | Taux de conversion normalisé pour les visites |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0 % | 0 % |
| B | 2 | 3 | 1 | 50 % | 33,3 % |
| Totaux | 2 | 4 | 1 | 50 % | 25 % |

*Tableau 1 : exemple de comparaison de rapports normalisés en fonction des visiteurs et normalisés en fonction des visites pour un scénario dans lequel les décisions sont liées à une visite (et non aux visiteurs, comme avec les tests A/B standard). Les mesures normalisées par les visiteurs sont déroutantes dans ce scénario.*

Comme le montre le tableau, les nombres au niveau du visiteur présentent une incongruité évidente. Bien qu’il existe deux visiteurs uniques au total, il ne s’agit pas de la somme des visiteurs uniques individuels pour chaque expérience. Bien que le taux de conversion au niveau du visiteur ne soit pas nécessairement incorrect, lorsqu’on compare des expériences individuelles, les taux de conversion au niveau du visiteur ont sans doute beaucoup plus de sens. Officiellement, l’unité d’analyse (&quot;visites&quot;) est identique à l’unité d’attractivité de décision, ce qui signifie que les ventilations au niveau de l’expérience de mesures peuvent être ajoutées et comparées.

## Filtre pour les visites réelles de l’activité

La méthodologie de comptage par défaut de [!DNL Adobe Analytics] pour les visites d’une activité [!DNL Target] peut inclure les visites au cours desquelles l’utilisateur n’a pas interagi avec l’activité [!DNL Target]. Cela est dû à la manière dont les affectations d’activité [!DNL Target] sont conservées dans le contexte du visiteur [!DNL Analytics]. Par conséquent, le nombre de visites de l’activité [!DNL Target] peut parfois être exagéré, ce qui entraîne une dépression des taux de conversion.

Si vous préférez créer un rapport sur les visites au cours desquelles l’utilisateur a réellement interagi avec l’activité [!UICONTROL Auto-Target] (soit par l’entrée de l’activité, un événement d’affichage ou de visite, soit par une conversion), vous pouvez :

1. Créez un segment spécifique qui inclut les accès de l’activité [!DNL Target] en question, puis
1. Filtrez la mesure [!UICONTROL Visits] à l’aide de ce segment.

**Pour créer le segment :**

1. Sélectionnez l’option **[!UICONTROL Components > Create Segment]** dans la barre d’outils [!DNL Analysis Workspace].
2. Spécifiez un **[!UICONTROL Title]** pour votre segment. Dans l’exemple ci-dessous, le segment est nommé [!DNL "Hit with specific Auto-Target activity"].
3. Faites glisser la dimension **[!UICONTROL Target Activities]** vers la section de segment **[!UICONTROL Definition]**.
4. Utilisez l’opérateur **[!UICONTROL equals]** .
5. Recherchez votre activité [!DNL Target] spécifique.
6. Cliquez sur l’icône d’engrenage, puis sélectionnez **[!UICONTROL Attribution model > Instance]** comme illustré dans la figure ci-dessous.
7. Cliquez sur **[!UICONTROL Save]**.

![Segment dans [!DNL Analysis Workspace]](assets/Figure5.png)

*Figure 5 : Utilisation d’un segment tel que celui illustré ici pour filtrer la mesure [!UICONTROL Visits] dans votre rapport A4T pour [!UICONTROL Auto-Target]*

Une fois le segment créé, utilisez-le pour filtrer la mesure [!UICONTROL Visits]. Par conséquent, la mesure [!UICONTROL Visits] n’inclut que les visites où l’utilisateur a interagi avec l’activité [!DNL Target].

**Pour filtrer [!UICONTROL Visits] à l’aide de ce segment :**

1. Faites glisser le segment nouvellement créé à partir de la barre d’outils des composants et survolez la base de l’étiquette de mesure **[!UICONTROL Visits]** jusqu’à ce qu’une invite bleue **[!UICONTROL Filter by]** s’affiche.
2. Relâchez le segment. Le filtre est appliqué à cette mesure.

Le panneau final s’affiche comme suit :

![[!UICONTROL Experiences by Activity Conversions] panel dans [!DNL Analysis Workspace]](assets/Figure6.png)

*Figure 6 : Panneau de création de rapports avec le segment &quot;Accès avec activité de ciblage automatique spécifique&quot; appliqué à la mesure [!UICONTROL Visits]. Ce segment garantit que seules les visites au cours desquelles un utilisateur a réellement interagi avec l’activité [!DNL Target] en question sont incluses dans le rapport.*

## Assurez-vous que la mesure et l’attribution de l’objectif sont alignées sur votre critère d’optimisation.

L’intégration A4T permet au modèle [!UICONTROL Auto-Target] ML d’être *entraîné* en utilisant les mêmes données d’événement de conversion que celles utilisées par [!DNL Adobe Analytics] pour *générer des rapports de performances*. Cependant, certaines hypothèses doivent être utilisées pour interpréter ces données lors de la formation des modèles ML, qui diffèrent des hypothèses par défaut faites lors de la phase de création de rapports dans [!DNL Adobe Analytics].

Plus précisément, les modèles ML [!DNL Adobe Target] utilisent un modèle d’attribution à portée de visite. En d’autres termes, les modèles ML supposent qu’une conversion doit avoir lieu au cours de la même visite comme affichage du contenu de l’activité pour que la conversion soit &quot;attribuée&quot; à la décision prise par le modèle ML. Cela est nécessaire pour [!DNL Target] afin de garantir une formation opportune de ses modèles ; [!DNL Target] ne peut pas attendre jusqu’à 30 jours pour une conversion (la fenêtre d’attribution par défaut pour les rapports dans [!DNL Adobe Analytics]) avant de l’inclure dans les données d’entraînement de ses modèles.

Par conséquent, la différence entre l’attribution utilisée par les modèles [!DNL Target] (pendant la formation) et l’attribution par défaut utilisée dans l’interrogation des données (pendant la génération du rapport) peut entraîner des incohérences. Il peut même sembler que les modèles ML sont peu performants, alors qu&#39;en fait le problème réside dans l&#39;attribution.

>[!TIP]
>
>Si les modèles ML optimisent une mesure qui est attribuée différemment des mesures que vous affichez dans un rapport, les modèles peuvent ne pas fonctionner comme prévu. Pour éviter cela, assurez-vous que les mesures d’objectif de votre rapport utilisent la même définition de mesure et la même attribution utilisées par les modèles ML [!DNL Target].

La définition exacte des mesures et les paramètres d’attribution dépendent du [critère d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=fr#supported){target=_blank} que vous avez spécifié lors de la création de l’activité.

### Conversions définies par Target ou [!DNL Analytics] mesures avec *Maximiser la valeur de mesure par visite*

Lorsque la mesure est une conversion [!DNL Target] ou une mesure [!DNL Analytics] avec **Maximiser la valeur de mesure par visite**, la définition de la mesure d’objectif permet à plusieurs événements de conversion de se produire au cours d’une même visite.

Pour afficher les mesures d’objectif qui ont la même méthodologie d’attribution utilisée par les modèles ML [!DNL Target], procédez comme suit :

1. Passez la souris sur l’icône d’engrenage de la mesure d’objectif :

   ![gearicon.png](assets/gearicon.png)

1. Dans le menu qui s’affiche, faites défiler l’écran jusqu’à **[!UICONTROL Data settings]**.
1. Sélectionnez **[!UICONTROL Use non-default  attribution model]** (s’il n’est pas déjà sélectionné).

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Cliquez sur **[!UICONTROL Edit]**.
1. Sélectionnez **[!UICONTROL Model]** : **[!UICONTROL Participation]** et **[!UICONTROL Lookback window]** : **[!UICONTROL Visit]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. Cliquez sur **[!UICONTROL Apply]**.

Ces étapes garantissent que votre rapport attribue la mesure d’objectif à l’affichage de l’expérience, si l’événement de mesure d’objectif s’est produit *à tout moment* (&quot;participation&quot;) au cours de la même visite qu’une expérience a été affichée.

### [!DNL Analytics] mesures avec *taux de conversion de visites uniques*

**Définir la visite avec un segment de mesure positif**

Dans le scénario où vous avez sélectionné *Maximiser le taux de conversion des visites uniques* comme critère d’optimisation, la définition correcte du taux de conversion est la fraction des visites pour lesquelles la valeur de mesure est positive. Pour ce faire, vous pouvez créer un segment en filtrant les visites par rapport aux visites avec une valeur positive de la mesure, puis en filtrant la mesure Visites.

1. Comme auparavant, sélectionnez l’option **[!UICONTROL Components > Create Segment]** dans la barre d’outils [!DNL Analysis Workspace].
2. Spécifiez un **[!UICONTROL Title]** pour votre segment.

   Dans l’exemple ci-dessous, le segment est nommé [!DNL "Visits with an order"].

3. Faites glisser la mesure de base que vous avez utilisée dans votre objectif d’optimisation dans le segment.

   Dans l’exemple ci-dessous, nous utilisons la mesure **commandes** afin que le taux de conversion mesure la fraction des visites où une commande est enregistrée.

4. En haut à gauche du conteneur de définitions de segment, sélectionnez **[!UICONTROL Include]** **Visite**.
5. Utilisez l’opérateur **[!UICONTROL is greater than]** et définissez la valeur sur 0.

   Si vous définissez la valeur sur 0, cela signifie que ce segment inclut les visites pour lesquelles la mesure des commandes est positive.

6. Cliquez sur **[!UICONTROL Save]**.

![Figure7.png](assets/Figure7.png)

*Figure 7 : Filtrage de la définition de segment pour les visites avec un ordre positif. Selon la mesure d’optimisation de votre activité, vous devez remplacer les commandes par une mesure appropriée*

**Appliquez cela aux visites dans la mesure filtrée de l’activité**

Ce segment peut désormais être utilisé pour filtrer les visites avec un nombre positif de commandes, et où il y a eu un accès pour l’activité [!DNL Auto-Target]. La procédure de filtrage d’une mesure est similaire à la procédure précédente. Après avoir appliqué le nouveau segment à la mesure de visite déjà filtrée, le panneau du rapport doit ressembler à la figure 8.

![Figure8.png](assets/Figure8.png)

*Figure 8 : Panneau du rapport présentant la mesure de conversion de visite unique correcte : le nombre de visites au cours desquelles un accès de l’activité a été enregistré et où la mesure de conversion (commandes dans cet exemple) était non nulle.*

## Étape finale : créez un taux de conversion qui capture la magie ci-dessus.

Avec les modifications apportées aux mesures [!UICONTROL Visit] et d’objectif dans les sections précédentes, la dernière modification que vous devez apporter à votre panneau de création de rapports A4T par défaut pour [!DNL Auto-Target] est de créer des taux de conversion qui sont le ratio correct, celui de la mesure d’objectif corrigée, à une mesure &quot;Visites&quot; correctement filtrée.

Pour ce faire, créez un [!UICONTROL Calculated Metric] en suivant les étapes suivantes :

1. Sélectionnez l’option **[!UICONTROL Components > Create Metric]** dans la barre d’outils [!DNL Analysis Workspace].
1. Spécifiez un **[!UICONTROL Title]** pour votre mesure. Par exemple, &quot;Taux de conversion corrigé des visites pour l’activité XXX&quot;.
1. Sélectionnez **[!UICONTROL Format]** = Pourcentage et **[!UICONTROL Decimal Places]** = 2.
1. Faites glisser la mesure d’objectif appropriée pour votre activité (par exemple, [!UICONTROL Activity Conversions]) dans la définition et utilisez l’icône en forme d’engrenage sur cette mesure d’objectif pour ajuster le modèle d’attribution à (Participation|Visite), comme décrit précédemment.
1. Sélectionnez **[!UICONTROL Add > Container]** dans le coin supérieur droit de la section **[!UICONTROL Definition]**.
1. Sélectionnez l&#39;opérateur de division (÷) entre les deux conteneurs.
1. Faites glisser le segment précédemment créé, nommé &quot;Accès avec une activité [!UICONTROL Auto-Target] spécifique&quot; dans ce tutoriel pour cette activité [!DNL Auto-Target] spécifique.
1. Faites glisser la mesure **[!UICONTROL Visits]** dans le conteneur de segments.
1. Cliquez sur **[!UICONTROL Save]**.

>[!TIP]
>
> Vous pouvez également créer cette mesure à l’aide de la [fonctionnalité de mesure calculée rapide](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=fr).

La définition de mesure calculée complète s’affiche ici.

![Figure9.png](assets/Figure9.png)

*Figure 7 : Définition de la mesure de taux de conversion de modèle corrigée pour les visites et corrigée pour l’attribution. (Notez que cette mesure dépend de votre mesure d’objectif et de votre activité. En d’autres termes, cette définition de mesure n’est pas réutilisable entre les activités.)*

>[!IMPORTANT]
>
>La mesure de taux [!UICONTROL Conversion] du panneau A4T n’est pas liée à l’événement de conversion ou à la mesure de normalisation dans le tableau. Lorsque vous effectuez les modifications suggérées dans ce tutoriel, le taux [!UICONTROL Conversion] ne s’adapte pas automatiquement aux modifications. Par conséquent, si vous apportez la modification à l’attribution d’événement de conversion ou à la mesure de normalisation (ou les deux), vous devez vous souvenir d’une étape finale pour modifier également le taux [!UICONTROL Conversion], comme illustré ci-dessus.

## Résumé : dernier exemple [!DNL Analysis Workspace] de panneau pour les rapports [!UICONTROL Auto-Target]

En combinant toutes les étapes ci-dessus dans un seul panneau, la figure ci-dessous présente une vue complète du rapport recommandé pour les activités A4T [!UICONTROL Auto-Target]. Ce rapport est identique à celui utilisé par les modèles [!DNL Target] ML pour optimiser la mesure de votre objectif. Le rapport intègre toutes les nuances et recommandations abordées dans ce tutoriel. Ce rapport est également le plus proche des méthodologies de comptage utilisées dans les activités [!UICONTROL Auto-Target] traditionnelles pilotées par des rapports [!DNL Target].

Cliquez sur pour développer l’image.

![Rapport final A4T dans [!DNL Analysis Workspace]](assets/Figure10.png "Rapport A4T dans Analysis Workspace"){width="600" zoomable="yes"}

*Figure 10 : Rapport final A4T [!UICONTROL Auto-Target] dans [!DNL Adobe Analytics] [!DNL Workspace], qui combine tous les ajustements aux définitions de mesures décrits dans les sections précédentes de ce tutoriel.*
