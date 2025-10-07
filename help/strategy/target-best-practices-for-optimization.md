---
title: Bonnes pratiques pour l’optimisation
description: Découvrez les six principes fondamentaux de l’optimisation d’Adobe et comment les appliquer.
solution: Target
role: Leader, Architect, Developer, Admin
feature: Overview
level: Beginner
exl-id: dd29faea-bb67-4128-b261-fa407ba7158c
source-git-commit: d65720ae992a3079462ba59421c3b7a8d4f5ea7b
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%

---

# Bonnes pratiques relatives à l’optimisation avec Adobe Target

Découvrez les six principes fondamentaux de l’optimisation d’Adobe et comment les appliquer.

Quand il s&#39;agit d&#39;établir une forte présence numérique, votre équipe sera confrontée à un certain nombre de défis. En plus de devoir interagir avec des centaines, voire des milliers de clients, vos clients affichent divers comportements et préférences uniques qui changeront au fil du temps. C&#39;est à vous de suivre ces changements, mais aussi de les anticiper et d&#39;exécuter vos stratégies de manière efficace et précise. Il s’agit d’une course contre la concurrence dans un marathon de contenu perpétuel, qui nécessite une itération constante et la meilleure technologie de sa catégorie.

L’optimisation avec Adobe Target constitue une solution à ce défi aux multiples facettes. Elle vous permet d’avoir une présence numérique en constante évolution, pertinente, précieuse et sans friction. L’architecture technique et les canaux dans lesquels vous déployez [!DNL Target] varieront considérablement d’un client à l’autre. Nous avons toutefois établi une liste des bonnes pratiques et des stratégies d’optimisation que chaque équipe peut utiliser pour exploiter toutes les fonctionnalités de cet outil puissant.

## Comprendre l’optimisation

L’optimisation est définie comme « l’action consistant à utiliser au mieux ou le plus efficacement possible une situation ou une ressource ». C’est le moyen le plus efficace de vous assurer que vous disposez de données qualitatives qui prouveront la valeur des changements que vous apportez. Pour véritablement optimiser, vous devez être en mesure de mesurer l&#39;impact et la valeur de vos efforts. Sinon, les modifications que vous apportez entraîneront des coûts plus élevés, avec un gain minimal. Pour y parvenir de façon efficace et efficiente, il faut commencer par la planification stratégique. Sans inclure de plan stratégique dans votre optimisation, ce serait une simple supposition.

### Six principes fondamentaux de l’optimisation

1. **Stratégier** : identifier les opportunités des activités qui sont alignées sur les objectifs commerciaux et qui sont basées sur les données.
1. **Hiérarchiser** : classer et planifier les activités en fonction de l’alignement des activités, du niveau d’effort et de l’impact potentiel.
1. **Conception** : créez des visuels finalisés d’expériences d’activité et élaborez des plans d’activité avec des critères détaillés.
1. **Créer et exécuter** : développez une activité, y compris la configuration des [!DNL Target], le développement du code et les tests d’assurance qualité.
1. **Analyser** : lancez [!DNL Target] activité en production et surveillez les performances pendant la durée de l’activité.
1. **Agir et itérer** : développez des recommandations basées sur les performances de l’activité de test ou de personnalisation.

Sachant que le changement est une constante, notre stratégie d’optimisation doit être un cycle d’exécution itératif pour répondre aux besoins en constante évolution de vos clients (voir la figure 1 ci-dessous).

![ Optimisation et personnalisation ](assets/optimize-and-personalize.png)

_Figure 1 - Cycle itératif d’optimisation_

## Création d’une stratégie d’optimisation

Le processus de développement d’une stratégie d’optimisation peut être décomposé en : (1) Création d’un plan d’activité de test et (2) Compréhension des bases d’optimisation.

1 : Le plan d’activité d’essai doit être documenté. Vous bénéficiez ainsi d’une norme de qualité minimale en ce qui concerne votre application d’activité de test. Votre plan d’activité de test doit inclure :

* **Nom et description :** nom intuitif de l’activité et description du thème de l’expérience. « Comment ? Quoi ? Quand ? Où ? Pourquoi ? »

* **Objectif :** objectif de l’activité et objectif commercial aligné sur lequel elle est conçue.

* **Hypothèse :** une hypothèse est une prédiction que vous créez avant d’exécuter une expérience. Il indique clairement ce qui est mis à l&#39;essai, ce que vous croyez que le résultat sera et pourquoi vous pensez que c&#39;est le cas. L’exécution de l’expérience confirmera ou infirmera votre hypothèse.

Une hypothèse complète se divise en trois parties :

* Si _variable_
* Alors _résultat_
* Parce que _raison_

* **Emplacement :** URL, section de page et type d’appareil.
* **Mesure de l’objectif :** comment le succès sera-t-il mesuré ?
* **Mesures Secondaire :** autres indicateurs de performance clés (KPI) utiles à évaluer dans le but de mieux comprendre l’impact et les itérations de planification.
* **Audience de l’activité :** description du filtrage d’exposition de test requis.
* **Audiences de rapports :** liste de descriptions des sous-ensembles de visiteurs à utiliser pour l’analyse.
* **Concepts d’expérience :** maquettes, exemples, maquettes et descriptions.

**Remarque générale :** tout élément d’une page web qui peut augmenter la valeur commerciale ou donner une précieuse insight au comportement des visiteurs peut être testé. Voici quelques types courants d’activités de test :

* Texte du titre
* Texte du contenu
* Texte du bouton
* Mise en page
* Photographie
* Couleur des boutons
* Disposition des éléments
* Retrait et ajout d&#39;éléments
* Ordre de navigation
* Taxonomie de navigation
* Mettre en évidence la recherche

2 : la deuxième étape de la stratégie consiste à comprendre les bases de l’optimisation, ce qui inclut la compréhension des éléments de test eux-mêmes. Les éléments de test de l’optimisation sont les suivants :

    A. Valeur de l
    
    élément . Pour ce faire, revenez en arrière et demandez-vous pourquoi un certain élément existe sur votre site et si le contenu a un objectif spécifique. Ces questions sont un bon point de départ si votre site vient de terminer une reconception ou si une nouvelle fonctionnalité a été récemment déployée. La tactique utilisée pour déterminer la valeur de l’élément est appelée Test d’inclusion/exclusion. Les tests d’inclusion/exclusion fournissent une bonne lecture de la valeur sur la page où l’élément est affiché.
    
    B. Présentation des éléments 
    
    c’est là que vous devez réfléchir à l’aspect général de l’élément et à la manière dont cela affecte la présentation globale de la page. La tactique utilisée pour la présentation consiste à se concentrer sur la modification du contenu et des éléments ayant un impact.
    
    C. Fonction de l
    
    élément : nous demandons ici si l’élément de la page fait ce qu’il est censé faire. L’interaction a-t-elle réussi et fonctionne-t-elle comme prévu ? L’interaction est-elle naturelle ou un point de friction ? La tactique utilisée pour cette fonction consiste à créer des expériences axées sur des fonctionnalités simples d’utilisation, sans incidence financière supplémentaire.

## Optimisation ou personnalisation

Maintenant que nous avons analysé et répertorié les composants de la stratégie, il est important de faire la distinction entre les efforts d’optimisation et les efforts de Personalization. L’optimisation est l’action consistant à utiliser au mieux ou le plus efficacement possible une situation ou une ressource, tandis que Personalization est l’action de concevoir ou de produire quelque chose pour répondre aux besoins individuels d’une personne.

À un niveau élevé :

* L’optimisation est axée sur les tests visant à déterminer ce qui est le plus efficace et le plus performant pour TOUS ceux qui interagissent avec votre présence numérique.
* Personalization effectue actuellement des tests afin de déterminer ce qui est le plus efficace et le plus performant pour CERTAINS de ceux qui interagissent avec votre présence numérique.

Lorsque vous vous concentrez sur l’optimisation, les activités de test les plus courantes sont les suivantes :

* **Test A/B :** test en temps réel de plusieurs pages ou éléments de page les uns par rapport aux autres pour obtenir une insight quantitative adaptée aux préférences du client.
* **Test multivarié :** comparaison de combinaisons d’offres entre les éléments d’une page afin de déterminer la combinaison la plus performante. En outre, le test multivarié identifie l’élément de la page qui améliore le mieux les conversions.

Lorsque vous vous concentrez sur Personalization, vous risquez de voir les mêmes activités de test que dans Optimisation , mais elles sont adaptées à des audiences plus spécifiques. Par exemple, dans les tests A/B, vous ajouterez probablement des pages et des audiences dans les expériences pour affiner votre Personalization.

Personalization comprend également le type d’activité de test Ciblage d’expérience , qui diffuse du contenu à des audiences spécifiques en fonction d’un ensemble de règles et de critères définis. À mesure que vous vous développez et approfondissez Personalization, c’est également là que vous exploiterez certaines des fonctionnalités premium de Target, telles que :

* Type d’activités Automated Personalization
* Type d’activités Recommendations

## Optimisation avant personnalisation

Compte tenu de ce qui précède, Adobe vous recommande d’effectuer l’optimisation avant de personnaliser et de faire passer Personalization du mode étendu au mode granulaire. Pour faire évoluer les activités Personalization de larges à granulaires, vous commencerez à utiliser un style de personnalisation un-à-plusieurs (large) (à l’aide des tests A/B), puis passerez à un style de personnalisation un-à-un (granulaire) (à l’aide d’activités de personnalisation automatisée).

Pour plus d’informations, veuillez lire la [QuickStart pour les tests de personnalisation et la création d’une feuille de route](https://experienceleague.adobe.com/en/perspectives/quickstart-for-personalization-testing-and-roadmap-creation).

Pour en savoir plus sur la stratégie et le leadership de la pensée, consultez le hub [Perspectives](https://experienceleague.adobe.com/en/perspectives).
