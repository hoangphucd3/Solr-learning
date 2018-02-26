### Indexed fields

Mark your field as indexed if you need to sort, facet, group by, provide query suggestions for, or execute function
queries on values within a field.

### Stored fields

Store fields are fields that aren’t useful from a search perspective but are still useful
for displaying search results.

A field may be indexed and stored. Each of these fields can be searched and displayed in results.

### Defining fields in schema.xml

#### Required field attributes

If you don’t return a field in search results, it doesn’t need to be stored.

#### Multivalued fields

In Solr, fields that can have more than one value per document are called multivalued
fields. In schema.xml, you declare a multivalued field by setting multiValued=
"true" on the field definition:

```
<field name="link"
 type="string"
 indexed="true"
 stored="true"
 multiValued="true"/>
```

#### Dynamic fields

Dynamic fields allow you to apply the same definition to any fields in your documents
whose names match either a prefix or suffix pattern, such as s_* or *_s.

See page 128 for more details.

You can’t formulate queries
to find a match in all string fields by querying with a prefix or suffix pattern:
*_s:coffee
