1. What is a view?

A view is a virtual table created from a query.

It does not store data itself; it shows data from underlying tables.

CREATE VIEW emp_view AS
SELECT name, salary FROM employees WHERE dept_id = 2;


2. Can we update data through a view?

Yes, if the view is based on a single table without complex joins, aggregates, or GROUP BY.

No, if the view has DISTINCT, GROUP BY, UNION, aggregate functions, or joins (depends on DBMS).

3. What is a materialized view?

A materialized view is a view whose query result is physically stored on disk.

It must be refreshed (manually or automatically) to update data.

Used in data warehousing for performance.

4. Difference between view and table?

Feature	Table	View
Storage	Stores actual data	Virtual (doesn’t store data, except materialized view)
Creation	CREATE TABLE	CREATE VIEW
Updates	Always updatable	Sometimes (depends on complexity)
Performance	Faster (direct storage)	Slower (depends on underlying query)

5. How to drop a view?

DROP VIEW view_name;


6. Why use views?

Simplify complex queries

Hide sensitive columns (security)

Provide consistent interface even if underlying schema changes

Reuse queries easily

7. Can we create indexed views?

Yes, some DBMSs (like SQL Server, Oracle) allow creating indexes on views (usually materialized or special “indexed views”).

Improves performance for complex joins/aggregations.

8. How to secure data using views?

Hide sensitive columns (e.g., salary, password) from users.

Grant access to the view instead of the base table.
Example:

CREATE VIEW emp_public AS
SELECT name, dept_id FROM employees; -- hides salary


9. What are limitations of views?

May not be updatable (if too complex)

Performance overhead (re-computes on each query unless materialized)

Cannot always use indexes directly (except in indexed/materialized views)

Dependent on base tables (if schema changes, view may break)

10. How does WITH CHECK OPTION work?

Ensures that INSERT or UPDATE through a view obeys the view’s WHERE condition.

Prevents entering rows that the view itself cannot display.

Example:

CREATE VIEW hr_emps AS
SELECT * FROM employees WHERE dept_id = 2
WITH CHECK OPTION;
