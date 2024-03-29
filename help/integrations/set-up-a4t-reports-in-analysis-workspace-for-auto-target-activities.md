---
title: Configuration des rapports A4T dans [!DNL Analysis Workspace] pour [!DNL Auto-Target] Activités
description: Comment configurer des rapports A4T dans [!DNL Analysis Workspace] pour obtenir les résultats attendus lors de l’exécution [!UICONTROL Ciblage automatique] activités ?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium newtab=true" tooltip="Découvrez les fonctionnalités incluses dans Target Premium."
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
source-wordcount: '2658'
ht-degree: 1%

---

# Configuration des rapports A4T dans [!DNL Analysis Workspace] pour [!DNL Auto-Target] activités

>[!IMPORTANT]
>
>Pour [!UICONTROL Ciblage automatique] activités, vous devez archiver les rapports dans [!DNL Analytics Workspace] et créez manuellement un panneau A4T.

La variable [!UICONTROL Analytics pour Target] Intégration (A4T) pour [!DNL Auto-Target] Les activités utilisent la variable [!DNL Adobe Target] algorithmes d’apprentissage automatique d’ensemble (ML) permettant de choisir la meilleure expérience pour chaque visiteur en fonction de son profil, de son comportement et de son contexte, tout en utilisant une [!DNL Adobe Analytics] mesure d’objectif.

Bien que des fonctionnalités d’analyse complètes soient disponibles dans [!DNL Adobe Analytics] [!DNL Analysis Workspace], quelques modifications apportées à la valeur par défaut **[!UICONTROL Analytics pour Target]** doivent être correctement interprétés. [!DNL Auto-Target] activités, en raison des différences entre les activités d’expérimentation (manuelle) [!UICONTROL Test A/B] et [!UICONTROL Affectation automatique]) et des activités de personnalisation ([!UICONTROL [!UICONTROL Ciblage automatique]]).

Ce tutoriel décrit les modifications recommandées pour l’analyse [!UICONTROL Ciblage automatique] activités dans [!DNL Analysis Workspace], qui reposent sur les concepts clés suivants :

* La variable **[!UICONTROL Comparaison du contrôle et du ciblage]** peut être utilisée pour distinguer les [!UICONTROL Contrôle] expériences par rapport à celles diffusées par la fonction [!UICONTROL Ciblage automatique] algorithme ML d’ensemble.
* Les visites doivent être utilisées comme mesure de normalisation lors de l’affichage des ventilations de performances au niveau de l’expérience. En outre, [La méthodologie de comptage par défaut d’Adobe Analytics peut inclure les visites pour lesquelles l’utilisateur ne voit pas réellement le contenu de l’activité.](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html#metrics){target=_blank}, mais ce comportement par défaut peut être modifié à l’aide d’un segment à portée appropriée (détails ci-dessous).
* L’attribution à portée de recherche en amont des visites, également appelée &quot;intervalle de recherche en amont des visites&quot; sur le modèle d’attribution prescrit, est utilisée par la fonction [!DNL Adobe Target] Les modèles ML pendant leurs phases de formation, et le même modèle d’attribution (autre que celui par défaut), doivent être utilisés lors de la ventilation de la mesure d’objectif.

## Création d’A4T pour [!UICONTROL Ciblage automatique] dans [!DNL Analysis Workspace]

Pour créer A4T pour [!UICONTROL Ciblage automatique] , commencez par la variable **[!UICONTROL Analytics pour Target]** dans [!DNL Analysis Workspace], comme illustré ci-dessous, ou commencez par un tableau à structure libre. Effectuez ensuite les sélections suivantes :

1. **[!UICONTROL Expérience de contrôle]**: vous pouvez choisir n’importe quelle expérience, mais vous remplacerez ce choix ultérieurement. Notez que pour [!UICONTROL Ciblage automatique] activités, l’expérience de contrôle est en fait une stratégie de contrôle, qui consiste à : a) diffuser de manière aléatoire parmi toutes les expériences, ou b) diffuser une seule expérience (ce choix est effectué au moment de la création de l’activité dans [!DNL Adobe Target]). Même si vous avez choisi (b), votre [!UICONTROL Ciblage automatique] activité désignait une expérience spécifique comme contrôle. Suivez toujours l’approche décrite dans ce tutoriel pour analyser A4T pour [!UICONTROL Ciblage automatique] activités.
2. **[!UICONTROL Mesure de normalisation]**: sélectionnez [!UICONTROL Visites].
3. **[!UICONTROL Mesures de succès]**: bien que vous puissiez sélectionner une mesure pour le rapport, vous devriez généralement afficher les rapports sur la même mesure que celle qui a été choisie pour l’optimisation lors de la création de l’activité dans [!DNL Target].

   ![[!UICONTROL Analytics pour Target] configuration du panneau pour [!UICONTROL Ciblage automatique] activités.](assets/Figure1.png)

   *Figure 1 : [!UICONTROL Analytics pour Target] configuration du panneau pour [!UICONTROL Ciblage automatique] activités.*

>[!TIP]
>
>Pour configurer votre [!UICONTROL Analytics pour Target] pour [!UICONTROL Ciblage automatique] activités, choisissez n’importe quelle expérience de contrôle, choisissez [!UICONTROL Visites] comme mesure de normalisation, et choisissez la même mesure d’objectif que celle qui a été choisie pour l’optimisation lors de la [!DNL Target] création de l’activité.

## Utilisez la variable [!UICONTROL Contrôles et cibles] dimension à comparer [!DNL Target] modèle ML d’ensemble à votre contrôle

Le panneau A4T par défaut est conçu pour les écrans classiques (manuels). [!UICONTROL Test A/B] ou [!UICONTROL Affectation automatique] activités dont l’objectif est de comparer les performances d’expériences individuelles à l’expérience de contrôle. Dans [!UICONTROL Ciblage automatique] toutefois, la première comparaison d’ordre doit être entre les activités de contrôle *stratégie* et le *stratégie*. En d’autres termes, déterminer l’effet élévateur de la performance globale de la variable [!UICONTROL Ciblage automatique] modèle ML d’ensemble sur la stratégie de contrôle.

Pour effectuer cette comparaison, utilisez le **[!UICONTROL Comparaison du contrôle et du ciblage (Analytics pour Target)]** dimension. Effectuez un glisser-déposer pour remplacer le **[!UICONTROL Expériences Target]** dans le rapport A4T par défaut.

Notez que ce remplacement invalide la valeur par défaut [!UICONTROL Effet élévateur et degré de confiance] calculs sur le panneau A4T. Pour éviter toute confusion, vous pouvez supprimer ces mesures du panneau par défaut, en laissant le rapport suivant :

![[!UICONTROL Expériences par conversion d’activité] dans [!DNL Analysis Workspace]](assets/Figure2.png)

*Figure 2 : Rapport de référence recommandé pour [!DNL Auto-Target] activités. Ce rapport a été configuré pour comparer le trafic ciblé (traité par le modèle ML d’ensemble) à votre trafic de contrôle.*

>[!NOTE]
>
>Actuellement, [!UICONTROL Effet élévateur et degré de confiance] les nombres ne sont pas disponibles pour [!UICONTROL Comparaison du contrôle et du ciblage] dimensions des rapports A4T pour [!UICONTROL Ciblage automatique]. Jusqu’à ce que la prise en charge soit ajoutée, [!UICONTROL Effet élévateur et degré de confiance] peut être calculé manuellement en téléchargeant la variable [calculateur de confiance](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx).

## Ajout de ventilations de mesures au niveau de l’expérience

Pour mieux comprendre les performances du modèle ML d’ensemble, vous pouvez examiner les ventilations au niveau de l’expérience de la variable **[!UICONTROL Comparaison du contrôle et du ciblage]** dimension. Dans [!DNL Analysis Workspace], faites glisser le **[!UICONTROL Expériences Target]** sur votre rapport, puis ventilez séparément chacune des dimensions de contrôle et des dimensions ciblées.

![[!UICONTROL Expériences par conversion d’activité] dans [!DNL Analysis Workspace]](assets/Figure3.png)

*Figure 3 : Ventilation de la dimension ciblée par expériences Target*

Un exemple du rapport obtenu est présenté ici.

![[!UICONTROL Expériences par conversion d’activité] dans [!DNL Analysis Workspace]](assets/Figure4.png)

*Figure 4 : Une norme [!UICONTROL Ciblage automatique] rapport avec des ventilations au niveau de l’expérience. Notez que votre mesure d’objectif peut être différente et que votre stratégie de contrôle peut comporter une seule expérience.*

>[!TIP]
>
>Dans [!DNL Analysis Workspace], cliquez sur l’icône d’engrenage pour masquer les pourcentages dans la variable [!UICONTROL Taux de conversion] pour vous aider à vous concentrer sur les taux de conversion de l’expérience. Les taux de conversion seront alors formatés sous forme de décimales, mais interprétés comme des pourcentages en conséquence.

## Pourquoi &quot;[!UICONTROL Visites]&quot; est la mesure de normalisation correcte pour [!UICONTROL Ciblage automatique] activités

Lors de l’analyse d’une [!UICONTROL Ciblage automatique] activité, toujours choisir [!UICONTROL Visites] comme mesure de normalisation par défaut. [!UICONTROL Ciblage automatique] la personnalisation sélectionne une expérience pour un visiteur une fois par visite (formellement, une fois par visite). [!DNL Target] session), ce qui signifie que l’expérience présentée à un visiteur peut changer à chaque visite. Ainsi, si vous utilisez [!UICONTROL Visiteurs uniques] comme mesure de normalisation, le fait qu’un utilisateur unique puisse voir plusieurs expériences (au cours de différentes visites) peut entraîner des taux de conversion déroutants.

Un exemple simple illustre ce point : imaginez un scénario dans lequel deux visiteurs entrent dans une campagne qui ne comporte que deux expériences. Le premier visiteur effectue deux visites. Elles sont affectées à l’expérience A lors de la première visite, mais à l’expérience B lors de la seconde visite (en raison de la modification de leur état de profil lors de cette deuxième visite). Après la deuxième visite, le visiteur effectue une conversion en passant une commande. La conversion est attribuée à l’expérience la plus récemment affichée (expérience B). Le deuxième visiteur se rend également deux fois sur le site et affiche l’expérience B à chaque fois, mais ne procède jamais à une conversion.

Comparons les rapports au niveau des visiteurs et des visites :

| Expérience | Visiteurs uniques | Visites | Conversions | Taux de conversion normalisé par les visiteurs | Taux de conversion normalisé pour les visites |
| --- | --- | --- | --- | --- | --- |
| Une | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50 % | 33.3% |
| Totaux | 2 | 4 | 1 | 50 % | 25 % |

*Tableau 1 : Exemple de comparaison des rapports normalisés en fonction des visiteurs et des visites pour un scénario dans lequel les décisions sont liées à une visite (et non aux visiteurs, comme avec les tests A/B standard). Dans ce scénario, les mesures normalisées par les visiteurs sont déroutantes.*

Comme le montre le tableau, les nombres au niveau du visiteur présentent une incongruité évidente. Bien qu’il existe deux visiteurs uniques au total, il ne s’agit pas de la somme des visiteurs uniques individuels pour chaque expérience. Bien que le taux de conversion au niveau du visiteur ne soit pas nécessairement incorrect, lorsqu’on compare des expériences individuelles, les taux de conversion au niveau du visiteur ont sans doute beaucoup plus de sens. Officiellement, l’unité d’analyse (&quot;visites&quot;) est identique à l’unité d’attractivité de décision, ce qui signifie que les ventilations au niveau de l’expérience de mesures peuvent être ajoutées et comparées.

## Filtre pour les visites réelles de l’activité

La variable [!DNL Adobe Analytics] méthodologie de comptage par défaut pour les visites d’un [!DNL Target] l’activité peut inclure des visites au cours desquelles l’utilisateur n’a pas interagi avec la variable [!DNL Target] activité. Ceci est dû à la façon dont [!DNL Target] les affectations d’activité sont conservées dans la variable [!DNL Analytics] contexte du visiteur. Par conséquent, le nombre de visites au [!DNL Target] l’activité peut parfois être exagérée, ce qui entraîne une dépression des taux de conversion.

Si vous préférez créer un rapport sur les visites au cours desquelles l’utilisateur a réellement interagi avec la variable [!UICONTROL Ciblage automatique] (soit par l’entrée de l’activité, un événement d’affichage, de visite ou une conversion), vous pouvez :

1. Créez un segment spécifique qui comprend les accès issus de la [!DNL Target] activité en question, puis
1. Filtrez les [!UICONTROL Visites] à l’aide de ce segment.

**Pour créer le segment :**

1. Sélectionnez la variable **[!UICONTROL Composants > Créer un segment]** dans le [!DNL Analysis Workspace] barre d’outils.
2. Spécifiez un **[!UICONTROL Titre]** pour votre segment. Dans l’exemple ci-dessous, le segment est nommé [!DNL "Hit with specific Auto-Target activity"].
3. Faites glisser le **[!UICONTROL Activités Target]** dimension au segment **[!UICONTROL Définition]** .
4. Utilisez la variable **[!UICONTROL est égal à]** de l’opérateur.
5. Recherchez votre [!DNL Target] activité.
6. Cliquez sur l’icône d’engrenage, puis sélectionnez **[!UICONTROL Modèle d’attribution > Instance]** comme illustré dans la figure ci-dessous.
7. Cliquez sur **[!UICONTROL Enregistrer]**.

![Segment dans [!DNL Analysis Workspace]](assets/Figure5.png)

*Figure 5 : Utilisation d’un segment tel que celui illustré ici pour filtrer la variable [!UICONTROL Visites] dans votre A4T pour [!UICONTROL Ciblage automatique] rapport*

Une fois le segment créé, utilisez-le pour filtrer la variable [!UICONTROL Visites] , donc la variable [!UICONTROL Visites] La mesure inclut uniquement les visites au cours desquelles l’utilisateur a interagi avec la variable [!DNL Target] activité.

**Pour filtrer [!UICONTROL Visites] à l’aide de ce segment :**

1. Faites glisser le segment nouvellement créé à partir de la barre d’outils des composants, puis survolez la base de la **[!UICONTROL Visites]** libellé de mesure jusqu’à ce qu’un bleu **[!UICONTROL Filtrer par]** s’affiche.
2. Relâchez le segment. Le filtre est appliqué à cette mesure.

Le panneau final s’affiche comme suit :

![[!UICONTROL Expériences par conversion d’activité] dans [!DNL Analysis Workspace]](assets/Figure6.png)

*Figure 6 : Panneau Création de rapports avec le segment &quot;Accès avec une activité de ciblage automatique spécifique&quot; appliqué au [!UICONTROL Visites] mesure. Ce segment garantit que seules les visites au cours desquelles un utilisateur a réellement interagi avec la variable [!DNL Target] Les activités en question sont incluses dans le rapport.*

## Assurez-vous que la mesure et l’attribution de l’objectif sont alignées sur votre critère d’optimisation.

L’intégration A4T permet à la variable [!UICONTROL Ciblage automatique] Modèle ML à utiliser *formé* en utilisant les mêmes données d’événement de conversion que [!DNL Adobe Analytics] utilise pour *génération de rapports de performances*. Cependant, certaines hypothèses doivent être utilisées pour interpréter ces données lors de la formation des modèles ML, qui diffèrent des hypothèses par défaut faites lors de la phase de création de rapports dans [!DNL Adobe Analytics].

Plus précisément, la variable [!DNL Adobe Target] Les modèles ML utilisent un modèle d’attribution à portée de visite. En d’autres termes, les modèles ML supposent qu’une conversion doit avoir lieu au cours de la même visite comme affichage du contenu de l’activité pour que la conversion soit &quot;attribuée&quot; à la décision prise par le modèle ML. Cette opération est requise pour [!DNL Target] assurer une formation rapide de ses modèles; [!DNL Target] ne peut pas attendre jusqu’à 30 jours pour une conversion (la fenêtre d’attribution par défaut des rapports dans [!DNL Adobe Analytics]) avant de l’inclure dans les données d’entraînement de ses modèles.

Ainsi, la différence entre l’attribution utilisée par la variable [!DNL Target] les modèles (pendant la formation) par rapport à l’attribution par défaut utilisée dans l’interrogation des données (pendant la génération des rapports) peuvent entraîner des incohérences. Il peut même sembler que les modèles ML sont peu performants, alors qu&#39;en fait le problème réside dans l&#39;attribution.

>[!TIP]
>
>Si les modèles ML optimisent une mesure qui est attribuée différemment des mesures que vous affichez dans un rapport, les modèles peuvent ne pas fonctionner comme prévu. Pour éviter cela, assurez-vous que les mesures d’objectif de votre rapport utilisent la même définition de mesure et la même attribution utilisées par [!DNL Target] Modèles ML.

La définition de mesure exacte et les paramètres d’attribution dépendent de [critère d’optimisation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank} vous avez spécifié lors de la création de l’activité.

### Conversions définies par Target, ou [!DNL Analytics] mesures avec *Maximiser la valeur de mesure par visite*

Lorsque la mesure est une [!DNL Target] une conversion ou une [!DNL Analytics] mesures avec **Maximiser la valeur de mesure par visite**, la définition de mesure d’objectif permet à plusieurs événements de conversion de se produire au cours d’une même visite.

Pour afficher les mesures d’objectif qui ont la même méthodologie d’attribution utilisée par la variable [!DNL Target] Modèles ML, procédez comme suit :

1. Passez la souris sur l’icône d’engrenage de la mesure d’objectif :

   ![gearicon.png](assets/gearicon.png)

1. Dans le menu qui s’affiche, faites défiler jusqu’à **[!UICONTROL Paramètres des données]**.
1. Sélectionner **[!UICONTROL Utilisation d’un modèle d’attribution différent du modèle par défaut]** (s’il n’est pas déjà sélectionné).

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Cliquez sur **[!UICONTROL Modifier]**.
1. Sélectionner **[!UICONTROL Modèle]**: **[!UICONTROL Participation]**, et **[!UICONTROL Intervalle de recherche en amont]**: **[!UICONTROL Visite]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. Cliquez sur **[!UICONTROL Appliquer]**.

Ces étapes garantissent que votre rapport attribue la mesure d’objectif à l’affichage de l’expérience, si l’événement de mesure d’objectif s’est produit. *à tout moment* (&quot;participation&quot;) au cours de la même visite que celle où une expérience a été affichée.

### [!DNL Analytics] mesures avec *Taux de conversion de visites uniques*

**Définition de la visite avec un segment de mesure positif**

Dans le scénario où vous avez sélectionné *Maximiser le taux de conversion des visites uniques* comme critère d’optimisation, la définition correcte du taux de conversion correspond à la fraction des visites pour lesquelles la valeur de mesure est positive. Pour ce faire, vous pouvez créer un segment en filtrant les visites par rapport aux visites avec une valeur positive de la mesure, puis en filtrant la mesure Visites.

1. Comme avant, sélectionnez la variable **[!UICONTROL Composants > Créer un segment]** dans le [!DNL Analysis Workspace] barre d’outils.
2. Spécifiez un **[!UICONTROL Titre]** pour votre segment.

   Dans l’exemple ci-dessous, le segment est nommé [!DNL "Visits with an order"].

3. Faites glisser la mesure de base que vous avez utilisée dans votre objectif d’optimisation dans le segment.

   Dans l’exemple ci-dessous, nous utilisons la méthode **commandes** afin que le taux de conversion mesure la fraction des visites pour lesquelles une commande est enregistrée.

4. En haut à gauche du conteneur de définitions de segment, sélectionnez **[!UICONTROL Inclure]** **Visite**.
5. Utilisez la variable **[!UICONTROL est supérieur à]** et définissez la valeur sur 0.

   Si vous définissez la valeur sur 0, cela signifie que ce segment inclut les visites pour lesquelles la mesure des commandes est positive.

6. Cliquez sur **[!UICONTROL Enregistrer]**.

![Figure7.png](assets/Figure7.png)

*Figure 7 : Filtrage de la définition de segment pour les visites avec un ordre positif. Selon la mesure d’optimisation de votre activité, vous devez remplacer les commandes par une mesure appropriée.*

**Appliquez-le aux visites dans la mesure filtrée de l’activité.**

Ce segment peut désormais être utilisé pour filtrer les visites avec un nombre positif de commandes, et lorsqu’un accès a eu lieu pour le [!DNL Auto-Target] activité. La procédure de filtrage d’une mesure est similaire à la procédure précédente. Après avoir appliqué le nouveau segment à la mesure de visite déjà filtrée, le panneau du rapport doit ressembler à la figure 8.

![Figure8.png](assets/Figure8.png)

*Figure 8 : Panneau du rapport présentant la mesure de conversion de visites uniques correcte : nombre de visites au cours desquelles un accès de l’activité a été enregistré, et où la mesure de conversion (commandes dans cet exemple) était non nulle.*

## Étape finale : créez un taux de conversion qui capture la magie ci-dessus.

Avec les modifications apportées à la variable [!UICONTROL Visite] et les mesures d’objectif dans les sections précédentes, la modification finale que vous devez apporter à votre A4T par défaut pour [!DNL Auto-Target] le panneau de création de rapports permet de créer des taux de conversion correspondant au bon ratio (celui de la mesure d’objectif corrigée), par rapport à une mesure &quot;Visites&quot; correctement filtrée.

Pour ce faire, créez une [!UICONTROL Mesure calculée] en procédant comme suit :

1. Sélectionnez la variable **[!UICONTROL Composants > Créer une mesure]** dans le [!DNL Analysis Workspace] barre d’outils.
1. Spécifiez un **[!UICONTROL Titre]** pour votre mesure. Par exemple, &quot;Taux de conversion corrigé des visites pour l’activité XXX&quot;.
1. Sélectionner **[!UICONTROL Format]** = Pourcentage et **[!UICONTROL Nombre de décimales]** = 2.
1. Faites glisser la mesure d’objectif appropriée pour votre activité (par exemple : [!UICONTROL Conversions des activités]) dans la définition et utilisez l’icône d’engrenage sur cette mesure d’objectif pour ajuster le modèle d’attribution à (Participation|Visite), comme décrit précédemment.
1. Sélectionner **[!UICONTROL Ajouter > Conteneur]** en haut à droite de la **[!UICONTROL Définition]** .
1. Sélectionnez l&#39;opérateur de division (÷) entre les deux conteneurs.
1. Faites glisser le segment précédemment créé, nommé &quot;Accès avec des [!UICONTROL Ciblage automatique] &quot;activity&quot; dans ce tutoriel pour ce [!DNL Auto-Target] activité.
1. Faites glisser le **[!UICONTROL Visites]** dans le conteneur de segments.
1. Cliquez sur **[!UICONTROL Enregistrer]**.

>[!TIP]
>
> Vous pouvez également créer cette mesure à l’aide de la variable [fonctionnalité de mesure calculée rapide](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html).

La définition de mesure calculée complète s’affiche ici.

![Figure9.png](assets/Figure9.png)

*Figure 7 : Définition de la mesure de taux de conversion du modèle corrigé des visites et corrigé des attributions. (Notez que cette mesure dépend de votre mesure d’objectif et de votre activité. En d’autres termes, cette définition de mesure n’est pas réutilisable entre les activités.)*

>[!IMPORTANT]
>
>La variable [!UICONTROL Conversion] la mesure de taux du panneau A4T n’est pas liée à l’événement de conversion ou à la mesure de normalisation dans le tableau. Lorsque vous effectuez les modifications suggérées dans ce tutoriel, la variable [!UICONTROL Conversion] Le taux ne s’adapte pas automatiquement aux modifications. Par conséquent, si vous apportez la modification à l’attribution d’événement de conversion ou à la mesure de normalisation (ou les deux), vous devez vous souvenir d’une étape finale pour modifier également la variable [!UICONTROL Conversion] rate, comme illustré ci-dessus.

## Résumé : exemple final [!DNL Analysis Workspace] pour [!UICONTROL Ciblage automatique] rapports

En combinant toutes les étapes ci-dessus dans un seul panneau, la figure ci-dessous présente une vue complète du rapport recommandé pour [!UICONTROL Ciblage automatique] Activités d’A4T. Ce rapport est identique à celui utilisé par la variable [!DNL Target] Modèles ML pour optimiser votre mesure d’objectif. Le rapport intègre toutes les nuances et recommandations abordées dans ce tutoriel. Ce rapport se rapproche également des méthodologies de comptage utilisées dans les [!DNL Target]-reporting piloté [!UICONTROL Ciblage automatique] activités.

Cliquez sur pour développer l’image.

![Rapport final A4T dans [!DNL Analysis Workspace]](assets/Figure10.png "Rapport A4T dans Analysis Workspace"){width="600" zoomable="yes"}

*Figure 10 : Le A4T final [!UICONTROL Ciblage automatique] rapport dans [!DNL Adobe Analytics] [!DNL Workspace], qui combine tous les ajustements aux définitions de mesures décrits dans les sections précédentes de ce tutoriel.*
