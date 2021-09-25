# Constraint

Constraint defines a rule to restrict the values in database. There are 6 types of constraints:

1. __Not null__
2. __Unique__
    + Cannot be Lob, Long, Varray, Object, Ref, Nested table, etc
    + Cannot have more than 32 columns
    + Cannot specify a unique key for a subview
3. __Primary key__  
   Combines Not null and Unique constraints.
4. __Foreign key__  
   Establishes a relationship between columns(foreign key) and a specified primary or unique key (referenced key).
5. __Check__  
   Specifies a condition that each row in the table must:
    + Cannot contain: sub queries, scalar sub queries, calls to function that is not deterministic, user-defined functions, nested table columns or attribute, pseucocolumns
    + Cannot refer to other table
    + Cannot add check constrains for view
6. __REF__
