<a id="readme-top"></a>
# QuickStatements Documentation

## Table of Contents



<!-- TABLE OF CONTENTS -->
<details open>
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
>[!NOTE]
>
>To use QuickStatements, you must be 4 days old on the platform and you must have made 50 edits.

QuickStatements can be used via:

1. **Web Interface**: Upload a CSV or TSV file or paste commands directly into the web interface.
2. **Batch Processing**: Execute large batches of commands through structured inputs.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## QuickStatements Command Examples

### 1. Create a New Item

This command will create a new item with a label and description.

```plaintext
CREATE
LAST|Len|"Sample Item"
LAST|Den|"This is a sample item for demonstration purposes."
LAST|P31|Q5  # Adds a claim that the item is an instance of a human
```

### 2. Add Statements (Claims)

Adding statements to an existing item (e.g., Douglas Adams - Q42).

```plaintext
Q42|P569|1952-03-11  # Adds the date of birth (P569) for Douglas Adams
Q42|P19|Q84          # Adds the place of birth (P19) as Cambridge (Q84)
```

### 3. Add Qualifiers

You can add qualifiers to existing statements to provide more detail.

```plaintext
Q42|P69|Q3918|P580|1971|P582|1974  # Adds education (P69) at St John's College (Q3918) with start (P580) and end (P582) dates
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### 4. Add References

Adding references to an existing statement:

```plaintext
Q42|P69|Q3918|S854|"https://example.com/education"  # Adds a URL reference for the education claim
```

### 5. Modify Labels, Descriptions, and Aliases
Modify Labels, descriptions, and aliases in different languages:
```plaintext
Q42|Len|"Douglas Adams"  # Changes the English label to "Douglas Adams"
Q42|Lde|"Douglas Adams"  # Changes the German label to "Douglas Adams"
Q42|Aen|"Douglas Noel Adams"  # Adds an alias in English
Q42|Den|"British author and screenwriter"  # Modifies the English description
```

### 6. Remove Statements or Items
Remove statements or delete items entirely:
```plaintext
Q42|P19|DELETE  # Deletes the place of birth (P19) statement for Q42
Q100000|DELETE  # Deletes the entire item Q100000
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>
---

## Best Practices
- Test with Small Batches: Always test your commands with a small set of items to avoid unintended changes.
- Review Edits: Double-check all data before running large batches.
- Use References: Ensure that statements are properly sourced with references to enhance data quality.
- Monitor Progress: After submission, keep track of your batch’s progress and check for errors.

## Importing CSV/TSV Data
You can prepare your data in CSV or TSV format, where each line represents one operation. A sample format:
```plaintext
Q42,P69,Q3918,P580,1971,P582,1974
Q42,P19,Q84
Q42,P569,1952-03-11
```
After preparing the CSV, upload it via the QuickStatements web interface to run the batch.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Error Handling

When an error occurs during execution, QuickStatements will indicate which command failed. Common issues include:
- Incorrect item or property IDs.
- Syntax errors in date formats or missing data fields.
- Permissions or throttling by Wikidata for large-scale edits.
In these cases, review the failed commands and correct the issues before re-running.

## Conclusion
QuickStatements is an essential tool for bulk editing on Wikidata, enabling users to manage large sets of data efficiently. By following this guide, you can create, update, and manage items with ease, improving the quality and accuracy of Wikidata.

For more advanced use cases, refer to the [Wikidata documentation](https://www.wikidata.org/wiki/Help:QuickStatements) for further details and updates.



## ️💚️ MENTORS 💙 
<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore -->
| [<img src="https://github.com/user-attachments/assets/1deb350c-3202-48b3-bef2-ead6c6f9a06d" width="100px;"/><br /><sub><b>Ederporto, EPorto (WMB)</b></sub>](https://phabricator.wikimedia.org/p/Ederporto/)<br />        | [<img src="https://github.com/user-attachments/assets/4d0112e0-00b8-421d-a043-67282f13d413" width="100px;"/><br /><sub><b>Artur Corrêa Souza</b></sub>](https://phabricator.wikimedia.org/p/ACorrea-WMB/)<br /> | [<img src="https://github.com/user-attachments/assets/b8c0a206-9e85-4b2c-a41d-13986e126565" width="100px;"/><br /><sub><b>MGalves (WMB)</b></sub>](https://phabricator.wikimedia.org/p/MGalves_WMB/)<br />          |
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------: |

<p align="right">(<a href="#readme-top">back to top</a>)</p>
<!-- ALL-CONTRIBUTORS-LIST:END -->

# Navigation

[Home](#home-section) | [About](#about-section) | [Services](#services-section) | [Contact](#contact-section)

---

<details id="home-section">
  <summary>Home</summary>
  <p>Welcome to the home page.</p>
</details>

<details id="about-section">
  <summary>About</summary>
  <p>This is the about section.</p>
</details>

<details id="services-section">
  <summary>Services</summary>
  <p>Details about the services offered.</p>
</details>

<details id="contact-section">
  <summary>Contact</summary>
  <p>Contact us through this section.</p>
</details>
