---
title: Optimisation de votre implémentation Adobe Target
description: Obtenez un aperçu de l’implémentation et de la structure d’Adobe Target. Découvrez comment comprendre et auditer la configuration de votre organisation. Découvrez les techniques de dépannage courantes et des conseils pour créer un référentiel de connaissances pour votre équipe.
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# Optimisation de votre implémentation Adobe Target

Si vous êtes nouveau dans votre organisation et que vous souhaitez vous familiariser avec ce qui est en place grâce à une pratique de test et d’optimisation, cet article vous aidera à commencer. Nous allons commencer par un aperçu de la mise en œuvre et de la structure d’Adobe Target. Vous apprendrez à comprendre et à auditer la configuration de votre organisation. Enfin, nous discuterons des techniques de dépannage courantes et des conseils sur la création d’un référentiel de connaissances pour votre équipe.

Adobe Target est un outil qui permet de tester et de cibler du contenu unique pour différents visiteurs. Pour obtenir un aperçu des fonctionnalités disponibles, [consultez ce guide](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en).

## Implémentation et structure de Target

Avant d’aborder le processus de mise en œuvre ou la structure d’Adobe Target, il est utile de comprendre certains principes de base du logiciel.

Adobe Target est un outil qui permet de tester et de cibler du contenu unique pour différents visiteurs sans modifier le code natif du site web. Target modifie temporairement l’expérience de l’utilisateur final et suit le comportement des utilisateurs après avoir constaté la modification. Target offre également la possibilité de modifier l’expérience des utilisateurs finaux en fonction des informations de profil ou d’actions précédentes.

Il existe trois types d’activités fondamentales de Target :

1. Test A/B
2. Multivariate testing (MVT)
3. Test d’expérience

Le **test A/B** compare plusieurs expériences afin de déterminer celle qui améliore le mieux les conversions au cours d’une période de test prédéfinie. Le test A/B est une expérience hautement contrôlée avec des mesures de trafic, divisées par des pourcentages plutôt que par une règle, ce qui vous permet d’effectuer les opérations suivantes :

* pour analyser les données de test.
* pour obtenir des informations sur votre audience.
* pour déterminer l’expérience la plus performante.

Le **test multivarié** (MVT) compare les combinaisons d’offres entre les éléments d’une page afin de déterminer la combinaison la plus performante pour une audience spécifique. Ce test identifie également l’élément de la page qui améliore le mieux les conversions tout au long d’une période de test prédéfinie. MVT offre les avantages suivants :

* Méthode d’affichage de plusieurs offres dans plusieurs éléments.
* Méthode permettant de tester l’expérience unique obtenue par rapport à un objectif spécifique.
* Insight sur les éléments qui ont l’impact négatif ou positif le plus important sur les interactions des visiteurs.

Le **test d’expérience** (ciblage d’expérience) diffuse du contenu à une audience spécifique selon un ensemble de règles et de critères définis par les responsables marketing. Cette méthode permet de cibler un contenu spécifique vers une audience spécifique en fonction d’un ensemble de règles d’attribution définies.

Comment fonctionne Target ?

Voici un exemple détaillé du fonctionnement de Target :

1. Un visiteur demande une page à votre serveur et l’affiche dans le navigateur.
1. Un cookie propriétaire est défini dans le navigateur du visiteur pour stocker le comportement.
1. La page appelle ensuite Adobe Target.
1. Le contenu s’affiche en fonction des règles de l’activité de l’utilisateur.
1. Adobe Target capture les mesures spécifiques définies dans la configuration des activités afin d’évaluer l’impact des expériences de test.

Target repose sur une « mbox globale » qui permet d’agir sur tout ce qui se trouve sur la page. Cette fonctionnalité se déploie au chargement de la page, soit sous la forme d’un lien codé en dur vers le fichier at.js, soit à l’aide d’un gestionnaire de balises comme Adobe Launch.

## Comprendre votre implémentation actuelle

Pour comprendre votre implémentation actuelle, Adobe vous recommande de passer en revue votre implémentation de l’interface utilisateur de Target, ainsi que votre implémentation du gestionnaire de balises et du chargement de page.

**Pour passer en revue votre interface utilisateur [!DNL Target], procédez comme suit**

1. Commencez votre examen sur l’interface utilisateur de [!DNL Target] :

   * Examen de la pile technologique [!DNL Target]
   * Confirmer les fonctionnalités disponibles
   * Identifier l’emplacement du déploiement

1. Examinez les activités pour connaître les bonnes pratiques :

   * Vérifier l’historique des campagnes pour la maturité du programme

1. Désactiver les anciennes activités :

   * Archiver et nettoyer [!DNL Target] ressource qui n’est plus utilisée actuellement ou ultérieurement

1. Vérifier les audiences.

1. Examinez les définitions d’environnement et les domaines associés.

1. Vérifier les scripts de profil pour l’applicabilité

   * Tous les scripts de profil s’exécutent sur chaque appel Target
   * Maintenir l’efficacité des appels en supprimant les scripts non applicables

Pour passer en revue le gestionnaire de balises et le chargement de page :

1. Confirmez les points suivants dans le gestionnaire de balises :

   * Le déploiement du code JavaScript [!DNL Target] attendu
   * La solution de masquage de contenu appropriée
   * Définissez les règles nécessaires pour renseigner les appels [!DNL Target] avec les paramètres attendus

1. Confirmez ce qui suit lors du chargement de la page :

   * Correspondance des numéros de version de l’URL de requête et de l’URL de requête [!DNL Target]
   * Valeur d’ID Experience Cloud renseignée (corps du cloud)
   * Présenter les valeurs d’intégration attendues (corps du cloud)
   * Paramètres de [!DNL Target] renseignés sur les pages appropriées

## [!DNL Target] les activités d’audit

Pour éviter de parcourir manuellement chaque page pour auditer [!DNL Target] activités, utilisez l’auditeur Adobe pour mieux comprendre l’état technique actuel de votre implémentation. Adobe Auditor est optimisé par ObservePoint et peut être configuré pour s’exécuter manuellement, afin d’identifier les problèmes d’implémentation de haut niveau sur votre site.

Adobe Auditor fournit les éléments suivants :

* Une intégrité élevée du site
* Appels rapides pour les problèmes d’implémentation

Adobe recommande d’effectuer des audits manuels mensuels pour :

* Identification des pages non balisées
* Identification des versions incohérentes
* Découvrir les versions obsolètes
* Fournir des informations détaillées qui peuvent être exportées

## Résolution des problèmes courants

>[!NOTE]
>
>Adobe recommande d’installer Adobe Experience Platform Debugger.

Voici des conseils de dépannage généraux pour accéder à l’expérience :

### Cache et cookies**

* Effacement du cache et des cookies
* Faites attention en utilisant le mode privé (par exemple : le mode privé dans Firefox peut bloquer [!DNL Target])

### Êtes-vous qualifié pour l&#39;activité ?

* Vérifiez que vous avez effectué les mêmes étapes que l’audience utilisée dans l’activité
* Utilisez des jetons de `mboxTrace` ou de réponse pour vérifier les valeurs de profil et de segment.

### Conseils généraux de dépannage lors de la validation visuelle/fonctionnelle

Si vous êtes dans l’expérience [!DNL Target] et que vous ne voyez pas l’expérience visuelle attendue :

Vérifiez la réponse [!DNL Target] :

* Si le code n’est pas exécuté :

1. Vérifier les activités en conflit
1. Contactez l’assistance clientèle

* Si le code est exécuté :

1. Retravailler le code dans ce scénario

## Gestion d’un référentiel de connaissances

Un référentiel de connaissances est une plateforme en ligne utilisée pour documenter et partager des informations. Le référentiel de connaissances contient des informations spécifiques à votre implémentation et peut également contenir des informations spécifiques à l’équipe.

Idéalement, le référentiel doit permettre la modification et l’enregistrement automatique dans la plateforme. Une fois qu’il a été initialement configuré, il est facile de le gérer et de le tenir à jour. Le contenu du référentiel de connaissances est traité en fonction des rôles utilisateur.

Les documents standard d’un référentiel de connaissances sont les suivants :

* **Document de présentation** - document utilisé pour expliquer clairement les buts, les objectifs, les processus et la structure du programme
* **Référentiel d’idées** - document utilisé pour gérer et classer par priorité les idées potentielles qui ne sont pas prêtes pour le processus de test.
* **Feuille de route du programme** - Document utilisé pour gérer tous les aspects des activités de test une fois que les idées sont prêtes à démarrer le processus de test
* **Document du plan d’activité** - document utilisé pour décrire les informations nécessaires à la création et au lancement d’activités.
* **Document du plan d’activité** - document utilisé pour communiquer les résultats et les étapes suivantes recommandées aux parties prenantes.
* **Tableau de bord du programme** - Document utilisé pour effectuer le suivi des performances, du rythme et des bénéfices du programme au fil du temps.

Pour plus d’informations, consultez notre [webinaire](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) avec Wilder Freed, consultant senior.

Pour en savoir plus sur la stratégie et le leadership, consultez le hub [Succès client](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html).
