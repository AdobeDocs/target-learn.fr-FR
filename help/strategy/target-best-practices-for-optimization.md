---
title: Bonnes pratiques pour l’optimisation
description: 'Découvrez les six éléments essentiels de l’optimisation de l’Adobe et comment les appliquer. '
solution: Target
source-git-commit: fd679d3fc2c72b9852d8129adf8c1187bf22b25f
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Bonnes pratiques relatives à l’optimisation avec Adobe Target

Découvrez les six éléments essentiels de l’optimisation de l’Adobe et comment les appliquer.

Quand il s&#39;agit de renforcer la présence numérique, votre équipe devra faire face à un certain nombre de défis. Non seulement vous êtes chargé d’impliquer des centaines, voire des milliers de clients, mais en plus, vos clients affichent une variété de comportements et de préférences uniques qui changeront au fil du temps. Il vous appartient non seulement de suivre ces changements, mais de les anticiper et d’exécuter vos stratégies de manière efficace et précise. C&#39;est une course contre la concurrence dans un marathon de contenu perpétuel, qui nécessite une itération constante et une technologie de pointe.

Une solution à ce défi à multiples facettes est l’optimisation avec Adobe Target, qui vous permet d’avoir une présence numérique évolutive pertinente, précieuse et sans friction. L’architecture technique et les canaux dans lesquels vous déployez [!DNL Target] varie considérablement d’un client à l’autre. Cependant, nous avons dressé une liste des bonnes pratiques et des stratégies d’optimisation que chaque équipe peut utiliser pour exploiter toutes les fonctionnalités de cet outil puissant.

## Présentation de l’optimisation

L’optimisation est définie comme &quot;l’action consistant à utiliser au mieux ou le plus efficacement possible une situation ou une ressource&quot;. C’est le moyen le plus efficace de vous assurer que vous disposez de données qualitatives qui prouvent que les modifications que vous apportez sont importantes. Pour véritablement optimiser, vous devez être en mesure de mesurer l’impact et la valeur de vos efforts. Sinon, les modifications que vous apportez entraîneront des coûts plus élevés, avec un gain minimal. Pour y parvenir efficacement, il faut commencer par planifier la stratégie. Sans inclure de plan stratégique dans votre optimisation, vous ne feriez que deviner.

### Six éléments essentiels de l’optimisation

1. **Strategize**: Identifiez les opportunités d’activités qui correspondent aux objectifs de l’entreprise et qui reposent sur des données.
1. **Définir la priorité**: Classement et planification des activités en fonction de l’alignement métier, du niveau d’effort et de l’impact potentiel.
1. **Conception**: Créez des visuels finalisés des expériences d’activité et développez des plans d’activité avec des critères détaillés.
1. **Créer et exécuter**: Activité de développement incluant [!DNL Target] configuration, développement de code et tests d’assurance qualité.
1. **Analyser**: Launch [!DNL Target] à la production et surveiller les performances pendant la durée de l’activité.
1. **Agir et effectuer une itération**: Développez des recommandations basées sur les performances des activités de test ou de personnalisation.

Sachant que le changement est une constante, notre stratégie d’optimisation doit être un cycle d’exécution itératif pour répondre aux besoins en constante évolution de vos clients (voir l’illustration 1 ci-dessous).

![Optimisation et personnalisation](assets/optimize-and-personalize.png)

_Figure 1 - Cycle itératif d’optimisation_

## Construire une stratégie d&#39;optimisation

Le processus de développement d’une stratégie d’optimisation peut être divisé en : (1) Créez un plan d’activité de test et (2) Comprenez les principes de base de l’optimisation.

1 : Le plan d’activité de test doit être documenté. Vous disposez ainsi d’un niveau de qualité minimal pour l’application de votre activité de test. Votre plan d’activité de test doit inclure :

* **Nom et description :** Nom intuitif de l’activité et description de la cible de l’expérience. &quot;Comment ? Quoi ? Lors de la? Où? Raison?&quot;

* **Objectif :** Objectif de l’activité et objectif commercial aligné, il est conçu pour avoir un impact.

* **Hypothèse :** Une hypothèse est une prédiction que vous créez avant de lancer une expérience. Il indique clairement ce qui est testé, ce que vous croyez que le résultat sera et pourquoi vous pensez que c&#39;est le cas. Exécuter l&#39;expérience va prouver ou infirmer votre hypothèse.

Une hypothèse complète comporte trois parties :

* If _variable_
* Alors _result_
* Parce que _raisonnement_

* **Emplacement :** URL, section de page et type d’appareil.
* **Mesure de l’objectif :** Comment le succès sera-t-il mesuré ?
* **Mesures Secondaire :** Autres indicateurs de performance clés (IPC) précieux à évaluer dans le but de mieux comprendre les itérations d’impact et de planification.
* **Audience de l’activité :** Description du filtrage de l’exposition au test requis.
* **Audiences avec création de rapports :** Liste des descriptions des sous-ensembles de visiteurs à utiliser pour l’analyse.
* **Concepts d’expérience :** Recherches, exemples de maquettes et descriptions.

**Remarque générale :** Il est possible de tester tout élément d’une page web pouvant générer de la valeur pour l’entreprise ou donner des informations précieuses sur le comportement des visiteurs. Voici quelques types d’activités de test courants :

* Texte du titre
* Texte du contenu
* Texte du bouton
* Mise en page
* Photographie
* Couleur du bouton
* Mettre en page les éléments
* Suppression et ajout d’éléments
* Ordre de navigation
* Taxonomie de navigation
* Accent de recherche

2 : La deuxième étape de la stratégie consiste à comprendre les principes de base de l’optimisation, ce qui inclut la compréhension des éléments de test eux-mêmes. Les éléments de test de l’optimisation incluent :

    A. Valeur de l’élément
    
    Pour ce faire, prenez du recul pour demander pourquoi un certain élément existe sur votre site et le contenu est-il destiné à un objectif spécifique ? Ces questions sont un bon point de départ si votre site vient de terminer une reconception ou si une nouvelle fonctionnalité a été récemment déployée. La tactique utilisée pour déterminer la valeur de l’élément est appelée Test d’inclusion/exclusion. Le test d’inclusion/exclusion permet une bonne lecture de la valeur sur la page où l’élément est affiché.
    
    B. Présentation des éléments
    
    C’est là que vous réfléchissez à l’aspect global de l’élément et à son impact sur la présentation générale de la page. La tactique utilisée pour la présentation consiste à mettre l’accent sur l’impact des changements de contenu et de page d’élément.
    
    C. Fonction de l’élément
    
    Ici, nous demandons : &quot;L&#39;élément de la page fait-il ce qu&#39;il est censé faire ?&quot; L&#39;interaction est-elle réussie et fonctionne-t-elle comme prévu ? L&#39;interaction est-elle naturelle, ou est-elle un point de friction ? La tactique utilisée pour la fonction consiste à créer des expériences axées sur des fonctionnalités faciles à utiliser sans impact sur les coûts supplémentaires.

## Optimisation et personnalisation

Maintenant que nous avons analysé et répertorié les composants de la stratégie, il est important d’établir une distinction entre les efforts d’optimisation et les efforts de personnalisation. L’optimisation est l’action consistant à utiliser au mieux ou le plus efficacement une situation ou une ressource, tandis que la personnalisation est l’action consistant à concevoir ou à produire quelque chose pour répondre aux besoins individuels de quelqu’un.

À un niveau élevé :

* L’optimisation est axée sur les tests afin de trouver les éléments les plus efficaces et les plus performants pour TOUS ceux qui interagissent avec votre présence numérique.
* La personnalisation consiste à tester les éléments les plus efficaces et les plus performants pour CERTAINS de ceux qui interagissent avec votre présence numérique.

Lors de l’optimisation, les activités de test les plus courantes sont les suivantes :

* **Test A/B :** Test en temps réel de plusieurs pages ou éléments de page les uns par rapport aux autres pour obtenir des informations quantitatives sur les préférences des clients.
* **Test multivarié :** Comparaison de combinaisons d’offres parmi les éléments d’une page afin de déterminer la combinaison offrant les meilleures performances. En outre, le test multivarié identifie l’élément de la page qui améliore le mieux les conversions.

Lorsque vous vous concentrez sur la personnalisation, il est probable que vous visualisiez les mêmes activités de test que dans Optimisation, mais elles sont orientées vers des audiences plus spécifiques. Par exemple, dans les tests A/B, vous ajouterez probablement des pages et des audiences dans les expériences pour optimiser votre personnalisation.

La personnalisation comprend également le type d’activité de test de ciblage d’expérience , qui diffuse du contenu à des audiences spécifiques en fonction d’un ensemble de règles et de critères définis. Au fur et à mesure que vous commencerez à grandir et à vous intégrer à la personnalisation, c’est également là que vous tirerez parti de certaines des fonctionnalités majeures de Target, telles que :

* Type d’activité Automated Personalization
* Type d’activités de recommandation

## Optimisation avant personnalisation

Compte tenu de ce qui précède, Adobe vous recommande d’optimiser avant de personnaliser et d’avancer la personnalisation de manière générale à granulaire. Pour parfaire les activités de personnalisation de manière générale à granulaire, vous commencerez à utiliser un style de personnalisation &quot;un à plusieurs&quot; (large) (à l’aide du test A/B), puis passerez à un style de personnalisation &quot;un à un&quot; (granulaire) (à l’aide des activités de personnalisation automatisée).

Pour plus d’informations, veuillez écouter [webinaire sur la compréhension et l’optimisation de la mise en oeuvre d’Adobe Target](https://adobecustomersuccess.adobeconnect.com/pkfafpzd9yarmp4/), avec la conseillère en affaires Katie Cozby.
