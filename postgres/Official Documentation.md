## Notes:

- In join query always *qualify* (ex: T.name and E.name) so that query wont fail if a duplicate column is later added to one of the tables.
- ORDER OF EVALUATION: 
  - WHERE ->  GROUP BY
- WHERE vs HAVING:
  - It is important to understand the interaction between aggregates and SQL's `WHERE` and `HAVING` clauses. The fundamental difference between `WHERE` and `HAVING` is this: `WHERE` selects input rows before groups and aggregates are computed (thus, it controls which rows go into the aggregate computation), whereas `HAVING` selects group rows after groups and aggregates are computed. Thus, the `WHERE` clause must not contain aggregate functions; it makes no sense to try to use an aggregate to determine which rows will be inputs to the aggregates. On the other hand, the `HAVING` clause always contains aggregate functions. (Strictly speaking, you are allowed to write a `HAVING` clause that doesn't use aggregates, but it's seldom useful. The same condition could be used more efficiently at the `WHERE` stage.) https://www.postgresql.org/docs/14/tutorial-agg.html
  - 







READ on 2023-01-17 upto 3.5 Window Functions.

NEXT: https://www.postgresql.org/docs/14/tutorial-window.html

