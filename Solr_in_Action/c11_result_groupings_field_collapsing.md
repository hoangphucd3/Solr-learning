## 11.1 Result grouping vs. field collapsing

field collapsing—to remove duplicate
documents from a set of search results.

## 11.2 Skipping duplicate documents

See Figure 11.1

See Listing 11.2 for Standard search containing duplicate documents

See Listing 11.3 for Grouped search results collapsing on the product field

- grouping must be turned on by specifying the `group=true` parameter 1
- `group.limit` was set to `1`  indicating that only one document should be returned for each unique
value within a group
- `group.main` set to `true` to merge the search results in each groups and return in main results format.

` group.main option` has disadavantages:

- lose access to the total number of uncollapsed results within each group.
- lose the name of the group in this simple format
- it can be significantly slower than executing a standard search request

## 11.7 Efficient field collapsing with the Collapsing query parser

Collapsing query parser (CollapsingQParserPlugin): collapse search results to a single result per unique field value

```
/select?q=*:*&fq={!collapse field=fieldToCollapseOn}
```

This query will return only one document per unique value within the field called
`fieldtoCollapseOn`, where that document is the one containing the highest relevancy
score among all documents containing that unique field value.
