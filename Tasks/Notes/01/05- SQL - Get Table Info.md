
```sql


SELECT column_name, data_type
FROM INFORMATION_SCHEMA.COLUMNS
WHERE table_name = 'TDeIcingConfiguration'

-----------------------------------------------------------------------------------------------------------------------------------------

SELECT table_name
FROM INFORMATION_SCHEMA.COLUMNS
WHERE column_name = 'DeIcingTriggerId';

-----------------------------------------------------------------------------------------------------------------------------------------

SELECT 
    fk.name AS foreign_key_name,
    tp.name AS parent_table,
    tr.name AS referenced_table,
    cp.name AS parent_column,
    cr.name AS referenced_column
FROM 
    sys.foreign_keys AS fk
    INNER JOIN sys.tables AS tp ON fk.parent_object_id = tp.object_id
    INNER JOIN sys.tables AS tr ON fk.referenced_object_id = tr.object_id
    INNER JOIN sys.foreign_key_columns AS fkc ON fk.object_id = fkc.constraint_object_id
    INNER JOIN sys.columns AS cp ON fkc.parent_object_id = cp.object_id AND fkc.parent_column_id = cp.column_id
    INNER JOIN sys.columns AS cr ON fkc.referenced_object_id = cr.object_id AND fkc.referenced_column_id = cr.column_id
WHERE 
    tr.name = 'TDeIcingConfiguration';


```


