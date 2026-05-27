---
title: Démarrage rapide pour les tests de personnalisation et la création d’une feuille de route
description: Découvrez un framework que vous pouvez utiliser pour commencer à valider les activités de personnalisation et créer une feuille de route de personnalisation à exécuter via Adobe Target et Adobe Analytics.
solution: Target,Analytics
level: Intermediate
role: Leader, Developer, Admin
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
TQID: https://experienceleague.adobe.com/d2BYxVQLaDPbZ7538S-uP1pSjtGgd10nYk-WW3KnVZk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 1438
ht-degree: 0%

---

# Démarrage rapide pour les tests de personnalisation et la création d’une feuille de route

Personalization peut être puissant, mais il doit être validé par des tests pour s’assurer qu’il génère réellement de la valeur. Les tests constituent la stratégie la plus efficace pour identifier qui, comment et ce que vous devez personnaliser.

Alors que nous entrons dans la deuxième décennie du XXIe siècle, des organisations comme la vôtre s&#39;écartent des stratégies obsolètes de ciblage des consommateurs et de l&#39;analyse inexacte des données. Nous sommes à l’aube de la personnalisation, une ère où les consommateurs en sont venus à n’attendre rien de moins qu’une expérience personnalisée. Personalization au niveau de l’entreprise est un processus complexe et en constante évolution, mais lorsqu’il est mis en œuvre efficacement, il permet d’optimiser la satisfaction des clients et d’augmenter considérablement le retour sur investissement.

L’article suivant fournit un framework que vous pouvez utiliser pour commencer à valider les activités de personnalisation et créer une feuille de route de personnalisation à exécuter via Adobe Target et Adobe Analytics. Le framework QuickStart d’Adobe comprend :

1. **Identifier les opportunités de personnalisation** - utilisez l’analyse des données pour identifier les opportunités d’affecter les indicateurs clés de performance de votre site, en fonction des objectifs commerciaux de votre organisation.

1. **Développer des cas d’utilisation** - définissez les objectifs de votre activité de personnalisation en gardant à l’esprit des attributs de visiteur spécifiques, soyez explicite sur la manière dont le contenu traité améliorera l’expérience du visiteur, établissez à l’avance à quoi ressemblera la réussite et quelles actions peuvent être entreprises à partir des enseignements de test.

1. **Créer une feuille de route** - agrégez une liste et hiérarchisez les cas d’utilisation de la personnalisation, assurez-vous que vos efforts sont concentrés sur des activités à forte valeur ajoutée. Attendez-vous à affiner et à réviser les cas d’utilisation et la feuille de route en fonction des enseignements tirés.

1. **Concevoir et exécuter** - Créez et lancez les activités Adobe Target pour diffuser du contenu traité pour vos audiences prioritaires.

1. **Agir sur les résultats** - Analysez les performances des activités et résumez les résultats, les informations, les recommandations et les étapes suivantes de l’activité.

## Étape 1 : identifier les opportunités de personnalisation{#personalization}

C’est le point de départ où vous commencez à élaborer la feuille de route Personalization. Lors de l’exécution d’un programme de personnalisation réussi, il est essentiel de se concentrer sur vos objectifs commerciaux clés et vos indicateurs de performance clés. Les efforts de Personalization doivent être alignés en conséquence afin d’apporter de la valeur ajoutée. Paul Morris, conseiller d’entreprise Adobe, déclare : « Si tout ce que vous faites contribue à la réalisation de ces objectifs, votre programme est très susceptible de générer une valeur significative. Cependant, si votre approche des tests est dispersée, vous obtiendrez probablement des résultats positifs, mais votre programme global ne sera pas aussi efficace. »

>[!NOTE]
>
>Si vous ne connaissez pas immédiatement vos principaux objectifs commerciaux, il est important de les identifier le plus tôt possible. Veillez à :


* Alignez-vous sur vos objectifs commerciaux et votre hypothèse exploitable. Cela vous permettra de donner la priorité aux cas d’utilisation qui offrent la plus grande valeur à votre entreprise.

* Rendez vos objectifs mesurables à des fins de suivi et corrélez-les à l’impact sur le chiffre d’affaires.

* L’alignement de chaque opportunité doit avoir un impact sur une mesure d’objectif unique.

Parfois, vous pouvez également avoir des objectifs qui semblent initialement intangibles, tels que la valeur de la marque ou la fidélité. Il est essentiel que vous puissiez les mesurer afin de les utiliser comme mesures d’objectif pour les activités Personalization. En règle générale, ces types d’objectifs peuvent toujours être alignés sur l’impact sur le chiffre d’affaires, comme la valeur client à vie ou les coûts d’acquisition.Au fur et à mesure de votre progression, assurez-vous d’examiner régulièrement les performances du programme par rapport à vos objectifs commerciaux clés afin de vous assurer que votre programme Personalization génère de la valeur.

Concentrez-vous sur l’analyse des données pour identifier les zones spécifiques de votre site web qui peuvent être améliorées. Adobe recommande de commencer par Adobe Analytics pour générer des cas d’utilisation ciblés. Si vous avez mis en place une équipe Analytics, demandez-lui d’examiner les points suivants :

1. Tableaux préformulaires personnels : une fonctionnalité d’idéation qui fournit des répartitions illimitées et peut vous aider à répondre à vos questions ou hypothèses.
1. Segmentation avancée - Segmentation IQ vous permet de comparer les visiteurs dans différentes sections de votre site.
1. Examens juridiques - Identifiez les parties de votre site qui bénéficieraient le plus de Personalization. Ces avis vous permettent de prendre du recul et de parcourir votre site comme le ferait un client.
1. Analyse de la concurrence - Il est fort probable que d&#39;autres entreprises soient confrontées aux mêmes défis que vous. Cette analyse ne se limite pas aux entreprises de la même industrie.

L’objectif de cette étape est de générer une insight exploitable sous la forme d’une hypothèse. Une hypothèse est une prédiction que vous créez avant d’exécuter une expérience. Il indique clairement ce qui est modifié, ce que vous croyez que le résultat sera et pourquoi vous pensez que c&#39;est le cas. L’exécution de l’expérience confirmera ou infirmera votre hypothèse. À la fin de cette étape, vous devez disposer d’un ensemble d’hypothèses pour les opportunités de personnalisation qui amélioreront votre site web et la satisfaction des visiteurs et visiteuses.

## Étape 2 : développer des cas d’utilisation{#use-cases}

Commencez par les hypothèses générées à l’étape 1, puis développez vos activités autour d’elles. Vous pouvez maintenant développer les tableaux de préformulaire créés à l’étape 1A ; chacun des indicateurs de performance clés comporte un ensemble d’hypothèses, qui deviennent ensuite des tests individuels dans Adobe Target. Si vous avez du mal à en arriver là, commencez le plus simplement possible, par exemple en vous concentrant sur les visiteurs récurrents qui fréquentent votre site. Pensez aux façons d’adapter votre page d’accueil à vos visiteurs réguliers. Une fois que vous disposez de votre ensemble d’hypothèses, vous devez définir chaque activité pour classer par priorité chaque cas d’utilisation.

1. Définissez les audiences prioritaires vers lesquelles vous souhaitez diffuser du contenu personnalisé, en tenant compte des attributs de visiteur uniques qui définissent qui ils sont et ce qu’ils veulent (par exemple, client existant ou client potentiel). Les souhaits et les besoins des audiences prioritaires doivent s’aligner sur les objectifs de votre entreprise

1. Identifiez l’emplacement spécifique dans le parcours du visiteur ou de la visiteuse où le contenu personnalisé aura le plus d’impact. Concentrez-vous sur les pages où vous attendez des visiteurs aux profils variés ou ayant des besoins/intentions différents.

1. Commencez à planifier le travail de conception de votre variante. Le contenu doit être soigneusement organisé en fonction des besoins et des souhaits spécifiques de l’audience, en tenant compte de leur emplacement dans leur parcours. Le contenu approprié doit être distinct et différencié.

## Étape 3 : création d’une feuille de route, agrégation et hiérarchisation des cas d’utilisation

Agrégez une liste complète d’opportunités de personnalisation qui capture au minimum l’emplacement, l’idée et la priorité des activités de personnalisation.

L’étape de hiérarchisation est divisée en deux facteurs :

**Valeur :** utilisez la recherche sur le secteur, l’évaluation comparative et des cas d’utilisation similaires du passé pour comprendre la valeur attendue de chacune de vos hypothèses. Vous souhaitez que votre valeur soit directement liée à l’un de vos principaux résultats commerciaux (KBO) et qu’elle soit dans un format standard afin que chacun de vos cas d’utilisation puisse être comparé. La méthode la plus courante consiste à appliquer une valeur monétaire à chaque cas d’utilisation à des fins de comparaison.

* Coût : il existe un coût naturel associé à la création de vos variantes de conception dans Target, puis au déploiement potentiel. Vous devez maintenant estimer le coût associé à chaque cas d’utilisation. Le coût inclut le temps et les ressources nécessaires pour créer des expériences de test, la planification et l’analyse post-test.

Adobe vous recommande de classer chacun de vos cas d’utilisation sur une échelle de 1 à 5, 1 étant simple et 5 étant complexe. Vous disposez désormais d’un ensemble d’activités prioritaires que vous pouvez tester dans Adobe Target. Ces activités formeront la base de vos activités de personnalisation annuelles. Adobe recommande de réévaluer régulièrement la feuille de route Personalization. Les leçons tirées de chaque activité devraient influencer vos priorités prospectives de feuille de route. Les enseignements et les recommandations auront plus d’impact s’ils sont mis en œuvre en temps opportun. Les priorités peuvent changer tout au long de l&#39;année, mais l&#39;application d&#39;une méthodologie itérative garantit que vous avez toujours un plan d&#39;action stratégique en place et que vous pouvez effectuer un suivi par rapport aux objectifs de votre équipe et de votre entreprise.

## Étape 4 : conception et exécution

Tirez parti de la documentation créée pour élaborer une stratégie pour le cas d’utilisation de la personnalisation, créez l’activité Personalization dans Target pour diffuser du contenu adapté à vos audiences prioritaires. Assurez-vous que le type d’activité, les paramètres, les expériences et les fonctionnalités de création de rapports sont alignés sur les objectifs du cas d’utilisation. La conception, le contrôle qualité et le lancement de votre effort de personnalisation sont plus efficaces lorsqu’ils s’inscrivent dans des processus d’entreprise existants.

## Étape 5 : Agir sur les résultats

Une fois que votre activité de personnalisation a impliqué un échantillon représentatif de visiteurs, vous pouvez commencer l’analyse en exploitant les informations pour guider les étapes suivantes. être piloté par les données dans votre analyse, en liant les recommandations à votre hypothèse de cas d’utilisation et en illustrant clairement l’impact sur les objectifs commerciaux.

### Plus d’informations

Nous vous recommandons de regarder cette vidéo qui décrit chacune de ces étapes : [&#128279;](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

Pour en savoir plus sur la stratégie et le leadership, consultez le hub [Succès client](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html?lang=fr).