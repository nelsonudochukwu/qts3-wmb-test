<a id="readme-top"></a>
# QuickStatements (QS) 3.0 Documentation

<details>
 <summary>Translations:</summary>
 <ul>
  <li><a href="translations/qts-index-fr.md">French</li>
  <li><a href="translations/qts-index-pt.md">Portugese</li>
   <li><a href="translations/qts-index-es.md">Spanish</li>
 </ul>
</details>
<a href="#mentor-feedback">Implemented Feedback from Mentors</a>

## Table of Contents
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#overview">Overview of QuickStatements</a></li>
    <li><a href="#a-brief-on-wikidata">A Brief on Wikidata</a>
      <ul>
        <li><a href="#structure-of-wikidata">Structure of Wikidata</a></li>
        <li><a href="#lda">Labels, descriptions and aliases</a></li>
        <li><a href="#wiki-statements">Wikidata Statements</a></li>
        <li><a href="#syntax-and-command-structure">Syntax and Command Structure</a></li>
      </ul>
    </li>
    <li><a href="#qs-v3-docs">QuickStatements 3.0 Docs</a>
      <ul>
        <li><a href="#prerequisites">Getting Started: Prerequisites</a></li>
        <li><a href="#qs-3.0-homepage">QuickStatements 3.0 Homepage Overview</a></li>
        <li><a href="#what-is-a-batch">How To/Guides: What is a batch?</a>
          <ul>
            <li><a href="#create-new-batch">Creating a New Batch</a></li>
            <li><a href="#details-of-a-batch">Details of a Batch</a></li>
          </ul>
        </li>
        <li><a href="#batch-details">Viewing Batch Details and Batch History</a></li>
        <li><a href="#batches-per-user">See all Batch-edits Created by a User</a></li>
        <li><a href="#writing-batch-commands">Writing Batch commands</a>
          <ul>
            <li><a href="#create-new-item">Create a New Item</a>
            <li><a href="#add-statements">Add Statements</a>
            <li><a href="#add-qualifiers">Add Qualifiers</a> 
            <li><a href="#add-references">Add References</a>
            <li><a href="#modify-lda">Modify Labels, Descriptions, and Aliases</a>
            <li><a href="#remove-items">Remove Statements or Items</a>
            <li><a href="#import-data">Importing CSV/TSV Data</a>                                                                  </ul>
        </li>
        <li><a href="#best-practices">Best Practices</a></li>
        <li><a href="#error-handling">Error Handling</a></li>
        <li><a href="#recommendations">Recommendations</a></li>
        <li><a href="#conclusion">Conclusion</a></li>
      </ul>
    </li> 
  </ol>
</details>

## Overview

**QuickStatements (QS)** is a powerful tool designed by [Magnus Manske](https://en.wikipedia.org/wiki/User:Magnus_Manske) for performing bulk edits on Wikidata. It allows users to add, modify, or remove large amounts of data efficiently, utilizing a simple command-line-like syntax. Whether you're adding new items, statements, or updating properties on multiple entities, QuickStatements is an essential tool for Wikidata editors who need to make large-scale changes quickly and reliably.

This documentation provides an introduction to the features, usage, and best practices of QuickStatements 3.0. _[Click](#qs-v3-docs)_ to jump right in. However, to fully grasp the features of quickstatements 3.0, it is important to first understand the major constituent of Quickstatements⎯```Wikidata.```

#

<a id="a-brief-on-wikidata"></a>
<details>
<summary> A brief on Wikidata</summary>
Wikidata is a free, collaborative, multilingual, secondary database, managed by the Wikimedia Foundation. It serves as a central storage for structured data that is used in various Wikimedia projects, like Wikipedia, and also provides data to external users and organizations. The primary goal of Wikidata is to allow humans and machines to understand and query information easily.

Some key features include:

- **Multilingual support:** Data is stored in such a way that it can be accessed in any language.
- **Open data:** Wikidata's data is freely available under the Creative Commons Public Domain Dedication (CC0).
- **Collaborative editing:** Anyone with an account can edit Wikidata, making it a community-driven resource.
- **Linking data:** Wikidata integrates with other Wikimedia projects, serving as the source of consistent, up-to-date data.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="structure-of-wikidata"></a>
## Structure of Wikidata
The structure of Wikidata is based on a simple yet powerful model of **items**, **properties**, and **values**. These three components form the backbone of how data is stored, linked, and retrieved.

- **Items (Q numbers):** Each item is a unique concept represented by a **QID** (e.g., Douglas Adams is represented by Q42). These items store data and link to other items.

- **Properties (P numbers):** Properties describe specific attributes of an item and are identified by **PIDs** (e.g., date of birth is represented by **P569**). Properties can describe relationships between items or between an item and a data value.

- **Values:** These are the actual data points (e.g., the date **1952-03-11** as the value for **P569** on item **Q42** for Douglas Adams’ birth date).

Together, items, properties, and values create **statements**, which are the building blocks of Wikidata.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="lda"></a>
## Labels, Descriptions, and Aliases
Each item in Wikidata can have multiple **labels**, **descriptions**, and **aliases** in different languages:

- **Labels:** A label is the main name of an item (e.g., “Douglas Adams” for **Q42**). An item can have a different label in every language.

- **Descriptions:** Descriptions provide context about the item to differentiate it from similar items (e.g., “British author and screenwriter” for **Q42**).

- **Aliases:** Aliases are alternative names for an item that are used for search purposes. For example, **Q42** (Douglas Adams) might have an alias like "Douglas Noel Adams."

These three components help ensure that items are easy to find, distinguish, and access in a variety of languages and contexts.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="wiki-statements"></a>
## Wikidata Statements
**Statements** are the core knowledge units in Wikidata, used to describe items through a combination of a property and a value. A statement connects an item to its associated data:

- **Property:** Defines what aspect of the item you are describing (e.g., date of birth, occupation, nationality).
- **Value:** Provides the specific information (e.g., a date, a string, or a reference to another item).
A statement can also have **qualifiers** and **references** to provide more context or cite the source of the data.

For example:

- **Item:** Douglas Adams (Q42)
- **Property:** Date of birth (P569)
- **Value:** March 11, 1952
- **Qualifier:** Source (S854) – Links to a webpage or database providing proof of the statement.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="syntax-and-command-structure"></a>
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

</details>

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#

<a id="qs-v3-docs"></a>
## QuickStatements 3.0 Docs

This documentation provides an introduction to the features of QuickStatements 3.0 which is an upgrade that enhances the functionality, performance and user experience of the QuickStatements platform to improve system stability.

#

### Prerequisites
In order to create and run batches, you must ensure the following:
- **Wikidata Account**: You must be logged into Wikidata to use QuickStatements.
- **Structured Data**: Your data must be well-structured in CSV/TSV format or similar to be easily imported and processed.
- **Autoconfirmed user**: To be an autoconfirmed user, you must be 4 days old on the platform and you must have made 50 edits to be considered one.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="qs-3.0-homepage"></a>
## QuickStatements 3.0 Homepage Overview
The homepage of **QuickStatements 3.0** is designed to facilitate easy access to core features for managing and running batch edits. Below is a breakdown of the visible elements:

<p align="center">
  <img src="https://github.com/user-attachments/assets/339297cb-b5e4-46ca-82d1-799ea0b964dd" alt="QuickStatements 3.0 Homepage" />
  <p align="center">QuickStatements 3.0 Homepage</p>
</p>

#### Navigation Menu:
1. **New batch:** A link that takes you to a form where you can create a new batch of edits to be uploaded to Wikidata.

2. **Last batches:** This link provides access to the history of recently submitted batches. Users can track the status and details of their past batch operations.

3. **Git:** Links to the [QuickStatements GitHub repository](https://github.com/WikiMovimentoBrasil/quickstatements3), where users can view the codebase, report issues, or contribute to the development of the platform.
  
4. **Login:** Allows users to log into their Wikidata accounts. Once logged in, users can access features like submitting and tracking their batch submissions.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#### Main Interface:
5. **“Welcome to QuickStatements 3.0”:** A header welcoming users to the main interface.

#### Primary Action Buttons:

6. **New batch:** Clicking this button initiates the creation of a new batch. Users can input data and commands to process and upload multiple edits to Wikidata in bulk.
  
#### Batch Lookup Section:
7. **Batch ID:** Users can input a specific batch ID to retrieve detailed information about that particular batch. Clicking the ```See batch details``` button shows the status, progress, and results of the batch.

8. **Username:** Users can enter a specific Wikidata username to retrieve a list of all batches associated with that user. Clicking ```See batches by user``` will display all submitted batches from that user.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#
  
<a id="what-is-a-batch"></a>
### What is a Batch in QuickStatements?
A **batch** refers to a set of commands or operations that are executed together to perform bulk edits. Each batch can include multiple statements or claims that you want to add, modify, or remove from items on Wikidata.

#

<a id="create-new-batch"></a>
#### A. Creating a new Batch in QuickStatements
To create a new batch in QuickStatements, follow these steps:
1. Click on the ```New Batch``` button located on the homepage

<p align="center">
  <img src="https://github.com/user-attachments/assets/d153bc61-0d95-4d32-b48e-876e1009f908" alt="QuickStatements 3.0 Homepage" />
  <p align="center">Click New Batch</p>
</p>

2. A form will appear where you can input your commands or upload your data file. The available formats include both the QuickStatements V1 format and CSV/TSV format.
<p align="right">(<a href="#readme-top">back to top</a>)</p>

#

<a id="details-of-a-batch"></a>
#### B. Details of a Batch in QuickStatements

<p align="center">
  <img src="https://github.com/user-attachments/assets/e81cd5a6-e029-454c-b4d6-67b7e607b920" alt="QuickStatements 3.0 Homepage" />
  <p align="center">Details of a New Batch</p>
</p>

<p align="right">(<a href="#readme-top">back to top</a>)</p>

A new batch consists of:
1. **Command format:** Your command format can be in V1 format or CSV format.
     - **V1 format:** Command-based format where each line represents a tab-separated command.
     - **CSV format:** Consists of a first line⎯the header⎯that defines the contents of each column. The subsequent lines supply information to be applied to Wikibase according to the contents of each column's header.
  
  Example of V1 syntax:
  ```
  CREATE
  LAST	Len	Doctor Worm
  LAST	Den	1998 song performed by They Might Be Giants
  LAST	P2650	Q128309
  ```
  
  Example of CSV syntax:
  ```
  qid,Len,Den,P260
  Q128309,Doctor Worm,1998,song performed by They Might Be Giants
  ```
  
  QuickStatements can also be run via URL:
  ```
  See example: https://quickstatements.toolforge.org/#/v1=Q37887397%7CP214%7C%2296480189%22%7CS143%7CQ565
  Qid: Q37887397
  Property: P214
  Senwiki : S143
  Value: Q565
  ```

2. **Custom batch name:** This is a label or identifier that you can assign to a specific batch of edits for easier management and reference. By default, batches are given generic names, typically just a batch ID. However, you have the option to provide a custom name when you create or upload a batch. This custom name makes it easier to recognize or remember what a particular batch was intended to do, especially when dealing with multiple batches over time.
  
3. **Commands:** These are the instructions you enter to perform specific operations on Wikidata items. These commands allow you to add, modify, or remove data from items in Wikidata. The commands are written in a specific format, and each line typically represents an action to be taken on a Wikidata item.
<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Viewing Batch Details and History
You can track the progress and status of a specific batch by entering the **Batch ID** in the appropriate field and clicking the **See batch details** button. This displays information like the number of edits made, the success or failure of operations, and any errors that occurred.

#

<a id="batches-per-user"></a>
#### C. See all Batches per User in QuickStatements
To view the history of batch edits by a specific user:
1. Enter the ```username``` of the user in the username field (username can be found at wiki-login.)
2. Click ```See batches by user```to list all the batches that the user has submitted. The list will include:
   - **Batch IDs**
   - **Descriptions (if you added custom names)**
   - **Status (e.g., in progress, completed, or failed)**
   - **Dates**
   - **Number of edits in the batch**

> [!NOTE]
> Each batch has a unique URL associated with it. You can bookmark or share this URL to access or monitor a batch later.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#

<a id="writing-batch-commands"></a>
#### D. Writing Batch Commands in QuickStatements

<a id="create-new-item"></a>
#### 1. Create a New Item

This command will create a new item with a label and description.

```plaintext
CREATE
LAST  Len  "Sample Item"
LAST  Den  "This is a sample item for demonstration purposes."
LAST  P31  Q5  # Adds a claim that the item is an instance of a human
```

<a id="add-statements"></a>
#### 2. Add Statements (Claims)

Adding statements to an existing item (e.g., Douglas Adams - Q42).

```plaintext
Q42  P569  1952-03-11  # Adds the date of birth (P569) for Douglas Adams
Q42  P19  Q84          # Adds the place of birth (P19) as Cambridge (Q84)
```

<a id="add-qualifiers"></a>
#### 3. Add Qualifiers

You can add qualifiers to existing statements to provide more detail.

```plaintext
Q42  P69  Q3918  P580  1971  P582  1974  # Adds education (P69) at St John's College (Q3918) with start (P580) and end (P582) dates
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="add-references"></a>
#### 4. Add References

Adding references to an existing statement:

```plaintext
Q42  P69  Q3918  S854  "https://example.com/education"  # Adds a URL reference for the education claim
```

<a id="modify-lda"></a>
#### 5. Modify Labels, Descriptions, and Aliases
Modify Labels, descriptions, and aliases in different languages:
```plaintext
Q42  Len  "Douglas Adams"  # Changes the English label to "Douglas Adams"
Q42  Ade  "Douglas Adams"  # Changes the German label to "Douglas Adams"
Q42  Aen  "Douglas Noel Adams"  # Adds an alias in English
Q42  Den  "British author and screenwriter"  # Modifies the English description
```

<a id="remove-items"></a>
#### 6. Remove Statements or Items
Remove statements or delete items entirely:
```plaintext
-Q42  P19  # Deletes the place of birth (P19) statement for Q42
-Q100000  # Deletes the entire item Q100000
```
<p align="right">(<a href="#readme-top">back to top</a>)</p>

<a id="import-data"></a>
#### 7. Importing CSV/TSV Data

You can prepare your data in CSV or TSV format, where each line represents one operation. A sample format:
```plaintext
Q42,P69,Q3918,P580,1971,P582,1974
Q42,P19,Q84
Q42,P569,+1856-01-01T00:00:00Z/9
```

Upload the file through the web interface to process the batch.
<p align="right">(<a href="#readme-top">back to top</a>)</p>

#

### Best Practices 
- **Test with Small Batches:** Always test your commands with a small set of items before large-scale edits to avoid unintended changes.
- **Use References:** Ensure that statements are properly sourced with references to enhance data quality.
- **Monitor Progress:** After submission, keep track of your batch’s progress and check for errors.

#

### Error Handling

When an error occurs during execution, QuickStatements will indicate which command failed. Common issues include:
- Incorrect item or property IDs.
- Syntax errors in date formats or missing data fields.
- Permissions or throttling by Wikidata for large-scale edits.
In these cases, review the failed commands and correct the issues before re-running.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#
  
### Conclusion
QuickStatements is an essential tool for bulk editing on Wikidata, enabling users to manage large sets of data efficiently. By following this guide, you can create, update, and manage items with ease, improving the quality and accuracy of Wikidata.

For more advanced use cases, refer to the [Wikidata documentation](https://www.wikidata.org/wiki/Help:QuickStatements) for further details and updates.

#

### References
This documentation was inspired from many sources, however, [Diátaxis](https://diataxis.fr/) was the most significant guide for a writing this as it provides a systematic approach to understanding the needs of documentation users. The [Google Technical Writing Course](https://developers.google.com/tech-writing/overview) was instrumental as well.

#

<a id="mentor-feedback"></a>
### Modifications and Improvements Implemented as Required in the Initial Review
| Feedback                                         | Modifications                                         | Location                    |
|--------------------------------------------------|-------------------------------------------------------|-----------------------------|
| You have more than 200 commits                   | The lengthy commits have been squashed to keep git history clean | Repository history          |
| DELETE command doesn't exist in QuickStatements  | The command has been rectified across all translations                       | [Remove Items](#remove-items) |
| Your images make the documentation easy to understand | Improved the images for better clarity                | All images                  |


## ️💚️ THANK YOU MENTORS 💙 
<!-- ALL-CONTRIBUTORS-LIST:START -->
<!-- prettier-ignore -->
| [<img src="https://github.com/user-attachments/assets/1deb350c-3202-48b3-bef2-ead6c6f9a06d" width="100px;"/><br /><sub><b>Ederporto, EPorto (WMB)</b></sub>](https://phabricator.wikimedia.org/p/Ederporto/)<br />        | [<img src="https://github.com/user-attachments/assets/4d0112e0-00b8-421d-a043-67282f13d413" width="100px;"/><br /><sub><b>Artur Corrêa Souza</b></sub>](https://phabricator.wikimedia.org/p/ACorrea-WMB/)<br /> | [<img src="https://github.com/user-attachments/assets/b8c0a206-9e85-4b2c-a41d-13986e126565" width="100px;"/><br /><sub><b>MGalves (WMB)</b></sub>](https://phabricator.wikimedia.org/p/MGalves_WMB/)<br />          |
| :---------------------: | :-----------------------: | :--------------------: |
<p align="right">(<a href="#readme-top">back to top</a>)</p>
<!-- ALL-CONTRIBUTORS-LIST:END -->
