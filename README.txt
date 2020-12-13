README for our modifcation in SQLova Text-to-SQL system

To view the changes that we made, in diff form:
https://github.com/sg1993/sqlova/commits?author=sg1993

The APIs introduced for our implementation:
1) def get_column_cells_naively(): 
This is for approach #1 and #2.
This API, given a table, returns the column-cells of all columns in the table.

2) def get_column_cells_selectively(table, nlu): 
This is for appraoch #3.
This API, given a table and the Natural Language Utterance (NLU), does a two-part processing:
  a) It first checks if a header appears in the NLU as it is.
  b) It also checks if any of cell-content appears in the NLU.

The contents of the two columns from (a) and (b) are then appended.

3) def generate_inputs():
This function has the logic to trim the contents from columns which are overflowing. 
We first compute what the allowed number of tokens should be for each columns by equally distributing
512 tokens among all the columns. Then we check which columns are under their quota and their surplus
slots are assigned to the ones that have crossed their quota.

The result from generate_inputs() is then fed as input to BERT for embedding-representation.