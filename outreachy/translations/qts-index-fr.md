<a id="readme-top"></a>
# Documentation de QuickStatements (QS) 3.0

<details>
 <summary>Traductions !!!!</summary>
</details>

## Table des Matières

<!-- TABLE DES MATIÈRES -->
<details>
  <summary>Table des Matières</summary>
  <ol>
    <li><a href="#overview">Aperçu de QuickStatements</a></li>
    <li><a href="#a-brief-on-wikidata">Un Bref Aperçu de Wikidata</a>
      <ul>
        <li><a href="#structure-of-wikidata">Structure de Wikidata</a></li>
        <li><a href="#lda">Libellés, descriptions et alias</a></li>
        <li><a href="#wiki-statements">Déclarations Wikidata</a></li>
        <li><a href="#syntax-and-command-structure">Syntaxe et Structure des Commandes</a></li>
      </ul>
    </li>
    <li><a href="#qs-v3-docs">Documentation QuickStatements 3.0</a>
      <ul>
        <li><a href="#prerequisites">Commencer : Prérequis</a></li>
        <li><a href="#qs-3.0-homepage">Aperçu de la page d'accueil de QuickStatements 3.0</a></li>
        <li><a href="#what-is-a-batch">Guides : Qu'est-ce qu'un lot ?</a>
          <ul>
            <li><a href="#create-new-batch">Créer un nouveau lot</a></li>
            <li><a href="#details-of-a-batch">Détails d'un lot</a></li>
          </ul>
        </li>
        <li><a href="#batch-details">Voir les Détails et l'Historique d'un Lot</a></li>
        <li><a href="#batches-per-user">Voir tous les lots créés par un utilisateur</a></li>
        <li><a href="#writing-batch-commands">Écrire des commandes de lot</a>
          <ul>
            <li><a href="#create-new-item">Créer un nouvel élément</a></li>
            <li><a href="#add-statements">Ajouter des déclarations</a></li>
            <li><a href="#add-qualifiers">Ajouter des qualificateurs</a></li>
            <li><a href="#add-references">Ajouter des références</a></li>
            <li><a href="#modify-lda">Modifier les libellés, descriptions et alias</a></li>
            <li><a href="#remove-items">Supprimer des déclarations ou des éléments</a></li>
            <li><a href="#import-data">Importer des données CSV/TSV</a></ul>
        </li>
        <li><a href="#best-practices">Bonnes Pratiques</a></li>
        <li><a href="#error-handling">Gestion des Erreurs</a></li>
        <li><a href="#recommendations">Recommandations</a></li>
        <li><a href="#conclusion">Conclusion</a></li>
      </ul>
    </li> 
  </ol>
</details>

## Aperçu

**QuickStatements (QS)** est un outil puissant conçu par [Magnus Manske](https://en.wikipedia.org/wiki/User:Magnus_Manske) pour effectuer des modifications en masse sur Wikidata. Il permet aux utilisateurs d'ajouter, de modifier ou de supprimer de grandes quantités de données efficacement, en utilisant une syntaxe simple semblable à une ligne de commande. Que vous ajoutiez de nouveaux éléments, des déclarations ou que vous mettiez à jour des propriétés sur plusieurs entités, QuickStatements est un outil essentiel pour les éditeurs de Wikidata qui doivent effectuer des modifications à grande échelle rapidement et de manière fiable.

Cette documentation propose une introduction aux fonctionnalités, à l'utilisation et aux meilleures pratiques de QuickStatements 3.0. _[Cliquez](#qs-v3-docs)_ pour commencer. Cependant, pour bien comprendre les fonctionnalités de QuickStatements 3.0, il est important de comprendre d'abord le principal constituant de QuickStatements - _Wikidata_.

## Un Bref Aperçu de Wikidata
Wikidata est une base de données collaborative, multilingue et gratuite, gérée par la Fondation Wikimedia. Elle sert de stockage central pour des données structurées utilisées dans divers projets Wikimedia, comme Wikipédia, et fournit également des données aux utilisateurs et organisations externes. L'objectif principal de Wikidata est de permettre aux humains et aux machines de comprendre et d'interroger facilement les informations.

Quelques fonctionnalités clés :

- **Support multilingue** : Les données sont stockées de manière à pouvoir être consultées dans n'importe quelle langue.
- **Données ouvertes** : Les données de Wikidata sont disponibles sous la licence Creative Commons Public Domain Dedication (CC0).
- **Édition collaborative** : Toute personne ayant un compte peut modifier Wikidata, ce qui en fait une ressource communautaire.
- **Liens de données** : Wikidata s'intègre aux autres projets Wikimedia, servant de source de données cohérente et à jour.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="structure-of-wikidata"></a>
## Structure de Wikidata
La structure de Wikidata est basée sur un modèle simple mais puissant composé d'**éléments**, de **propriétés** et de **valeurs**. Ces trois composants forment la base de la manière dont les données sont stockées, liées et récupérées.

- **Éléments (numéros Q)** : Chaque élément est un concept unique représenté par un **QID** (par exemple, Douglas Adams est représenté par Q42). Ces éléments stockent des données et se lient à d'autres éléments.

- **Propriétés (numéros P)** : Les propriétés décrivent des attributs spécifiques d'un élément et sont identifiées par des **PIDs** (par exemple, la date de naissance est représentée par **P569**). Les propriétés peuvent décrire des relations entre des éléments ou entre un élément et une valeur de données.

- **Valeurs** : Ce sont les points de données réels (par exemple, la date **1952-03-11** comme valeur pour **P569** sur l'élément **Q42** pour la date de naissance de Douglas Adams).

Ensemble, les éléments, les propriétés et les valeurs créent des **déclarations**, qui sont les éléments constitutifs de Wikidata.

<a id="lda"></a>
## Libellés, Descriptions et Alias
Chaque élément de Wikidata peut avoir plusieurs **libellés**, **descriptions** et **alias** dans différentes langues :

- **Libellés** : Un libellé est le nom principal d'un élément (par exemple, « Douglas Adams » pour **Q42**). Un élément peut avoir un libellé différent dans chaque langue.

- **Descriptions** : Les descriptions fournissent un contexte sur l'élément pour le différencier des éléments similaires (par exemple, « auteur et scénariste britannique » pour **Q42**).

- **Alias** : Les alias sont des noms alternatifs pour un élément utilisés pour des recherches. Par exemple, **Q42** (Douglas Adams) pourrait avoir un alias comme "Douglas Noël Adams."

Ces trois composants permettent de s'assurer que les éléments sont faciles à trouver, à distinguer et à accéder dans une variété de langues et de contextes.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="wiki-statements"></a>
## Déclarations Wikidata
Les **déclarations** sont les unités de base de la connaissance dans Wikidata, utilisées pour décrire des éléments par une combinaison d'une propriété et d'une valeur. Une déclaration relie un élément à ses données associées :

- **Propriété** : Définit l'aspect de l'élément que vous décrivez (par exemple, date de naissance, profession, nationalité).
- **Valeur** : Fournit l'information spécifique (par exemple, une date, une chaîne, ou une référence à un autre élément).
Une déclaration peut également avoir des **qualificatifs** et des **références** pour fournir plus de contexte ou citer la source des données.

Par exemple :

- **Élément** : Douglas Adams (Q42)
- **Propriété** : Date de naissance (P569)
- **Valeur** : 11 mars 1952
- **Qualificatif** : Source (S854) – Lien vers une page Web ou une base de données fournissant la preuve de la déclaration.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="syntax-and-command-structure"></a>
## Syntaxe et Structure des Commandes

Chaque commande QuickStatements suit un format simplifié avec des colonnes spécifiant l'**élément**, la **propriété**, la **valeur**, et des **qualificatifs**, **références**, etc. optionnels.

| Champ        | Description                                                                                     |
|--------------|-------------------------------------------------------------------------------------------------|
| `Q####`      | Fait référence à un élément (par exemple, `Q42` pour Douglas Adams).                                               |
| `P####`      | Fait référence à une propriété (par exemple, `P31` pour "instance de").                                            |
| Valeur       | La valeur associée à la propriété. Cela peut être une référence à un élément (par exemple, `Q####`), une chaîne, un nombre, etc. |
| Qualificatif | Informations supplémentaires ajoutées à une déclaration pour lui donner plus de contexte (par exemple, temps, lieu).             |
| Références   | Données pour soutenir une déclaration (par exemple, une URL, une date de publication).                                         |
| Libellés     | Noms ou titres d'éléments dans différentes langues.                                                 |
| Descriptions | Résumés brefs qui décrivent les éléments.                                                         |
| Alias        | Noms alternatifs ou termes par lesquels un élément est connu.                                              |

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="qs-v3-docs"></a>
## Documentation QuickStatements 3.0

Cette documentation propose une introduction aux fonctionnalités de QuickStatements 3.0, qui est une mise à jour améliorant la fonctionnalité, les performances et l'expérience utilisateur de la plateforme QuickStatements pour améliorer la stabilité du système.

#

### Prérequis
Pour créer et exécuter des lots, vous devez vous assurer des éléments suivants :
- **Compte Wikidata** : Vous devez être connecté à Wikidata pour utiliser QuickStatements.
- **Données structurées** : Vos données doivent être bien structurées au format CSV/TSV ou similaire pour être facilement importées et traitées.
- **Utilisateur autoconfirmé** : Pour être un utilisateur autoconfirmé, vous devez être inscrit depuis 4 jours sur la plateforme et avoir effectué 50 modifications.

<a id="qs-3.0-homepage"></a>
## Aperçu de la page d'accueil de QuickStatements 3.0

La page d'accueil de **QuickStatements 3.0** est conçue pour faciliter l'accès aux fonctionnalités principales de gestion et d'exécution des modifications en masse. Voici un aperçu des éléments visibles :

#### Section d'en-tête :
- **Nouveau lot :** Un lien qui vous dirige vers un formulaire où vous pouvez créer un nouveau lot de modifications à télécharger sur Wikidata.
- **Derniers lots :** Ce lien donne accès à l'historique des lots récemment soumis. Les utilisateurs peuvent suivre l'état et les détails de leurs opérations de lots passées.

- **Git :** Un lien vers le dépôt GitHub de QuickStatements, où les utilisateurs peuvent consulter le code, signaler des problèmes ou contribuer au développement de la plateforme.
  
- **Connexion :** Permet aux utilisateurs de se connecter à leur compte Wikidata. Une fois connectés, les utilisateurs peuvent accéder à des fonctionnalités comme la soumission et le suivi de leurs lots soumis.
  
#### Interface principale :
- **"Bienvenue dans QuickStatements 3.0" :** Un en-tête accueillant les utilisateurs sur l'interface principale.

#### Boutons d'action principaux :

- **Nouveau lot :** Cliquer sur ce bouton lance la création d'un nouveau lot. Les utilisateurs peuvent saisir des données et des commandes pour traiter et télécharger plusieurs modifications en masse sur Wikidata.
  
#### Section de Recherche de Lot :
- **ID de Lot :** Les utilisateurs peuvent saisir un identifiant de lot spécifique pour récupérer des informations détaillées sur ce lot particulier. Cliquer sur le bouton **"Voir les détails du lot"** montre l'état, la progression et les résultats du lot.

- **Nom d'utilisateur :** Les utilisateurs peuvent entrer un nom d'utilisateur Wikidata spécifique pour récupérer une liste de tous les lots associés à cet utilisateur. Cliquer sur **"Voir les lots par utilisateur"** affichera tous les lots soumis par cet utilisateur.

#
  
<a id="what-is-a-batch"></a>
### Qu'est-ce qu'un lot dans QuickStatements ?
Un **lot** désigne un ensemble de commandes ou d'opérations exécutées ensemble pour effectuer des modifications en masse. Chaque lot peut inclure plusieurs déclarations ou affirmations que vous souhaitez ajouter, modifier ou supprimer d'éléments sur Wikidata.

#

<a id="create-new-batch"></a>
#### A. Créer un nouveau lot dans QuickStatements
Pour créer un nouveau lot dans QuickStatements, suivez ces étapes :
1. Cliquez sur le bouton **Nouveau lot** situé sur la page d'accueil

![Screenshot 2024-10-15 at 19 03 34](https://github.com/user-attachments/assets/67129eef-b4b9-4e37-bf97-5c85e351bea8)

2. Un formulaire apparaîtra où vous pourrez saisir vos commandes ou télécharger votre fichier de données. Les formats disponibles incluent le format QuickStatements V1 ainsi que les formats CSV/TSV.
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

<a id="details-of-a-batch"></a>
#### B. Détails d'un lot dans QuickStatements
![Screenshot 2024-10-15 at 19 04 43](https://github.com/user-attachments/assets/0c48dbe9-9ad2-4966-acad-aee0437bd880)
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

Un nouveau lot se compose de :
- **Format de commande :** Votre format de commande peut être au format V1 ou CSV.
  - **Format V1 :** Format basé sur des commandes où chaque ligne représente une commande séparée par des tabulations.
  - **Format CSV :** Composé d'une première ligne - l'en-tête - qui définit le contenu de chaque colonne. Les lignes suivantes fournissent des informations à appliquer à Wikibase selon le contenu de chaque colonne d'en-tête.
  
  Exemple de syntaxe V1 :
