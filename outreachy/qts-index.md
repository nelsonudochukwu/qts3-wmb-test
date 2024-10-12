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



## Prerequisites

- **Wikidata Account**: You must be logged into Wikidata to use QuickStatements.
- **Permissions**: Ensure you have permission to perform bulk edits, especially for large-scale operations.
- **Structured Data**: Your data must be well-structured in CSV/TSV format or similar to be easily imported and processed.



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



## Usage

QuickStatements can be used via:

1. **Web Interface**: Upload a CSV or TSV file or paste commands directly into the web interface.
2. **Batch Processing**: Execute large batches of commands through structured inputs.



## QuickStatements Command Examples

### 1. Create a New Item

This command will create a new item with a label and description.

```plaintext
CREATE
LAST|Len|"Sample Item"
LAST|Den|"This is a sample item for demonstration purposes."
LAST|P31|Q5  # Adds a claim that the item is an instance of a human
