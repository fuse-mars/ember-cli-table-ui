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


# Resource
https://blog.udemy.com/html5-tables
http://webdesign.about.com/od/tables/a/aa122605.htm
http://www.echoecho.com/htmltables.htm
http://www.pcmag.com/encyclopedia/term/44496/html-table
