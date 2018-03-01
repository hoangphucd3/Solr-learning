## The anatomy of a Solr request

### Request handlers

Receive a request, perform some function, and return a response to the client.

See figure 7.1

Table 7.1 A brief description of many of Solr’s request handlers

`MoreLikeThisHandler`: Allows textually similar documents to be found based
upon an input document

### Search components

Search components are configurable processing steps that occur within the lifetime of a search handler.

Search components are configured in solrconfig.xml

View Listing 7.2

### Query parsers

Query  parsers are  used  to  interpret  a  search  syntax  into  a  Lucene  query  for  finding  a desired set of documents.

## Working with query parsers

### Specifying a query parser

using the defType parameter 

```
/select?defType=edismax&q=…
/select?defType=term&q=…
```

In this example, notice that two different query parsers—eDisMax and Lucene:

```
/select?q={!edismax}hello world OR {!lucene}title:"my title"
```

The `{!... }` syntax used to define query parsers inline known as local params.

### Local params

local params allow you to pass request parameters only to the specific query parser that you want to consider them.

#### Syntax

```
{!param1=value1 param2=value2 … paramN=valueN}
```
Begins with `{!` and ends with `}`

For example,

```
/select?q=hello world&defType=edismax&qf=title^10 text&q.op=AND
```

is functionally equivalent to the following query utilizing local params:

```
/select?q={!defType=edismax qf="title^10 text" q.op=AND}hello world
```

`defType` stands for default type

You can override the default type within a specific context using the type
parameter inside a set of local params:

```
/select?q={!type=edismax qf="title^10 text" q.op=AND}hello world
```

`{!type=edismax …}` and `{!edismax …} `. Both of these work because type is considered the default local param key if only a
value is specified

#### PARAMETER DEREFERENCING

The ability to substitute arbitrary variables into your query.

```
/select?q={!edismax v=$userQuery}&userQuery="hello world"
```

## Queries and filters

### The fq and q parameters

The `fq` parameter stands for filter => put machine-generated filters (such as category:"technology")

the `q` parameter stands for query => put user keywords (such as keywords:"apache solr")

## 7.4 The default query parser (Lucene query parser)

### FIELDED TERM SEARCHES

```
title:solr
title:"apache solr" content:(search engine)
```

### SPECIAL CHARACTER ESCAPING

In Solr, these characters include:

```
+ - && || ! ( ) { } [ ] ^ " ~ * ? : /
```

## 7.5 Handling user queries (eDisMax query parser)

Extended Disjunction Maximum (eDisMax)

### 7.5.3 Searching across multiple fields

With the Lucene query parser, you would have to construct a query
for Solr in Action to look something like this:

```
(((title:solr) OR (description:solr) OR (author:solr)) AND ((title:in) OR
(description:in) OR (author:in)) AND ((title:action) OR (description:action)
OR (author:action)))
```

the eDisMax query parser can do this for you with ease

```
q=solr in action&qf=title description author
```

You can assign different boosts to each field if you want:

```
q=solr in action&qf=title^1.5 description author^3
```

See Figure 7.4 demonstrates how this kind of boosted field search works

### 7.5.4 Boosting queries and phrases

#### THE PF (PHRASE FIELDS), PF2, AND PF3 PARAMETERS

uses the same format as the `qf `
