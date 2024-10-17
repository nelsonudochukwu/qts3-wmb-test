<a id="readme-top"></a>
# Documentation de QuickStatements (QS) 3.0

<details>
 <summary>Traductions:</summary>
  <ul>
  <li><a href="/outreachy/qts-index.md">Anglaise</li>
   <li><a href="/outreachy/translations/qts-index-pt.md">
Portugais</li>
    <li><a href="/outreachy/translations/qts-index-es.md">Espagnol</li>
 </ul>
</details>

## Table des Matières

<!-- TABLE DES MATIÈRES -->
<details>
  <summary>Table des Matières</summary>
  <ol>
    <li><a href="#Aperçu">Aperçu de QuickStatements</a></li>
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

Cette documentation propose une introduction aux fonctionnalités, à l'utilisation et aux meilleures pratiques de QuickStatements 3.0. _[Cliquez](#qs-v3-docs)_ pour commencer. Cependant, pour bien comprendre les fonctionnalités de QuickStatements 3.0, il est important de comprendre d'abord le principal constituant de QuickStatements - ```Wikidata.```

#

<a id="a-brief-on-wikidata"></a>
<details>
 <summary>Un Bref Aperçu de Wikidata</summary>
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

</details>
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

<a id="qs-v3-docs"></a>
## Documentation QuickStatements 3.0

Cette documentation propose une introduction aux fonctionnalités de QuickStatements 3.0, qui est une mise à jour améliorant la fonctionnalité, les performances et l'expérience utilisateur de la plateforme QuickStatements pour améliorer la stabilité du système.

#

### Prérequis
Pour créer et exécuter des lots, vous devez vous assurer des éléments suivants :
- **Compte Wikidata** : Vous devez être connecté à Wikidata pour utiliser QuickStatements.
- **Données structurées** : Vos données doivent être bien structurées au format CSV/TSV ou similaire pour être facilement importées et traitées.
- **Utilisateur autoconfirmé** : Pour être un utilisateur autoconfirmé, vous devez être inscrit depuis 4 jours sur la plateforme et avoir effectué 50 modifications.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="qs-3.0-homepage"></a>
## Aperçu de la page d'accueil de QuickStatements 3.0

La page d'accueil de **QuickStatements 3.0** est conçue pour faciliter l'accès aux fonctionnalités principales de gestion et d'exécution des modifications en masse. Voici un aperçu des éléments visibles:

<p align="center">
  <img src="https://github.com/user-attachments/assets/476030c9-efb0-4967-b01c-b6c3586f49dc" alt="QuickStatements 3.0 Homepage" />
  <p align="center">Page d'accueil de QuickStatements 3.0</p>
</p>

#### Section d'en-tête :
1. **Nouveau lot :** Un lien qui vous dirige vers un formulaire où vous pouvez créer un nouveau lot de modifications à télécharger sur Wikidata.
  
2. **Derniers lots :** Ce lien donne accès à l'historique des lots récemment soumis. Les utilisateurs peuvent suivre l'état et les détails de leurs opérations de lots passées.

3. **Git :** Un lien vers le [dépôt GitHub de QuickStatements](https://github.com/WikiMovimentoBrasil/quickstatements3), où les utilisateurs peuvent consulter le code, signaler des problèmes ou contribuer au développement de la plateforme.
  
4. **Connexion :** Permet aux utilisateurs de se connecter à leur compte Wikidata. Une fois connectés, les utilisateurs peuvent accéder à des fonctionnalités comme la soumission et le suivi de leurs lots soumis.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#### Interface principale :
5. **"Bienvenue dans QuickStatements 3.0" :** Un en-tête accueillant les utilisateurs sur l'interface principale.

#### Boutons d'action principaux :

6. **Nouveau lot :** Cliquer sur ce bouton lance la création d'un nouveau lot. Les utilisateurs peuvent saisir des données et des commandes pour traiter et télécharger plusieurs modifications en masse sur Wikidata.
  
#### Section de Recherche de Lot :
7. **ID de Lot :** Les utilisateurs peuvent saisir un identifiant de lot spécifique pour récupérer des informations détaillées sur ce lot particulier. Cliquer sur le bouton ```Voir les détails du lot``` montre l'état, la progression et les résultats du lot.

8. **Nom d'utilisateur :** Les utilisateurs peuvent entrer un nom d'utilisateur Wikidata spécifique pour récupérer une liste de tous les lots associés à cet utilisateur. Cliquer sur ```Voir les lots par utilisateur``` affichera tous les lots soumis par cet utilisateur.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#
  
<a id="what-is-a-batch"></a>
### Qu'est-ce qu'un lot dans QuickStatements ?
Un **lot** désigne un ensemble de commandes ou d'opérations exécutées ensemble pour effectuer des modifications en masse. Chaque lot peut inclure plusieurs déclarations ou affirmations que vous souhaitez ajouter, modifier ou supprimer d'éléments sur Wikidata.

#

<a id="create-new-batch"></a>
#### A. Créer un nouveau lot dans QuickStatements
Pour créer un nouveau lot dans QuickStatements, suivez ces étapes :
1. Cliquez sur le bouton ```Nouveau lot``` situé sur la page d'accueil

<p align="center">
  <img src="https://github.com/user-attachments/assets/97e40a11-34a4-489c-8a22-5f5b5aeef792" alt="Détails d'un Nouveau Lot" />
  <p align="center">Détails d'un Nouveau Lot</p>
</p>

2. Un formulaire apparaîtra où vous pourrez saisir vos commandes ou télécharger votre fichier de données. Les formats disponibles incluent le format QuickStatements V1 ainsi que les formats CSV/TSV.
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

<a id="details-of-a-batch"></a>
#### B. Détails d'un lot dans QuickStatements

<p align="center">
  <img src="https://github.com/user-attachments/assets/e79d7d84-a162-47ac-87f0-739ceb36afa8" alt="Détails d'un Nouveau Lot" />
  <p align="center">Détails d'un Nouveau Lot</p>
</p>
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

Un nouveau lot se compose de :

1. **Format de commande :** Votre format de commande peut être au format V1 ou CSV.
     - **Format V1 :** Format basé sur des commandes où chaque ligne représente une commande séparée par des tabulations.
     - **Format CSV :** Composé d'une première ligne - l'en-tête - qui définit le contenu de chaque colonne. Les lignes suivantes fournissent des informations à appliquer à Wikibase selon le contenu de chaque colonne d'en-tête.
  
Exemple de syntaxe V1:
```
CREATE LAST Len Doctor Worm LAST Den 1998 song performed by They Might Be Giants LAST P2650 Q128309
```
Exemple de syntaxe CSV :
```
qid,Len,Den,P2650,
Doctor Worm,1998 song performed by They Might Be Giants,Q128309
```

2. **Nom de lot personnalisé :** C'est un label ou un identifiant que vous pouvez attribuer à un lot spécifique de modifications pour une gestion et une référence plus facile. Par défaut, les lots sont nommés de manière générique, généralement juste un identifiant de lot. Cependant, vous avez la possibilité de fournir un nom personnalisé lors de la création ou du téléchargement d'un lot. Ce nom personnalisé facilite la reconnaissance ou le rappel de l'objectif d'un lot particulier, en particulier lorsqu'il s'agit de plusieurs lots au fil du temps.

3. **Commandes** : Ce sont les instructions que vous saisissez pour effectuer des opérations spécifiques sur les éléments Wikidata. Ces commandes vous permettent d'ajouter, de modifier ou de supprimer des données des éléments de Wikidata. Les commandes sont écrites dans un format spécifique, et chaque ligne représente généralement une action à effectuer sur un élément Wikidata.
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

## Voir les Détails et l'Historique d'un Lot
Vous pouvez suivre la progression et l'état d'un lot spécifique en saisissant l'**ID de lot** dans le champ approprié et en cliquant sur le bouton **Voir les détails du lot**. Cela affiche des informations telles que le nombre de modifications effectuées, le succès ou l'échec des opérations, et les erreurs éventuelles.

#

<a id="batches-per-user"></a>
#### C. Voir tous les lots par utilisateur dans QuickStatements
Pour voir l'historique des modifications en lot par un utilisateur spécifique :
1. Saisissez le ```nom d'utilisateur``` de l'utilisateur dans le champ de nom d'utilisateur (le nom d'utilisateur peut être trouvé lors de la connexion à Wikidata.)
2. Cliquez sur ```Voir les lots par utilisateur``` pour afficher la liste de tous les lots soumis par cet utilisateur. La liste inclura :
   - **Identifiants de lot**
   - **Descriptions (si vous avez ajouté des noms personnalisés)**
   - **État (par exemple, en cours, terminé ou échoué)**
   - **Dates**
   - **Nombre de modifications dans le lot**

> [!NOTE]
> Chaque lot a une URL unique qui lui est associée. Vous pouvez ajouter cette URL aux favoris ou la partager pour accéder ou surveiller un lot ultérieurement.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

#

<a id="writing-batch-commands"></a>
#### D. Écrire des commandes de lot dans QuickStatements

<a id="create-new-item"></a>
#### 1. Créer un nouvel élément

Cette commande créera un nouvel élément avec un libellé et une description.

```plaintext
CREATE
LAST|Len|"Élément d'exemple"
LAST|Den|"Ceci est un élément d'exemple à des fins de démonstration."
LAST|P31|Q5  # Ajoute une déclaration indiquant que l'élément est une instance d'un humain
```

<a id="add-statements"></a>
#### 2. Ajouter des déclarations (affirmations)
Ajout de déclarations à un élément existant (par exemple, Douglas Adams - Q42).

```
Q42|P569|1952-03-11  # Ajoute la date de naissance (P569) pour Douglas Adams
Q42|P19|Q84          # Ajoute le lieu de naissance (P19) comme Cambridge (Q84)
```

<a id="add-qualifiers"></a>
#### 3. Ajouter des qualificateurs
Vous pouvez ajouter des qualificateurs aux déclarations existantes pour donner plus de détails.
```
Q42|P69|Q3918|P580|1971|P582|1974  # Ajoute l'éducation (P69) au St John's College (Q3918) avec des dates de début (P580) et de fin (P582)
```
<p align="right">(<a href="#readme-top">retour en haut</a>)</p>
<a id="add-references"></a>

#### 4. Ajouter des références
Ajouter des références à une déclaration existante:
```
Q42|P69|Q3918|S854|"https://example.com/education"  # Ajoute une référence URL pour la déclaration d'éducation
```

<a id="modify-lda"></a>
#### 5. Modifier les Libellés, Descriptions et Alias
Modifier les libellés, descriptions et alias dans différentes langues:
```
Q42|Len|"Douglas Adams"  # Modifie le libellé anglais en "Douglas Adams"
Q42|Lde|"Douglas Adams"  # Modifie le libellé allemand en "Douglas Adams"
Q42|Aen|"Douglas Noël Adams"  # Ajoute un alias en anglais
Q42|Den|"Auteur et scénariste britannique"  # Modifie la description anglaise
```

<a id="remove-items"></a>
#### 6. Supprimer des Déclarations ou des Éléments
Supprimer des déclarations ou supprimer des éléments entièrement:
```
Q42|P19|DELETE  # Supprime la déclaration de lieu de naissance (P19) pour Q42
Q100000|DELETE  # Supprime entièrement l'élément Q100000
```

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

<a id="import-data"></a>
#### 7. Importer des Données CSV/TSV
Vous pouvez préparer vos données au format CSV ou TSV, où chaque ligne représente une opération. Exemple de format:
```
Q42,P69,Q3918,P580,1971,P582,1974
Q42,P19,Q84
Q42,P569,1952-03-11
```
Téléchargez le fichier via l'interface web pour traiter le lot.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

## Bonnes Pratiques
- **Tester avec des Petits Lots:** Testez toujours vos commandes avec un petit ensemble d'éléments avant de faire des modifications à grande échelle pour éviter des changements non désirés.
- **Utiliser des Références:** Assurez-vous que les déclarations sont correctement sourcées avec des références pour améliorer la qualité des données.
- **Suivre la Progression:** Après soumission, suivez la progression de votre lot et vérifiez les erreurs.

## Gestion des Erreurs
Lorsqu'une erreur survient lors de l'exécution, QuickStatements indiquera quelle commande a échoué. Les problèmes courants incluent :

- Identifiants d'éléments ou de propriétés incorrects.
- Erreurs de syntaxe dans les formats de date ou champs de données manquants.
- Permissions ou limitations imposées par Wikidata pour les modifications en masse. Dans ces cas, révisez les commandes échouées et corrigez les problèmes avant de les exécuter à nouveau.

<p align="right">(<a href="#readme-top">retour en haut</a>)</p>

## En Conclusion
QuickStatements est un outil essentiel pour les modifications en masse sur Wikidata, permettant aux utilisateurs de gérer efficacement de grands ensembles de données. En suivant ce guide, vous pouvez créer, mettre à jour et gérer des éléments avec facilité, améliorant ainsi la qualité et l'exactitude des données sur Wikidata.

Pour des cas d'utilisation plus avancés, consultez la [documentation Wikidata](https://www.wikidata.org/wiki/Help:QuickStatements) pour plus de détails et de mises à jour.

## Références
Cette documentation s'inspire de nombreuses sources, cependant, [Diátaxis](https://diataxis.fr/) a été le guide le plus important pour l'écriture de ce document car il propose une approche systématique pour comprendre les besoins des utilisateurs de documentation. Le [cours de rédaction technique de Google](https://developers.google.com/tech-writing/overview) a également été très utile.

️💚️ MERCI MENTORS 💙
<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore -->
| [<img src="https://github.com/user-attachments/assets/1deb350c-3202-48b3-bef2-ead6c6f9a06d" width="100px;"/><br /><sub><b>Ederporto, EPorto (WMB)</b></sub>](https://phabricator.wikimedia.org/p/Ederporto/)<br />        | [<img src="https://github.com/user-attachments/assets/4d0112e0-00b8-421d-a043-67282f13d413" width="100px;"/><br /><sub><b>Artur Corrêa Souza</b></sub>](https://phabricator.wikimedia.org/p/ACorrea-WMB/)<br /> | [<img src="https://github.com/user-attachments/assets/b8c0a206-9e85-4b2c-a41d-13986e126565" width="100px;"/><br /><sub><b>MGalves (WMB)</b></sub>](https://phabricator.wikimedia.org/p/MGalves_WMB/)<br />          |
| :---------------------: | :-----------------------: | :--------------------: |
<p align="right">(<a href="#readme-top">back to top</a>)</p>
<!-- ALL-CONTRIBUTORS-LIST:END -->


