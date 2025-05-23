---
title: Optimisation de la mise en oeuvre Adobe Target
description: Obtenez un aperçu de la mise en oeuvre et de la structure d’Adobe Target. Découvrez comment comprendre et contrôler la configuration de votre organisation. Découvrez les techniques de dépannage courantes et des conseils sur la création d’un référentiel de connaissances pour votre équipe.
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# Optimisation de la mise en oeuvre Adobe Target

Si vous découvrez votre entreprise et que vous souhaitez vous familiariser avec ce qui est en place à partir d’une pratique de test et d’optimisation, cet article vous aide à démarrer. Nous commencerons par une présentation de la mise en oeuvre et de la structure d’Adobe Target. Vous apprendrez à comprendre et à contrôler la configuration de votre organisation. Enfin, nous discuterons des techniques de dépannage courantes et des conseils sur la création d’un référentiel de connaissances pour votre équipe.

Adobe Target est un outil qui permet de tester et de cibler du contenu unique pour différents visiteurs. Pour un aperçu des fonctionnalités disponibles, [consultez ce guide](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=fr).

## Implémentation et structure de Target

Avant de passer au processus de mise en oeuvre d’Adobe Target ou à sa structure, il est utile de commencer par comprendre quelques principes de base du logiciel.

Adobe Target est un outil qui permet de tester et de cibler du contenu unique pour différents visiteurs sans modifier le code natif du site web. Target modifie temporairement l’expérience de l’utilisateur final et suit le comportement des utilisateurs après avoir vu la modification. Target offre également la possibilité de modifier l’expérience pour les utilisateurs finaux en fonction des informations de profil ou des actions précédentes.

Il existe trois types d’activité fondamentaux de Target :

1. Test A/B
2. Test multivarié (MVT)
3. Test d’expérience

**Le test A/B** compare plusieurs expériences afin de déterminer celle qui améliore le mieux les conversions tout au long d’une période de test prédéfinie. Le test A/B est une expérience hautement contrôlée avec des mesures de trafic, fractionnées en pourcentages plutôt qu’en règles, qui vous permet d’effectuer les opérations suivantes :

* pour analyser les données de test.
* pour obtenir des informations sur votre audience.
* pour déterminer l’expérience la plus performante.

Le **test multivarié** (MVT) compare des combinaisons d’offres parmi les éléments d’une page afin de déterminer la combinaison offrant les meilleures performances pour une audience spécifique. Ce test identifie également l’élément de la page qui améliore le mieux les conversions tout au long d’une période de test prédéfinie. MVT fournit :

* Une façon d’afficher plusieurs offres dans plusieurs éléments.
* Méthode permettant de tester l’expérience unique résultante par rapport à un objectif spécifique.
* Identifier les éléments qui ont le plus d’impact négatif ou positif sur les interactions des visiteurs.

**Le** (ciblage d’expérience) diffuse du contenu à une audience spécifique selon un ensemble de règles et de critères définis par le marketeur. Cette méthode permet de cibler du contenu spécifique sur une audience spécifique en fonction d’un ensemble de règles d’attribution définies.

Comment Target fonctionne-t-il ?

Voici un exemple général du fonctionnement de Target :

1. Un visiteur demande une page à votre serveur et elle s’affiche dans le navigateur.
1. Un cookie propriétaire est défini dans le navigateur du visiteur pour stocker le comportement.
1. La page appelle ensuite Adobe Target.
1. Le contenu s’affiche en fonction des règles de l’activité de l’utilisateur.
1. Adobe Target capture des mesures spécifiques telles que définies dans la configuration de l’activité pour évaluer l’impact des expériences de test.

Target est basé sur une &quot;mbox globale&quot; qui permet d’avoir un impact sur n’importe quel élément de la page. Cette fonctionnalité est déployée au chargement de la page sous la forme d’un lien codé en dur vers le fichier at.js ou elle est diffusée à l’aide d’un gestionnaire de balises comme Adobe Launch.

## Présentation de votre implémentation actuelle

Pour comprendre votre mise en oeuvre actuelle, Adobe vous recommande de passer en revue votre mise en oeuvre de l’interface utilisateur Target, ainsi que votre mise en oeuvre de Tag Manager et de Page Load.

**Pour passer en revue votre [!DNL Target] interface utilisateur :**

1. Commencez votre révision dans l’interface utilisateur de [!DNL Target] :

   * Examinez la pile de technologie [!DNL Target]
   * Confirmation des fonctionnalités disponibles
   * Identifier l’emplacement du déploiement actif

1. Examinez les activités pour connaître les bonnes pratiques :

   * Vérifier les campagnes historiques pour la maturité du programme

1. Désactiver les anciennes activités :

   * Archivage et nettoyage d’une ressource [!DNL Target] qui n’a plus d’utilisation actuelle ou future

1. Examinez les audiences.

1. Examinez les définitions d’environnement et les domaines associés.

1. Vérifier les scripts de profil pour l’applicabilité

   * Tous les scripts de profil sont exécutés à chaque appel cible
   * Conserver l’efficacité des appels en supprimant les scripts non applicables

Pour examiner le gestionnaire de balises et le chargement de page :

1. Confirmez ce qui suit dans le gestionnaire de balises :

   * Déploiement du code JavaScript [!DNL Target] attendu
   * Solution de masquage du contenu appropriée
   * Définissez les règles nécessaires pour remplir les appels [!DNL Target] avec les paramètres attendus.

1. Confirmez ce qui suit au chargement de la page :

   * Correspondance de numéros de version pour l’URL de requête et l’URL de requête [!DNL Target]
   * Valeur Experience Cloud ID renseignée (Cloud Body)
   * Présenter les valeurs d’intégration attendues (Cloud Body)
   * Paramètres renseignés [!DNL Target] sur les pages appropriées

## [!DNL Target] activités d’audit

Pour éviter de parcourir manuellement chaque page pour contrôler les activités [!DNL Target], utilisez Adobe Auditor afin de vous aider à comprendre l’état technique actuel de votre mise en oeuvre. Adobe Auditor est optimisé par ObservePoint et peut être configuré pour s’exécuter manuellement afin d’identifier les problèmes de mise en oeuvre de haut niveau sur votre site.

Adobe Auditor fournit les informations suivantes :

* Un haut niveau de santé
* Appels rapides pour les problèmes de mise en oeuvre

Adobe recommande d’effectuer des audits manuels mensuels pour :

* Identification des pages non balisées
* Identification des versions incohérentes
* Découvrez les versions obsolètes
* Fournir des informations détaillées qui peuvent être exportées

## Résolution des problèmes courants

>[!NOTE]
>
>Adobe recommande d’installer l’Adobe Experience Platform Debugger.

Vous trouverez ci-dessous des conseils généraux de dépannage lors de la saisie de l’expérience :

### Cache et cookies**

* Effacement du cache et des cookies
* Faites attention en utilisant le mode privé (par exemple : le mode privé dans Firefox peut bloquer [!DNL Target]).

### Êtes-vous qualifié pour l’activité ?

* Vérifiez que vous avez effectué les mêmes étapes que l’audience utilisée dans l’activité.
* Utiliser `mboxTrace` ou des jetons de réponse pour vérifier les valeurs de profil et de segment

### Conseils de dépannage généraux lors de la validation visuelle/fonctionnelle

Si se trouve dans l’expérience [!DNL Target] et que vous ne voyez pas l’expérience visuelle attendue :

Vérifiez la réponse [!DNL Target] :

* Si le code n’est pas exécuté :

1. Vérifier les activités en conflit
1. Contacter le service à la clientèle

* Si le code est exécuté :

1. Retravailler le code dans ce scénario

## Maintenance d&#39;un référentiel de connaissances

Un référentiel de connaissances est une plateforme en ligne utilisée pour documenter et partager des informations. Le référentiel de connaissances contient des informations spécifiques à votre mise en oeuvre et peut contenir des informations spécifiques à l’équipe.

Idéalement, le référentiel doit permettre la modification et l’enregistrement automatique dans la plateforme. Une fois paramétré initialement, il est facile de le gérer et de le tenir à jour. Le contenu du référentiel de connaissances est traité en fonction des rôles utilisateur.

Les documents standard d’un référentiel de connaissances sont les suivants :

* **Document de présentation** : document utilisé pour expliquer clairement les objectifs, les objectifs, les processus et la structure du programme.
* **Référentiel d’idées** : document utilisé pour gérer et classer par priorité les idées potentielles qui ne sont pas prêtes pour le processus de test.
* **Feuille de route du programme** : document utilisé pour gérer tous les aspects des activités de test une fois que les idées sont prêtes à démarrer le processus de test.
* **Document de plan d’activité** : document utilisé pour décrire les informations nécessaires à la création et au lancement des activités
* **Document de plan d’activité** : document utilisé pour communiquer les résultats et les étapes suivantes recommandées aux parties prenantes
* **Tableau de bord du programme** : document utilisé pour effectuer le suivi des performances, de la cadence et des recettes du programme au fil du temps.

Pour plus d’informations, consultez notre [webinaire](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) avec Wilder Freed, consultant principal.

Pour en savoir plus sur la stratégie et le leadership de la pensée, rendez-vous sur le [hub Customer Success](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html?lang=fr).
