# ember-cli-table-ui
Place for describing my design decisions on creating a table component in ember

# Inspiration
Ember-table addon from Addepar (https://github.com/Addepar/ember-table), provides a good solution for emberjs developers who want to display data in a table.
However, it does not cover a use case of data that needs frequent updates
i.e. Changes made to a cell value has to be persisted to the backend.

In this case:
* Ember-data is being used to communicate with the backend
* A path to read the cell value is diffrent from a path used to save new/updated value
* 

# Philosophy
* A table is An HTML structure for creating rows and columns on a Web page. This means that you can use table for multiple reasons, but in our case, a **table** solve a soul purpose of efficiently presenting large number of data.
* Data is Factual information, especially information organized for analysis or used to reason or make decisions, when this data is presented using a table we call it tabiiar data.
* Tabular data is any data that can be displayed in an excel sheet or stored in a database.

# Design
* A table is composed of **rows** and **columns**.
* Each row is identified by a number (1, 2, 3 ... )
* Each column is identified by a name ('name', 'email' ...)
* Intersection between a row and a column is a **cell**.
* Cells are owner of the displayed **piece of data** (value of a cell, which is visual to the user).
* A piece of data, in Emberjs terms, is represented as an **attribute** of an Ember-Data **Model object**.
* The model-object above in is owned by the row.
* Each column holds information on how to manipulate pieces of data from the model-object.
* By **manipulate** I mean getting and updating value of a cell.

### Displaying piece of data
Since this key used to get the actual data out of the owning object, is owned by the column, 
a refresh ma be needed for cells that receive their data in asynchronous way.

ex:
```
// contact is the main object
contact : {
  id: 0,
  name: "John Smith",
  address: 1
}

address: {
  id: 1,
  country: "USA",
  zip: "00001"
}

// direct (synchronous) data retrieval
contact.get("name")
// future (asynchronous) data retrieval
contact.get("address.country")
```
Note: There is assumption that the path to the data-value is at most 2 keys deep.
```
contact.get("address.country") // accepted
contact.get("address.country.gdp") // non accepted
```

### Creating/Updating piece of data
With the concept of DDAU, the update of a cell value will have to trigger an action in the **controller** because this controller is the owner of all data and therefore should be responsible of all changes that happen to its data.


# Resource
https://blog.udemy.com/html5-tables
http://webdesign.about.com/od/tables/a/aa122605.htm
http://www.echoecho.com/htmltables.htm
http://www.pcmag.com/encyclopedia/term/44496/html-table
