# Entity Relationship Diagrams (ERD)

![](https://www.conceptdraw.com/solution-park/icons/SD_TOOL_ERD/spbanner.png)

## Overview

In this lesson, we'll talk about one of the most important aspects of building an **organized** and **efficient** database. ERDs are diagrams that are an important part of the planning process. ERDs help us determine the data persistence needs of that application and draft up what our database will look like before we ever write out a line of code!

## Data Modeling

Now before we jump into the fun of ERDs we need to get familiar with a something known as a **data model**. The data model is the result of your planning. It is a conceptual blueprint for implementing the data persistence needs within a given database. This could be SQL, NoSQL, etc. The data model is typically visualized with an ERD, or **Entity Relationship Diagram**.

## What Are ERD's?

As you've probably realized by now, ERD stands for Entity Relationship Diagram. It is a type of structural diagram that provides a graphical representation of our database and the relationship between its tables/collections.There are special symbols that are used in order to model the direction of the relationship in a parent/child format (for the most part).

## Data Entities

### What is a Data Entity?
- A **Data Entity**, or just **entity**, is used to conceptually model (represent) a real-world object within an application.

- Examples:  **User**, **Post**, **Comment**, **Order**, **Product**, etc.

- Each entity type will have one or more **attributes**...

### The Attributes for a Data Entity

- **Attributes** represent an entity's data. For example, a **Book** entity would probably have a **title** attribute.

- Each attribute has a data type. For example, _string_, _numeric_, _datetime_

#### 🧠💪 Thought Exercise (2 minutes)

- **Take a moment to identify what other attributes a Book entity might have** 

### Mapping Between an Entity and a Database

- Remember, the **conceptual data model** is used as a **blueprint** for how the actual database will be structured.

- Each **entity** in the data model identifies a **collection** in the database. For example, a **Book** entity will result in a **books** collection in the database.

**💡 Quick note:** MongoDB stores data records as BSON documents. BSON is a binary representation of JSON documents, though it contains more data types than JSON. So, it's going to contain fields and values. Like this: ![BSON](/images/png/fields.png)

- Each **attribute** in an entity identifies a **field/column** in the document/table.  For example, the **title** attribute will result in a field/column with the same name.

- Each **document/row** in the collection/table is logically an **instance** of the **entity**.

### 💡 Notice how we keep using collections vs tables and documents vs rows. These terms will differ depending on whether you are working with a NoSQL or SQL database.

### Types Of Relationships

- **Relationships** determine how the entities are related in terms of their **cardinality**.

- There are three main types of **cardinality**:
	- **one-to-one** (1:1)
	- **one-to-many** (1:M)
	- **many-to-many** (M:M)

| Relationship | Description                                                                                                                                         |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| One-To-One  (1:1) | One parent can only have one child                                                                                                                  |
| One-To-Many  | One parent can have many children. A child can only have one parent. We use a foreign key/reference (typically a unique value such as the ObjectId) |
| Many-To-Many | Many parents can have many children, join table/collection is used as a middleman to store both references                                          |

- Although 1:1relationships are not as common as 1:M or M:M, they have their place. 
- Let's take a look at a 1:1 relationship in an ERD...
- A **business** has one **mailing address** and that one mailing address belongs to one business: <br>
<img src="images/png/onetoone.png" height="200">

### ERD Cardinality Lines

- In an ERD, lines drawn between entities describe the cardinality between those entities as follows:

	<img src="https://i.imgur.com/sEnNZyZ.png">

- **Note** that these are the three main types of cardinality. There are more specific versions of these, such as _zero or many_, as [shown here](https://imgur.com/JtPQEOO).



## Determining the Cardinality Between Collections

- Okay, let's model the relationships between the entities of the _book recommending_ application...

	<img src="images/png/erd_blank.png" height="450">


- Usually by focusing on two entities, [domain knowledge](https://en.wikipedia.org/wiki/Domain_knowledge) and common-sense will reveal the relationship (usually a<br>one-to-many or many-to-many). 

## Continue Designing the ERD

### Beginning with `User` and `Book`

**❓ What's the relationship?**

<details>
<summary>
Let's see how this is diagramed...
</summary>
<img src="images/png/erd1.png" height="400">
<br><br>Reads as: <br> "A User has many Books (recommended)/ A Book belongs to a User".<br> "A User has many Books (reading)/ A book has many Users (reading)"
</details>

### Now for `Book` and `Comment`

**❓ What's the relationship?**

<details>
<summary>
Let's see how this is diagramed...
</summary>
<img src="images/png/erd2.png" height="400">
<br><br>Reads as: "A Book has many Comments/ A Comment belongs to a Book".
</details>

### Creating the ERD - Exercise (2 min)

Please identify the remaining relationships:
- **User** and **Comment**

- We'll review in 2 minutes... (don't peek)

### Books ERD - Final Version

<details>
<summary>
Here's our final ERD...
</summary>
<img src="images/png/finalerd.png" height="400">
<br><br>Reads as: "A User has many Comments/ A Comment Belongs to a User"
</details>

### User Has Two Different Relationships with Books

Note that in this app, a user "recommends" a book to other users by creating it in the database.  This one-to-many relationship is modeled with a `userRecommending` property on the Book model that references the `_id` of the user that created each particular book.

In addition, users can add books to their reading list.  This many-to-many relationship is modeled with a `usersReading` property which references an array of user documents' `_id` values.

### Comments

Because comments are being embedded within the book documents, there is no Comment model, just a schema.

#### Restricting Updating and/or Deleting of Comments Functionality

Each comment needs to know the user that submitted it.  Not just for display purposes, but to restrict the ability to update and/or delete a comment to that of the user that submitted it.  The `userId` property in the comment schema holds the `_id` of the user that submitted the comment and can therefore be compared to the logged in user's `_id` to render the additional UI for updating/deleteing.


## In Summary

- Modeling data is an important step during the planning of an application.  After all, _**data is the single source of truth**_ of an application!

- In addition to what we covered in this lesson, there are several other notations/ways to diagram an application's data model.  Check out [this post](https://www.lucidchart.com/pages/er-diagrams) from _lucidchart.com's_ website for more info.  

## How Do You Draw An ERD

There's a few free and readily available tools that can be used to design and build ERD's. Below you'll find a list of those tools:

- [Lucid Chart](https://www.lucidchart.com/)
- [DrawIO](https://app.diagrams.net/)

The tools listed above are intuitive and simpler to use than others and are more than adequate to build ERD's during this course. They also have really awesome tutorials on how to do anything with them!

