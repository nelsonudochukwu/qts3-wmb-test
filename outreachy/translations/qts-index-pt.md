<a id="readme-top"></a>
# QuickStatements (QS) 3.0 Documentation

<details>
 <summary>Traductions!!!!</summary>
 <ul>
  <li><a href="https://github.com/nelsonudochukwu/qts3-wmb-test/blob/main/outreachy/qts-index.md">
Inglês</li>
  <li><a href="/outreachy/translations/qts-index-fr.md">Français</li>
   <li><a href="/outreachy/translations/qts-index-es.md">Espagnol</li>
 </ul>
</details>

## Table des Matières
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table des Matières</summary>
  <ol>
    <li><a href="#overview">Vue d'ensemble de QuickStatements</a></li>
    <li><a href="#a-brief-on-wikidata">Aperçu de Wikidata</a>
      <ul>
        <li><a href="#structure-of-wikidata">Structure de Wikidata</a></li>
        <li><a href="#lda">Étiquettes, descriptions et alias</a></li>
        <li><a href="#wiki-statements">Déclarations Wikidata</a></li>
        <li><a href="#syntax-and-command-structure">Syntaxe et Structure des Commandes</a></li>
      </ul>
    </li>
    <li><a href="#qs-v3-docs">Docs QuickStatements 3.0</a>
      <ul>
        <li><a href="#prerequisites">Commencer : Prérequis</a></li>
        <li><a href="#qs-3.0-homepage">Vue d'ensemble de la page d'accueil de QuickStatements 3.0</a></li>
        <li><a href="#what-is-a-batch">Comment faire : Qu'est-ce qu'un lot ?</a>
          <ul>
            <li><a href="#create-new-batch">Créer un Nouveau Lot</a></li>
            <li><a href="#details-of-a-batch">Détails d'un Lot</a></li>
          </ul>
        </li>
        <li><a href="#batch-details">Voir les Détails et l'Historique d'un Lot</a></li>
        <li><a href="#batches-per-user">Voir tous les Lots créés par un Utilisateur</a></li>
        <li><a href="#writing-batch-commands">Écrire des Commandes de Lot</a>
          <ul>
            <li><a href="#create-new-item">Créer un Nouvel Élément</a>
            <li><a href="#add-statements">Ajouter des Déclarations</a>
            <li><a href="#add-qualifiers">Ajouter des Qualificatifs</a> 
            <li><a href="#add-references">Ajouter des Références</a>
            <li><a href="#modify-lda">Modifier les Étiquettes, Descriptions, et Alias</a>
            <li><a href="#remove-items">Supprimer des Déclarations ou des Éléments</a>
            <li><a href="#import-data">Importer des Données CSV/TSV</a>                                                                  </ul>
        </li>
        <li><a href="#best-practices">Bonnes Pratiques</a></li>
        <li><a href="#error-handling">Gestion des Erreurs</a></li>
        <li><a href="#recommendations">Recommandations</a></li>
        <li><a href="#conclusion">Conclusion</a></li>
      </ul>
    </li> 
  </ol>
</details>

## Vue d'ensemble

**QuickStatements (QS)** est un outil puissant conçu par [Magnus Manske](https://en.wikipedia.org/wiki/User:Magnus_Manske) pour effectuer des modifications en masse sur Wikidata. Il permet aux utilisateurs d'ajouter, de modifier ou de supprimer de grandes quantités de données efficacement, en utilisant une syntaxe simple similaire à celle d'une ligne de commande. Que vous ajoutiez de nouveaux éléments, des déclarations ou que vous mettiez à jour des propriétés sur plusieurs entités, QuickStatements est un outil essentiel pour les éditeurs de Wikidata qui doivent effectuer des changements à grande échelle rapidement et de manière fiable.

Cette documentation fournit une introduction aux fonctionnalités, à l'utilisation et aux bonnes pratiques de QuickStatements 3.0. _[Cliquez](#qs-v3-docs)_ pour plonger directement dans le sujet. Cependant, pour bien comprendre les fonctionnalités de QuickStatements 3.0, il est important de d'abord comprendre le composant principal de QuickStatements⎯ _Wikidata._

#

<a id="a-brief-on-wikidata"></a>
<details>
 <summary> Aperçu de Wikidata</summary>
Wikidata est une base de données secondaire, gratuite, collaborative et multilingue, gérée par la Fondation Wikimedia. Elle sert de stockage centralisé pour les données structurées utilisées dans divers projets Wikimedia, comme Wikipédia, et fournit également des données à des utilisateurs et organisations externes. L'objectif principal de Wikidata est de permettre aux humains et aux machines de comprendre et de requêter facilement des informations.

Quelques caractéristiques clés:

- **Support multilingue:** Les données sont stockées de manière à pouvoir être accessibles dans n'importe quelle langue.
- **Données ouvertes:** Les données de Wikidata sont librement disponibles sous la licence de dédication au domaine public Creative Commons (CC0).
- **Édition collaborative :** Toute personne ayant un compte peut éditer Wikidata, ce qui en fait une ressource communautaire.
- **Données liées:** Wikidata s'intègre à d'autres projets Wikimedia, servant de source de données cohérente et à jour.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="structure-of-wikidata"></a>
## Structure de Wikidata
La structure de Wikidata repose sur un modèle simple mais puissant d'**éléments**, de **propriétés** et de **valeurs**. Ces trois composants forment l'épine dorsale de la manière dont les données sont stockées, liées et récupérées.

- **Éléments (numéros Q):** Chaque élément est un concept unique représenté par un **QID** (par exemple, Douglas Adams est représenté par Q42). Ces éléments stockent des données et sont liés à d'autres éléments.

- **Propriétés (numéros P):** Les propriétés décrivent des attributs spécifiques d'un élément et sont identifiées par des **PID** (par exemple, la date de naissance est représentée par **P569**). Les propriétés peuvent décrire des relations entre des éléments ou entre un élément et une valeur de données.

- **Valeurs:** Ce sont les données réelles (par exemple, la date **1952-03-11** en tant que valeur pour **P569** sur l'élément **Q42** pour la date de naissance de Douglas Adams).

Ensemble, les éléments, les propriétés et les valeurs créent des **déclarations**, qui sont les unités de base de Wikidata.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="lda"></a>
## Étiquettes, Descriptions et Alias
Chaque élément dans Wikidata peut avoir plusieurs **étiquettes**, **descriptions** et **alias** dans différentes langues :

- **Étiquettes:** Une étiquette est le nom principal d'un élément (par exemple, "Douglas Adams" pour **Q42**). Un élément peut avoir une étiquette différente dans chaque langue.

- **Descriptions:** Les descriptions fournissent un contexte sur l'élément pour le différencier d'éléments similaires (par exemple, "Auteur et scénariste britannique" pour **Q42**).

- **Alias:** Les alias sont des noms alternatifs pour un élément utilisés à des fins de recherche. Par exemple, **Q42** (Douglas Adams) pourrait avoir un alias comme "Douglas Noel Adams."

Ces trois composants aident à s'assurer que les éléments sont faciles à trouver, à distinguer et à accéder dans une variété de langues et de contextes.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="wiki-statements"></a>
## Déclarations Wikidata
Les **Déclarations** sont les unités de connaissances centrales dans Wikidata, utilisées pour décrire des éléments via une combinaison d'une propriété et d'une valeur. Une déclaration relie un élément à ses données associées :

- **Propriété :** Définit quel aspect de l'élément vous décrivez (par exemple, date de naissance, profession, nationalité).
- **Valeur :** Fournit l'information spécifique (par exemple, une date, une chaîne de caractères ou une référence à un autre élément).
Une déclaration peut également avoir des **qualificatifs** et des **références** pour fournir plus de contexte ou citer la source des données.

Par exemple :

- **Élément :** Douglas Adams (Q42)
- **Propriété :** Date de naissance (P569)
- **Valeur :** 11 mars 1952
- **Qualificatif :** Source (S854) – Lien vers une page web ou une base de données fournissant la preuve de la déclaration.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="syntax-and-command-structure"></a>
## Syntaxe et Structure des Commandes

Chaque commande QuickStatements suit un format simplifié avec des colonnes spécifiant l'**Élément**, la **Propriété**, la **Valeur** et des **Qualificatifs**, **Références** optionnels, etc.

| Champ        | Description                                                                                     |
|--------------|-------------------------------------------------------------------------------------------------|
| `Q####`      | Fait référence à un élément (par exemple, `Q42` pour Douglas Adams).                                               |
| `P####`      | Fait référence à une propriété (par exemple, `P31` pour "instance de").                                            |
| Valeur        | La valeur associée à la propriété. Peut être une référence à un élément (par exemple, `Q####`), chaîne, nombre, etc. |
| Qualificatif    | Information supplémentaire ajoutée à une déclaration pour lui donner plus de contexte (par exemple, temps, lieu).             |
| Références   | Données pour appuyer une déclaration (par exemple, une URL, date de publication).                                         |
| Étiquettes       | Noms ou titres des éléments dans différentes langues.                                                 |
| Descriptions | Résumés succincts qui décrivent les éléments.                                                         |
| Alias      | Noms alternatifs ou termes par lesquels un élément est connu.                                              |

</details>

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

<a id="qs-v3-docs"></a>
## Docs QuickStatements 3.0

Cette documentation fournit une introduction aux fonctionnalités de QuickStatements 3.0, une mise à niveau qui améliore la fonctionnalité, les performances et l'expérience utilisateur de la plateforme QuickStatements pour améliorer la stabilité du système.

#

### Prérequis
Pour créer et exécuter des lots, vous devez vous assurer des points suivants :
- **Compte Wikidata :** Vous devez être connecté à Wikidata pour utiliser QuickStatements.
- **Données structurées :** Vos données doivent être bien structurées au format CSV/TSV ou similaire pour être facilement importées et traitées.
- **Utilisateur autoconfirmé :** Pour être autoconfirmé, vous devez avoir un compte actif depuis 4 jours sur la plateforme et avoir effectué 50 modifications.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="qs-3.0-homepage"></a>
## Vue d'ensemble de la page d'accueil de QuickStatements 3.0

La page d'accueil de **QuickStatements 3.0** est conçue pour faciliter l'accès aux fonctionnalités principales de gestion et d'exécution des modifications en lot. Voici un aperçu des éléments visibles :

#### Section d'en-tête:
- **Nouveau lot:** Un lien qui vous mène à un formulaire où vous pouvez créer un nouveau lot de modifications à télécharger sur Wikidata.
- **Derniers lots:** Ce lien permet d'accéder à l'historique des lots récemment soumis. Les utilisateurs peuvent suivre le statut et les détails de leurs opérations de lots passées.

- **Git:** Un lien vers le dépôt GitHub de QuickStatements, où les utilisateurs peuvent consulter la base de code, signaler des problèmes ou contribuer au développement de la plateforme.
  
- **Connexion:** Permet aux utilisateurs de se connecter à leurs comptes Wikidata. Une fois connectés, ils peuvent accéder à des fonctionnalités telles que soumettre et suivre leurs lots.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#### Interface principale:
- **“Bienvenue sur QuickStatements 3.0” :** Un en-tête accueillant les utilisateurs sur l'interface principale.

#### Boutons d'action principaux:

- **Nouveau lot:** En cliquant sur ce bouton, vous initiez la création d'un nouveau lot. Les utilisateurs peuvent saisir des données et des commandes pour traiter et télécharger plusieurs modifications en masse sur Wikidata.
  
#### Section de recherche de lot:
- **ID du lot:** Les utilisateurs peuvent entrer un ID de lot spécifique pour récupérer des informations détaillées sur ce lot particulier. En cliquant sur le bouton **“Voir les détails du lot”**, vous pouvez voir le statut, la progression et les résultats du lot.

- **Nom d'utilisateur:** Les utilisateurs peuvent entrer un nom d'utilisateur Wikidata spécifique pour récupérer une liste de tous les lots associés à cet utilisateur. En cliquant sur **“Voir les lots par utilisateur”**, tous les lots soumis par cet utilisateur seront affichés.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#
  
<a id="what-is-a-batch"></a>
### Qu'est-ce qu'un Lot dans QuickStatements?
Un **lot** fait référence à un ensemble de commandes ou d'opérations exécutées ensemble pour effectuer des modifications en masse. Chaque lot peut inclure plusieurs déclarations ou revendications que vous souhaitez ajouter, modifier ou supprimer sur des éléments de Wikidata.

#

<a id="create-new-batch"></a>
#### A. Créer un Nouveau Lot dans QuickStatements
Pour créer un nouveau lot dans QuickStatements, suivez ces étapes:
1. Cliquez sur le bouton **Nouveau Lot** situé sur la page d'accueil
   
![Capture d'écran 2024-10-15 à 19 03 34](https://github.com/user-attachments/assets/67129eef-b4b9-4e37-bf97-5c85e351bea8)

2. Un formulaire apparaîtra où vous pourrez saisir vos commandes ou télécharger votre fichier de données. Les formats disponibles incluent à la fois le format QuickStatements V1 et le format CSV/TSV.
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

<a id="details-of-a-batch"></a>
#### B. Détails d'un Lot dans QuickStatements
![Capture d'écran 2024-10-15 à 19 04 43](https://github.com/user-attachments/assets/0c48dbe9-9ad2-4966-acad-aee0437bd880)
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

Un nouveau lot se compose de:
- **Format de commande :** Votre format de commande peut être au format V1 ou au format CSV.
  - **Format V1:** Format basé sur des commandes où chaque ligne représente une commande séparée par des tabulations.
  - **Format CSV:** Composé d'une première ligne⎯l'en-tête⎯qui définit le contenu de chaque colonne. Les lignes suivantes fournissent les informations à appliquer à Wikibase selon le contenu de l'en-tête de chaque colonne.
  
Exemple de syntaxe V1:
```
CREATE
LAST Len Doctor Worm
LAST Den 1998 song performed by They Might Be Giants
LAST P2650 Q12830
```
Exemple de syntaxe CSV:
```
qid,Len,Den,P265,
Doctor Worm,
1998 song performed by They Might Be Giants,Q128309
```

- **Nom de lot personnalisé:** C'est un libellé ou identifiant que vous pouvez attribuer à un lot spécifique de modifications pour une gestion et une référence plus faciles. Par défaut, les lots sont nommés de manière générique, généralement juste un ID de lot. Cependant, vous avez la possibilité de fournir un nom personnalisé lorsque vous créez ou téléchargez un lot. Ce nom personnalisé permet de reconnaître ou de se souvenir plus facilement de l'intention d'un lot particulier, en particulier lorsqu'il s'agit de plusieurs lots au fil du temps.

- **Commandes:** Ce sont les instructions que vous entrez pour effectuer des opérations spécifiques sur des éléments de Wikidata. Ces commandes vous permettent d'ajouter, de modifier ou de supprimer des données d'éléments dans Wikidata. Les commandes sont écrites dans un format spécifique, et chaque ligne représente généralement une action à entreprendre sur un élément Wikidata.
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

## Voir les Détails et l'Historique d'un Lot
Vous pouvez suivre la progression et le statut d'un lot spécifique en entrant l'**ID de Lot** dans le champ approprié et en cliquant sur le bouton **Voir les détails du lot**. Cela affiche des informations telles que le nombre de modifications effectuées, la réussite ou l'échec des opérations, ainsi que les erreurs survenues.

#

<a id="batches-per-user"></a>
#### C. Voir tous les Lots par Utilisateur dans QuickStatements
Pour voir l'historique des modifications en lot par un utilisateur spécifique:
1. Entrez le **nom d'utilisateur** de l'utilisateur dans le champ nom d'utilisateur (le nom d'utilisateur peut être trouvé à la connexion wiki.)
2. Cliquez sur **Voir les lots par utilisateur** pour lister tous les lots que l'utilisateur a soumis. La liste comprendra:
- **ID de Lots**
- **Descriptions (si vous avez ajouté des noms personnalisés)**
- **Statut (par exemple, en cours, terminé ou échoué)**
- **Dates**
- **Nombre de modifications dans le lot**

> [!NOTE]
> Chaque lot a une URL unique qui lui est associée. Vous pouvez mettre en signet ou partager cette URL pour accéder ou surveiller un lot plus tard.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

<a id="writing-batch-commands"></a>
#### D. Écrire des Commandes de Lot dans QuickStatements

<a id="create-new-item"></a>
#### 1. Créer un Nouvel Élément

Cette commande créera un nouvel élément avec une étiquette et une description.
```
CREATE
LAST|Len|"Élément Exemple"
LAST|Den|"Ceci est un exemple d'élément à des fins de démonstration."
LAST|P31|Q5  # Ajoute une revendication selon laquelle l'élément est une instance d'un humain
```

<a id="add-statements"></a>

#### 2. Ajouter des Déclarations (Revendiquer)
Ajouter des déclarations à un élément existant (par exemple, Douglas Adams - Q42).
```
Q42|P569|1952-03-11  # Ajoute la date de naissance (P569) pour Douglas Adams
Q42|P19|Q84          # Ajoute le lieu de naissance (P19) comme Cambridge (Q84)
```

<a id="add-qualifiers"></a>

#### 3. Ajouter des Qualificatifs
Vous pouvez ajouter des qualificatifs à des déclarations existantes pour fournir plus de détails.
```
Q42|P69|Q3918|P580|1971|P582|1974  # Ajoute l'éducation (P69) au St John's College (Q3918) avec des dates de début (P580) et de fin (P582)
```

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="add-references"></a>
#### 4. Ajouter des Références
Ajouter des références à une déclaration existante:
```
Q42|P69|Q3918|S854|"https://exemple.com/education"  # Ajoute une référence URL pour la revendication d'éducation
```

<a id="modify-lda"></a>
5. Modifier les Étiquettes, Descriptions, et Alias
Modifier les étiquettes, descriptions et alias dans différentes langues:
```
Q42|Len|"Douglas Adams"  # Change l'étiquette anglaise en "Douglas Adams"
Q42|Lde|"Douglas Adams"  # Change l'étiquette allemande en "Douglas Adams"
Q42|Aen|"Douglas Noel Adams"  # Ajoute un alias en anglais
Q42|Den|"Auteur et scénariste britannique"  # Modifie la description anglaise
```

<a id="remove-items"></a>
6. Supprimer des Déclarations ou des Éléments
Supprimer des déclarations ou supprimer entièrement des éléments:
```
Q42|P19|DELETE  # Supprime la déclaration du lieu de naissance (P19) pour Q42
Q100000|DELETE  # Supprime entièrement l'élément Q100000
```

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="import-data"></a>
7. Importer des Données CSV/TSV
Vous pouvez préparer vos données au format CSV ou TSV, où chaque ligne représente une opération. Un format d'exemple:
```
Q42,P69,Q3918,P580,1971,P582,1974
Q42,P19,Q84
Q42,P569,1952-03-11
```

Téléchargez le fichier via l'interface web pour traiter le lot.
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

### Bonnes Pratiques
- **Tester avec des petits lots:** Testez toujours vos commandes avec un petit ensemble d'éléments avant des modifications à grande échelle pour éviter des changements non désirés.
- **Utilisez des Références:** Assurez-vous que les déclarations sont correctement sourcées avec des références pour améliorer la qualité des données.
- **Surveiller la Progression:** Après soumission, suivez la progression de votre lot et vérifiez les erreurs.

#

### Gestion des Erreurs
Lorsqu'une erreur survient pendant l'exécution, QuickStatements indiquera quelle commande a échoué. Les problèmes courants incluent:

- Identifiants d'élément ou de propriété incorrects.
- Erreurs de syntaxe dans les formats de date ou des champs de données manquants.
- Permissions ou limitation par Wikidata pour des modifications à grande échelle. Dans ces cas, revoyez les commandes échouées et corrigez les problèmes avant de les relancer.
  
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#          

### Conclusion
QuickStatements est un outil essentiel pour l'édition en masse sur Wikidata, permettant aux utilisateurs de gérer de grands ensembles de données efficacement. En suivant ce guide, vous pouvez créer, mettre à jour et gérer des éléments avec facilité, améliorant ainsi la qualité et la précision de Wikidata.

Pour des cas d'utilisation plus avancés, consultez la [documentation Wikidata](https://www.wikidata.org/wiki/Help:QuickStatements) pour plus de détails et mises à jour.

# 

### Références
Cette documentation a été inspirée de nombreuses sources, cependant, [Diátaxis](https://developers.google.com/tech-writing/overview) a été le guide le plus significatif pour la rédaction de cette documentation, car il fournit une approche systématique pour comprendre les besoins des utilisateurs de documentation. Le [Cours de Rédaction Technique Google](https://developers.google.com/tech-writing/overview) a également été déterminant.

## 💚️ MERCI MENTORS 💙
<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore -->
| [<img src="https://github.com/user-attachments/assets/1deb350c-3202-48b3-bef2-ead6c6f9a06d" width="100px;"/><br /><sub><b>Ederporto, EPorto (WMB)</b></sub>](https://phabricator.wikimedia.org/p/Ederporto/)<br />        | [<img src="https://github.com/user-attachments/assets/4d0112e0-00b8-421d-a043-67282f13d413" width="100px;"/><br /><sub><b>Artur Corrêa Souza</b></sub>](https://phabricator.wikimedia.org/p/ACorrea-WMB/)<br /> | [<img src="https://github.com/user-attachments/assets/b8c0a206-9e85-4b2c-a41d-13986e126565" width="100px;"/><br /><sub><b>MGalves (WMB)</b></sub>](https://phabricator.wikimedia.org/p/MGalves_WMB/)<br />          |
| :---------------------: | :-----------------------: | :--------------------: |
<p align="right">(<a href="#readme-top">back to top</a>)</p>
<!-- ALL-CONTRIBUTORS-LIST:END -->

