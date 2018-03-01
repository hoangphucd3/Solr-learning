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
