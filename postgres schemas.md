Schemas in [[postgress]] are like namespaces
By default, everything is in the schema `public`

to list them
```
select schema_name from information_schema.schemata;
or
\dn
```
to create/destroy one
```
CREATE SCHEMA schema_name;
DROP SCHEMA schema_name;
```
You can add your schema to the top level by setting your search path
```
 show search_path;
   search_path   
-----------------
 "$user", public
postgres=# SET search_path TO scheduler,public;
postgres=# show search_path;
    search_path    
-------------------
 scheduler, public
