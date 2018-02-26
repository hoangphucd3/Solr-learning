
## Searching, matching, and finding content

### What is a document?

A document could be a newspaper article, a resume
or social profile, or, in an extreme case, an entire book.

Each document contains one or more fields

Example Solr document

```
<doc>
 <field name="id">company123</field>
 <field name="companycity">Atlanta</field>
 <field name="companystate">Georgia</field>
 <field name="companyname">Code Monkeys R Us, LLC</field>
 <field name="companydescription">we write lots of code</field>
 <field name="lastmodified">2013-06-01T15:26:37Z</field>
</doc>
```

Although Solr has a flexible schema for each document, it’s not "schema-less." 
All field types must be defined, and all field names (or dynamic
field-naming patterns) should be specified in Solr’s `schema.xml`)

A document, then, is a collection of fields that map to particular field types
defined in a schema.

### Terms, phrases, and Boolean logic

#### REQUIRED TERMS

- +new +house
- new AND house

`+`: is a unary symbol operator (toán tử một ngôi). That
means that the part of the query immediately following it is required to exist in any
documents matched.

`AND`: binary operator (toán tử hai ngôi) that means that the part of
the query immediately preceding and the part of the query immediately following it
are both required.

#### OPTIONAL TERMS

`OR`: binary operator, which
means that either the part of the query preceding or the part of the query following it
is required to exist in any documents matched. This is default.

- new house
- new OR house

#### NEGATED TERMS

To require parts of query not exist in any matched documents:
- new house –rental
- new house NOT rental

#### PHRASES

You can also search for phrases:

- "new home" OR "new house"
- "3 bedrooms" AND "walk in closet" AND "granite countertops"

### Finding sets of documents

Find out about Inverted Index
See Table 3.6

### Phrase queries and term positions

term positions: a feature of the index that we
conveniently left out of our initial inverted index
See Table 3.7 Inverted index with term positions.

one of the Benefits is Searching for specific phrases.

### Fuzzy matching

Fuzzy matching is defined as the ability to perform inexact matches
on terms in the search index.

For example: 
- Search for any words that start with a particular prefix (wildcard searching).
- Find spelling variations within one or two characters (fuzzy searching or edit distance searching).
- Match two terms within some maximum distance of each other (proximity searching).

#### WILDCARD SEARCHING
common forms of fuzzy matching in Solr is the use of wildcards.
Suppose you want to find `offic`.

We can enumarates all of the possible variations:
- Query: office OR officer OR official OR officiate OR …

You can use the asterisk (*) wildcard character to perform this same function:

- Query: offi* Matches office, officer, official, and so on
- Query: off*r Matches offer, officer, officiator, and so on

The question mark (?) match only a single character.

- Query: off?r Matches offer, but not officer

Wildcards are only meant to work on individual search terms, not on phrase searches:

- Works: softwar* eng?neering
- Does not work: "softwar* eng?neering"

#### RANGE SEARCHING

The ability to search for terms that fall between known values.

For examples: Match documents created in the six
months between February 2, 2012, and August 2, 2012.

