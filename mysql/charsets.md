# Charsets and Collation and indexes

Not only does the storage type define how an UNIQUE INDEX works, but so does
collation

```
mysql> SET NAMES utf8mb4 COLLATE utf8mb4_bin;
Query OK, 0 rows affected (0.01 sec)
mysql> SELECT 'e' = 'é';
+------------+
| 'e' = 'é'  |
+------------+
|          0 |
+------------+
1 row in set (0.00 sec)

mysql> SET NAMES utf8mb4 COLLATE utf8mb4_unicode_ci;
Query OK, 0 rows affected (0.01 sec)

mysql> SELECT 'e' = 'é';
+------------+
| 'e' = 'é'  |
+------------+
|          1 |
+------------+
1 row in set (0.00 sec)
```

This has an effect on how indexes work. If adding an unique index to a table
that has a case insensitive collation such as `utf8mb4_unicode_ci` a duplicate
error will be produced. In the past is was all based on the column type or so I
thought. 
