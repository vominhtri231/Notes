# Procedure function

A stored procedure/function are prepared SQL code that you can save and reuse later.

``` sql
CREATE [OR REPLACE] PROCEDURE procedure_name (parameter_list)
IS
...

exec procedure_name(a,b,c);
```

``` sql
CREATE [OR REPLACE] FUNCTION function_name (parameter_list)
IS
...

select function_name(a,b,c) from dual;
```

## Comparison

| Procedure | Function |
| --- | --- |
| Could return 0 -> n values | Must return 1 value |
| Could have input + output parameters | Have input parameters only |
| Could call functions | Can't call procedure |
| allow DML | not allow DML |
| can not be embedded in Select | can be embedded in Select |
| can use Transactions | can not use Transaction |
