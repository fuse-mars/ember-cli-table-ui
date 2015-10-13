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
The Column has a path(key with one or more words separated by ".") to the string value of the data,
Since this key used to get the actual data-value out of the owning object, is owned by the column, 
a refresh may be needed for cells that receive their data in asynchronous way.

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
Note1: There is assumption that the **path** to the data-value is at most 2 keys deep.
```
contact.get("address.country") // accepted
contact.get("address.country.gdp") // non accepted
```
Note2: There is assumption that the data is an object or a list of objects of same type.

### Creating/Updating piece of data
With the concept of DDAU, the update of a cell value will have to trigger an action in the **controller** because this controller is the owner of all data and therefore should be responsible of all changes that happen to its data.
* Saving/Updating varies depending on the data-value displayed in a cell, so if we will have to take into account all possible cases (which we don't know up front), if we give the controller responsible for these actions.
 * The solution for now is to have the column define a method to create/update the data-object, given a new data-value (since data-objects are of same type in each column). 
 * There will be a default implementation. However, the user can override it by adding their own implementation during the column definition(i.e. when creating a column object).
* Creating (happens for data whose path is 2 keys deep. i.e. parent object is the direct owner)
```
let n = contact.get("name") // contact is direct owner of n
let c = contact.get("address.country") // contact is not the direct owner of c, direct owner is "address"
```


# Resource
https://blog.udemy.com/html5-tables
http://webdesign.about.com/od/tables/a/aa122605.htm
http://www.echoecho.com/htmltables.htm
http://www.pcmag.com/encyclopedia/term/44496/html-table
