# QuickStatements Documentation

## Table of Contents


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#features">Features</a></li>
    <li><a href="#prerequisites">Prerequisites</a></li>
    <li><a href="#syntax-and-command-structure">Syntax and Command Structure</a></li>
    <li><a href="#usage">Usage</a></li>
    <li>
      <a href="#quickstatements-command-examples">QuickStatements Command Examples</a>
      <ul>
        <li><a href="#1-create-a-new-item">Create a New Item</a></li>
        <li><a href="#2-add-statements-claims">Add Statements (Claims)</a></li>
        <li><a href="#3-add-qualifiers">Add Qualifiers</a></li>
        <li><a href="#4-add-references">Add References</a></li>
        <li><a href="#5-modify-labels-descriptions-and-aliases">Modify Labels, Descriptions, and Aliases</a></li>
        <li><a href="#6-remove-statements-or-items">Remove Statements or Items</a></li>
      </ul>
    </li>
    <li><a href="#best-practices">Best Practices</a></li>
    <li><a href="#importing-csvtsv-data">Importing CSV/TSV Data</a></li>
    <li><a href="#error-handling">Error Handling</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ol>
</details>



## Overview

**QuickStatements** is a powerful tool designed for performing bulk edits on Wikidata. It allows users to add, modify, or remove large amounts of data efficiently, utilizing a simple command-line-like syntax. Whether you're adding new items, statements, or updating properties on multiple entities, QuickStatements is an essential tool for Wikidata editors who need to make large-scale changes quickly and reliably.

This documentation provides a comprehensive guide to using QuickStatements, covering its features, usage, and best practices.



## Features

1. **Create New Items**
   - Quickly create new items with specific labels, descriptions, and properties.
2. **Add Statements (Claims)**
   - Add new properties to an existing Wikidata item.
3. **Edit Statements**
   - Modify or delete existing statements on Wikidata items.
4. **Add Qualifiers**
   - Add qualifiers to existing statements for providing further context.
5. **Add References**
   - Attach references to statements to ensure they are properly sourced.
6. **Modify Labels, Descriptions, and Aliases**
   - Edit or add multilingual labels, descriptions, and aliases to items.
7. **Remove Data**
   - Delete items, claims, or qualifiers from Wikidata.
8. **Batch Execution**
   - Process hundreds or thousands of operations in a single batch.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Prerequisites

- **Wikidata Account**: You must be logged into Wikidata to use QuickStatements.
- **Permissions**: Ensure you have permission to perform bulk edits, especially for large-scale operations.
- **Structured Data**: Your data must be well-structured in CSV/TSV format or similar to be easily imported and processed.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Syntax and Command Structure

Each QuickStatements command follows a simplified format with columns specifying the **Item**, **Property**, **Value**, and optional **Qualifiers**, **References**, etc.

| Field        | Description                                                                                     |
|--------------|-------------------------------------------------------------------------------------------------|
| `Q####`      | Refers to an item (e.g., `Q42` for Douglas Adams).                                               |
| `P####`      | Refers to a property (e.g., `P31` for "instance of").                                            |
| Value        | The value associated with the property. Can be a reference to an item (e.g., `Q####`), string, number, etc. |
| Qualifier    | Additional information added to a claim to give it more context (e.g., time, place).             |
| References   | Data to support a claim (e.g., a URL, publication date).                                         |
| Labels       | Names or titles of items in different languages.                                                 |
| Descriptions | Brief summaries that describe the items.                                                         |
| Aliases      | Alternate names or terms by which an item is known.                                              |

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

QuickStatements can be used via:

1. **Web Interface**: Upload a CSV or TSV file or paste commands directly into the web interface.
2. **Batch Processing**: Execute large batches of commands through structured inputs.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## QuickStatements Command Examples

### 1. Create a New Item

This command will create a new item with a label and description.

```plaintext
CREATE
LAST|Len|"Sample Item"
LAST|Den|"This is a sample item for demonstration purposes."
LAST|P31|Q5  # Adds a claim that the item is an instance of a human
```

<h1 align="center"> ️💚️ MENTORS 💚 </h1>

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
| [<img src="https://avatars3.githubusercontent.com/u/3171900?v=3" width="100px;"/><br /><sub><b>Juan Herrera</b></sub>](http://juandavidherrera.com/en)<br />        | [<img src="https://avatars0.githubusercontent.com/u/464978?v=3" width="100px;"/><br /><sub><b>Alejandro Ñáñez</b></sub>](http://co.linkedin.com/in/alejandronanez/)<br /> | [<img src="https://avatars0.githubusercontent.com/u/8260962?v=3" width="100px;"/><br /><sub><b>Daniel Correa</b></sub>](https://github.com/danielcb29)<br />          | [<img src="https://avatars2.githubusercontent.com/u/19215389?v=3" width="100px;"/><br /><sub><b>Melina Mejía</b></sub>](https://github.com/MelinaMejia95)<br /> | [<img src="https://avatars3.githubusercontent.com/u/10712317?v=3" width="100px;"/><br /><sub><b>Felipe Jaramillo </b></sub>](https://github.com/p1p3)<br />    | [<img src="https://avatars1.githubusercontent.com/u/7959823?v=3" width="100px;"/><br /><sub><b>Diego Coy</b></sub>](https://diegocoy.com)<br />                               | [<img src="https://avatars2.githubusercontent.com/u/26748227?s=400&v=4" width="100px;"/><br /><sub><b>Laura Ciro</b></sub>](https://github.com/ltciro)<br />  |
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------: |
| [<img src="https://avatars1.githubusercontent.com/u/9866446?v=3" width="100px;"/><br /><sub><b>Fabian Buitrago</b></sub>](https://github.com/Fabian-Buitrago)<br /> | [<img src="https://avatars2.githubusercontent.com/u/25943655?v=3" width="100px;"/><br /><sub><b>teffcode</b></sub>](https://github.com/teffcode)<br />                    | [<img src="https://avatars3.githubusercontent.com/u/9259335?v=3" width="100px;"/><br /><sub><b>Alvaro Martinez</b></sub>](https://github.com/alvaromartinez986)<br /> | [<img src="https://avatars0.githubusercontent.com/u/348883?v=3" width="100px;"/><br /><sub><b>Jorge Ramírez</b></sub>](http://shinkei.github.io/)<br />         | [<img src="https://avatars0.githubusercontent.com/u/19542631?v=3" width="100px;"/><br /><sub><b>Camilo Perez</b></sub>](https://github.com/juancapm09)<br />   | [<img src="https://avatars3.githubusercontent.com/u/20744476?v=4" width="100px;"/><br /><sub><b>Harlen Giraldo</b></sub>](https://github.com/H4isan)<br />                    | [<img src="https://avatars2.githubusercontent.com/u/16061815?v=4" width="100px;"/><br /><sub><b>Camila Gomez</b></sub>](https://github.com/camigomez35)<br /> |
| [<img src="https://avatars3.githubusercontent.com/u/5982204?v=4" width="100px;"/><br /><sub><b>Jorge Cano</b></sub>](https://medium.com/@jorgeucano)<br />          | [<img src="https://avatars2.githubusercontent.com/u/39881?v=4" width="100px;"/><br /><sub><b>Josue</b></sub>](https://twitter.com/eusoj)<br />                            | [<img src="https://avatars2.githubusercontent.com/u/6851052?v=4" width="100px;"/><br /><sub><b>camilo</b></sub>](https://github.com/camilo56)<br />                   | [<img src="https://avatars1.githubusercontent.com/u/1382824?v=4" width="100px;"/><br /><sub><b>Pablo Velásquez</b></sub>](http://www.pablovem.com/)<br />       | [<img src="https://avatars3.githubusercontent.com/u/9832291?v=4" width="100px;"/><br /><sub><b>Carlos Angulo</b></sub>](https://github.com/CarlosAngulo)<br /> | [<img src="https://avatars0.githubusercontent.com/u/7102342?v=4" width="100px;"/><br /><sub><b>royalcas</b></sub>](https://github.com/royalcas)<br />                         | [<img src="https://avatars0.githubusercontent.com/u/4933011?v=4" width="100px;"/><br /><sub><b>Israel Guzman</b></sub>](https://github.com/GuzmanPI)<br />    |
| [<img src="https://avatars2.githubusercontent.com/u/17752391?v=4" width="100px;"/><br /><sub><b>Santiago Molina</b></sub>](https://www.justbit.site)<br />          | [<img src="https://avatars0.githubusercontent.com/u/3485075?v=4" width="100px;"/><br /><sub><b>Luis Aviles</b></sub>](https://luixaviles.com)<br />                       | [<img src="https://avatars2.githubusercontent.com/u/3689856?v=4" width="100px;"/><br /><sub><b>Carlos Roso</b></sub>](http://carlosroso.com)<br />                    | [<img src="https://avatars2.githubusercontent.com/u/2563374?v=4" width="100px;"/><br /><sub><b>Sherry</b></sub>](https://github.com/sazimi)<br />               | [<img src="https://avatars2.githubusercontent.com/u/3924809?v=4" width="100px;"/><br /><sub><b>Marian Villa</b></sub>](http://www.marianvilla.co)<br />        | [<img src="https://avatars1.githubusercontent.com/u/1557524?v=4" width="100px;"/><br /><sub><b>Carlos Ortiz</b></sub>](http://theowlo.blogspot.com)<br />                     | [<img src="https://avatars0.githubusercontent.com/u/165056?v=4" width="100px;"/><br /><sub><b>Stephen Fluin</b></sub>](https://github.com/StephenFluin)<br /> |
| [<img src="https://avatars0.githubusercontent.com/u/26145998?v=4" width="100px;"/><br /><sub><b>Mateo Castaño</b></sub>](https://github.com/matew17)<br />          | [<img src="https://avatars3.githubusercontent.com/u/22488812?v=4" width="100px;"/><br /><sub><b>Danilo Gutiérrez</b></sub>](https://github.com/CrisDan1905)<br />         | [<img src="https://avatars1.githubusercontent.com/u/1154098?v=4" width="100px;"/><br /><sub><b>Bonnie Brennan</b></sub>](https://twitter.com/bonnster75)<br />        | [<img src="https://avatars0.githubusercontent.com/u/19338528?v=4" width="100px;"/><br /><sub><b>Robin Hurtado</b></sub>](https://github.com/robinHurtado)<br /> | [<img src="https://avatars3.githubusercontent.com/u/18565471?v=4" width="100px;"/><br /><sub><b>Angela Ordoñez</b></sub>](http://angelitaooo.github.io)<br />  | [<img src="https://avatars2.githubusercontent.com/u/9698639?v=4" width="100px;"/><br /><sub><b>Carlos Esteban Lopez Jaramillo</b></sub>](https://github.com/luchillo17)<br /> | [<img src="https://avatars3.githubusercontent.com/u/7611944?v=4" width="100px;"/><br /><sub><b>Nicolas Molina Monroy</b></sub>](http://nicobytes.com)<br />   |
| [<img src="https://avatars1.githubusercontent.com/u/8793032?v=4" width="100px;"/><br /><sub><b>Sebastian Molano</b></sub>](http://www.nebulae.com.co)<br />         | [<img src="https://avatars3.githubusercontent.com/u/9942486?v=4" width="100px;"/><br /><sub><b>Frank Alejo Betancur</b></sub>](https://github.com/Krank2me)<br />         | [<img src="https://avatars1.githubusercontent.com/u/19813968?v=4" width="100px;"/><br /><sub><b>Ana Cidre</b></sub>](http://anacidre.com)<br />                       | [<img src="https://avatars1.githubusercontent.com/u/34170261?v=4" width="100px;"/><br /><sub><b>Juan Felipe Lujan</b></sub>](http://www.felipelujan.com)<br />  | [<img src="https://avatars2.githubusercontent.com/u/10585946?v=4" width="100px;"/><br /><sub><b>Manuela</b></sub>](http://www.manucastrillonm.co)<br />        | [<img src="https://avatars3.githubusercontent.com/u/5604472?v=4" width="100px;"/><br /><sub><b>AresDev</b></sub>](https://github.com/AresDev)<br />                           | [<img src="https://avatars3.githubusercontent.com/u/36491?v=4" width="100px;"/><br /><sub><b>Bram Borggreve</b></sub>](http://colmena.io/)<br />              |
| [<img src="https://avatars3.githubusercontent.com/u/6992488?v=4" width="100px;"/><br /><sub><b>maleja111</b></sub>](https://github.com/maleja111)<br />             | [<img src="https://avatars0.githubusercontent.com/u/7296623?v=4" width="100px;"/><br /><sub><b>Jorge Vergara</b></sub>](http://javebratt.com)<br />                       | [<img src="https://avatars0.githubusercontent.com/u/30100043?v=4" width="100px;"/><br /><sub><b>Juanjo Rendon</b></sub>](https://github.com/jnrndn)<br />             |
<!-- ALL-CONTRIBUTORS-LIST:END -->



