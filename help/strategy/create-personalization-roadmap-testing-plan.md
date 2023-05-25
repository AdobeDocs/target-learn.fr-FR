---
title: QuickStart pour les tests de personnalisation et la création de feuilles de route
description: Découvrez une structure que vous pouvez utiliser pour commencer à valider des activités de personnalisation et créer une feuille de route de personnalisation à exécuter via Adobe Target et Adobe Analytics.
solution: Target,Analytics
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
source-git-commit: 389f754ff909752d89f74a2d6c698fc9f5d8c354
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# QuickStart pour les tests de personnalisation et la création de feuilles de route

La personnalisation peut être puissante, mais elle doit être validée par des tests pour s’assurer qu’elle génère réellement de la valeur. Le test est la stratégie la plus efficace pour identifier qui, comment et ce que vous devez personnaliser.

Alors que nous entrons dans la deuxième décennie du 21ème siècle, des organisations comme la vôtre se délectent de stratégies de ciblage des consommateurs dépassées et d&#39;analyses de données inexactes. C&#39;est l&#39;aube de la personnalisation, une ère où les consommateurs en sont venus à s&#39;attendre à rien de moins qu&#39;une expérience personnalisée. La personnalisation au niveau de l’entreprise est un processus complexe et en constante évolution, mais lorsqu’elle est réalisée efficacement, elle maximise la satisfaction des clients et augmente considérablement le retour sur investissement.

L’article suivant fournit une structure que vous pouvez utiliser pour commencer à valider des activités de personnalisation et créer une feuille de route de personnalisation à exécuter via Adobe Target et Adobe Analytics. La structure QuickStart d’Adobe comprend :

1. **Identifier les opportunités de personnalisation** : utilisez l’analyse des données pour identifier les opportunités d’impact sur les indicateurs de performances clés de votre site, en fonction des objectifs commerciaux de votre entreprise.

1. **Développement de cas d’utilisation** : définissez les objectifs de votre activité de personnalisation en gardant à l’esprit les attributs du visiteur spécifiques, soyez explicite quant à la manière dont le contenu traité améliorera l’expérience du visiteur, déterminez à l’avance à quoi ressemblera le succès et quelles actions peuvent être entreprises à partir des enseignements du test.

1. **Créer une feuille de route** - agréger une liste et donner la priorité aux cas pratiques de personnalisation, veiller à ce que vos efforts se concentrent sur des activités à forte valeur ajoutée ; espèrent affiner et revoir les cas d’utilisation et la feuille de route en fonction des enseignements tirés.

1. **Concevoir et exécuter** : créez et lancez les activités Adobe Target pour diffuser du contenu traité pour les audiences prioritaires.

1. **Agir sur les résultats** : analysez les performances de l’activité et résumez les résultats, les informations, les recommandations et les étapes suivantes de l’activité.

## Étape 1 : Identifier les opportunités de personnalisation{#personalization}

Il s’agit du point de départ où vous commencez à former la feuille de route de la personnalisation. Lors de l’exécution d’un programme de personnalisation réussi, il est essentiel de se concentrer sur vos objectifs commerciaux clés et sur les indicateurs de performances clés. Les efforts de personnalisation doivent être harmonisés en conséquence afin de fournir de la valeur. Paul Morris, Adobe Consultant en affaires, déclare : &quot;Si tout ce que vous faites se répercute sur ces objectifs, votre programme est très susceptible de générer une valeur importante. Cependant, si vous avez une approche dispersée des tests, vous trouverez probablement quelques victoires, mais votre programme global ne sera pas aussi réussi.&quot;

>[!NOTE]
>
>Si vous ne savez pas immédiatement quels sont vos principaux objectifs commerciaux, il est important de les identifier dès que possible. Veillez à :


* Permet d’établir un alignement entre les objectifs de votre entreprise et votre hypothèse exploitable. Vous pourrez ainsi classer par priorité les cas d’utilisation qui offrent la plus grande valeur à votre entreprise.

* Rendre vos objectifs mesurables à des fins de suivi et corréler avec l’impact sur les recettes.

* L’alignement de chaque opportunité doit avoir une incidence sur une mesure d’objectif unique.

Parfois, vous pouvez avoir des objectifs qui semblent eux aussi intangibles, comme la valeur de la marque ou la fidélité. Il est essentiel que vous soyez en mesure de les mesurer afin de les utiliser comme mesures d’objectif pour les activités de personnalisation. En règle générale, ces types d’objectifs peuvent toujours être alignés sur l’impact des recettes, tel que la valeur client totale ou les coûts d’acquisition. Au fur et à mesure que vous progressez, veillez à passer régulièrement en revue les performances du programme par rapport à vos objectifs commerciaux clés afin de vous assurer que la valeur provient de votre programme de personnalisation.

Concentrez l’analyse des données afin d’identifier les zones spécifiques de votre site web qui peuvent être améliorées. Adobe recommande de commencer par Adobe Analytics pour générer des cas d’utilisation ciblés. Si une équipe Analytics est en place, demandez-lui de consulter les éléments suivants :

1. Tableaux de pré-formulaire personnels : une fonction d’idéation qui fournit des ventilations illimitées et qui peut vous aider à répondre à toutes les questions ou hypothèses que vous pourriez avoir.
1. Segmentation avancée : Segmentation IQ vous permet de comparer les visiteurs dans différentes sections de votre site.
1. Révisions juridiques - Identifiez les parties de votre site qui bénéficieraient le plus de la personnalisation. Ces révisions vous permettent de prendre du recul et de parcourir votre site comme le ferait un client.
1. Analyse des concurrents : il y a des chances que d’autres entreprises fassent face aux mêmes défis que vous. Cette analyse ne se limite pas aux entreprises du même secteur.

L’objectif de cette étape est de générer des informations exploitables sous la forme d’une hypothèse. Une hypothèse est une prédiction que vous créez avant de lancer une expérience. Il indique clairement ce qui est en train de changer, ce que vous croyez que le résultat sera et pourquoi vous pensez que c&#39;est le cas. Exécuter l&#39;expérience va prouver ou infirmer votre hypothèse. À la fin de cette étape, vous devriez avoir un ensemble d’hypothèses pour les opportunités de personnalisation qui amélioreront votre site web et la satisfaction des visiteurs.

## Étape 2 : Développement de cas d’utilisation{#use-cases}

Commencez par les hypothèses générées à l&#39;étape 1, puis développez vos activités autour d&#39;elles. Vous pouvez maintenant développer les tables de préformulaire créées à l’étape 1A. chacun des indicateurs de performance clés comporte un ensemble d’hypothèses qui deviennent ensuite des tests individuels dans Adobe Target. Si vous avez du mal à atteindre ce point, commencez le plus simplement possible, par exemple en vous concentrant sur les visiteurs récurrents qui consultent votre site. Pensez aux façons dont vous pouvez personnaliser votre page d’accueil pour les visiteurs récurrents. Une fois que vous disposez de votre ensemble d’hypothèses, vous devez définir chaque activité afin de donner une priorité efficace à chaque cas d’utilisation.

1. Définissez les audiences prioritaires auxquelles vous souhaitez diffuser du contenu personnalisé, en gardant à l’esprit les attributs du visiteur unique qui définissent qui il est et ce qu’il veut (par exemple, client existant ou client prospect) Les besoins des audiences prioritaires doivent correspondre aux objectifs de votre entreprise.

1. Identifiez l’emplacement spécifique dans le parcours du visiteur où le contenu personnalisé aura le plus d’impact. Concentrez-vous sur les pages où vous attendez des visiteurs de différentes personas ou de visiteurs ayant des besoins/intentions différents.

1. Commencez à planifier le travail de conception de votre variante. Le contenu doit être soigneusement géré en fonction des besoins et des besoins spécifiques de l’audience, en fonction de l’endroit où il se trouve dans leur parcours. Le contenu approprié doit être distinct et différencié.

## Étape 3 : Créer une feuille de route, agréger et classer par priorité les cas d’utilisation

Agrégez une liste complète d’opportunités de personnalisation qui capture au minimum l’emplacement, l’idée et la priorité des activités de personnalisation.

L’étape de priorisation est divisée en deux facteurs :

**Valeur :** Utilisez la recherche du secteur, l’évaluation des performances et des cas d’utilisation similaires du passé pour comprendre la valeur attendue de chacune de vos hypothèses. Vous souhaitez que votre valeur soit directement liée à l’un de vos principaux résultats commerciaux (KBO) et soit dans un format standard afin que chacun de vos cas d’utilisation puisse être comparé. La méthode la plus courante consiste à appliquer une valeur monétaire à chaque cas d’utilisation à des fins de comparaison.

* Coût : un coût naturel est associé à la création de vos variantes de conception dans Target, puis au déploiement potentiel. Vous devez maintenant estimer le coût associé à chaque cas d’utilisation. Le coût inclut le temps et les ressources nécessaires à la création d’expériences de test, à la planification et à l’analyse post-test.

Adobe vous recommande de classer chacun de vos cas d’utilisation sur une échelle de 1 à 5 ; 1 étant simple et 5 étant complexe. Vous disposez désormais d’un ensemble d’activités prioritaires que vous pouvez tester dans Adobe Target. Ces activités formeront la base de vos activités de personnalisation annuelles. Adobe recommande de réévaluer régulièrement la feuille de route de la personnalisation. Les enseignements tirés de chaque activité doivent influencer vos priorités de feuille de route prospectives. Les leçons retenues et les recommandations seront plus efficaces si elles sont appliquées en temps opportun. Les priorités peuvent changer tout au long de l’année, mais l’application d’une méthodologie itérative garantit que vous avez toujours un plan d’action stratégique en place et que vous pouvez le suivre par rapport aux objectifs de votre équipe et de votre entreprise.

## Étape 4 : Concevoir et exécuter

En exploitant la documentation créée pour configurer le cas d’utilisation de la personnalisation, construisez l’activité de personnalisation dans Target pour diffuser du contenu traité pour vos audiences prioritaires. Assurez-vous que le type d’activité, les paramètres, les expériences et les fonctionnalités de création de rapports correspondent aux objectifs du cas d’utilisation. La conception, l’assurance qualité et le lancement de vos efforts de personnalisation sont plus efficaces lorsque les processus d’organisation existants les affectent.

## Étape 5 : Agir sur les résultats

Une fois que votre activité de personnalisation a mobilisé un échantillon représentatif de visiteurs, vous pouvez commencer l’analyse en exploitant les informations pour guider les étapes suivantes. Soyez guidé par les données de votre analyse, en liant les recommandations à votre hypothèse de cas d’utilisation et en illustrant clairement l’impact sur les objectifs de l’entreprise.

### Informations supplémentaires

Nous vous recommandons de regarder cette vidéo qui présente chacune des étapes suivantes : [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

Pour en savoir plus sur la stratégie et le leadership de la pensée, voir [Succès des clients](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html) hub.