https://www.elastic.co/guide/en/kibana/current/lucene-query.html



Lucene:

- https://www.elastic.co/guide/en/kibana/7.7/lucene-query.html
- https://www.elastic.co/guide/en/elasticsearch/reference/7.7/query-dsl-query-string-query.html#query-string-syntax


KQL

- 



### CookBook

=









### Lucene vs KQL

https://stackoverflow.com/questions/62281279/what-is-the-difference-between-lucene-query-language-and-kql

The current documentation for [KQL](https://www.elastic.co/guide/en/kibana/current/kuery-query.html) and [Lucene query syntax](https://www.elastic.co/guide/en/kibana/current/lucene-query.html) shows the syntax of both for various types of queries. I will summarize the main differences:

### 1. Dropdown Suggestions

It seems that KQL enables getting suggestions for fields, values and  operators as you type your query, while this feature is not present when using Lucene. (This feature requires the “Basic Tier” or above.)

### 2. Range Queries

To find content where `count` is greater than or equal to `5`: the KQL syntax is `count:>=5`, while the Lucene syntax is `count:[5 TO *]`.

To find content where `account_number` is greater than or equal to 100, but less than 200: the KQL syntax is `account_number:>=100 and account_number:<200`, while the Lucene syntax is `account_number:[100 TO 200}`.

### 3. Operators

The KQL documentation outlines the Boolean operators `or`, `and` and `not`. The upper case versions (`OR`, `AND` and `NOT`) also work. The documentation specifies that `and` has a higher precedence over `or`, which is the usual operator precedence rule.

The Lucene documentation specifies the following:

> The preferred operators are `+` (this term must be present) and `-` (this term must not be present).

For example, `brown +fox -news` specifies that `brown` is optional, `fox` must be present, and `news` must not be present.

Lucene also supports `AND`, `OR` and `NOT`, but only in uppercase. So, if you try using `and`, it will be taken as the literal word. Also, Lucene supports `&&`, `||` and `!`. However, the documentation states that all of these operators do not  honor the usual operator precedence rules, and advises the use of  parentheses whenever multiple operators are used together.

### 4. Exist queries

To find documents that contain the field `response`: the KQL syntax is `response:*`, and the Lucene syntax is `_exists_:response` (`response:*` also works in Lucene, but the behavior if the value of the field is an empty string might be different).

### 5. Wildcards

For KQL, the documentation only mentions the `*` wildcard, which matches zero or more characters. There is no mention of `?`, so I assume it does not exist. In Lucene, `?` exists and matches a single character.

In KQL, escaping the wildcard character is never necessary when using it as a wildcard, so we can have something like `book.*:(quick or brown).` In Lucene, it seems that the wildcard needs to be escaped when used as part of the field name. The example given is `book.\*:(quick OR brown)`.

### 6. Nested queries

The syntax for nested queries seems to be different as per the documentations.

### 7. Extra Features in Lucene

The KQL documentation does not mention regular expressions, fuzzy  search, nor boosting; so they are probably not supported. Lucene  supports them.