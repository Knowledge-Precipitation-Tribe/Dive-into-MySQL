# IF语句

Mysql的if既可以作为表达式用，也可在存储过程中作为流程控制语句使用IF表达式 

```text
IF(expr1,expr2,expr3) 
```

如果 expr1 是TRUE \(expr1 != 0 and expr1 != NULL\)，则IF\(\)的返回值为expr2; 否则返回值则为 expr3。IF\(\) 的返回值为数字值或字符串值，具体情况视其所在语境而定。 

## IFNULL

IFNULL\(\) 函数用于判断第一个表达式是否为 NULL，如果为 NULL 则返回第二个参数的值，如果不为 NULL 则返回第一个参数的值。

