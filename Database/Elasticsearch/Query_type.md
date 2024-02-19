# Query types

## Match

Match query would analyze the input text and search for each term independently, the exact order is ignore.

Example: for the match query  of `quick fix` would return `quick me fix`, `quick fix me`, `me fix quick`, etc.

## Match_phrase

Match phrase query would analyze the input text and search the terms appear in the same order and close to each other.

Example: for the match phrase query of `quick fix` would return `quick fix me`, `I quick fix`, etc.

## Term/Terms

Term or terms query, would not analyze the input text and look for exact field value matches.

The different between term query and terms query is term query allows us to search by by list of values. 

## Compound

The bool query type is used to combine multiple queries.

* Must

* Should

* Must not

* Filter
