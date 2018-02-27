## Basic text analysis

See Listing 6.1 Example field type for analyzing general text

#### Analyzer

Inside the <fieldType> element, you should define at least one <analyzer> that
determines how the text will be analyzed.

Two separate <analyzer> elements:

- for indexing
- for analyzing the text entered by users when searching

The analysis applied to query terms must be compatible with how the text was analyzed during indexing

#### Tokenizer

each <analyzer> breaks the text analysis process into two phases: 
 
- tokenization (parsing)
- token filtering

`WhitespaceTokenizer`: splits text on whitespace only

`StandardTokenizer`: split terms on whitespace and punctuation and correctly handles URLs, email addresses, and acronyms

Example:

```
<tokenizer class="solr.StandardTokenizerFactory"/>
```

All tokenizers produce a stream of tokens that can be processed by zero or more
filters to perform some sort of transformation of the token.

#### Token filter

 Performs one of three actions on a token:
 
- Transformation — Changing the token to a different form such as lowercasing all letters or stemming
- Token injection — Adding a token to the stream, as is done with the synonym filter
- Token removal — Removing tokens, as is done by the stop word filter
 
Filters can be chained together to apply a series of transformations on each token.
The order of the filters is important.

#### StandardTokenizer

#### Removing stop words with StopFilterFactory

#### LowerCaseFilterFactory—lowercase letters in terms
