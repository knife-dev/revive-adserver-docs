# Database DataObject
!> Documentation is incomplete.

### Getting Started
A DataObject is a "model" in the database.

> DataObject schema must be defined under the database's XML manifest file in order to auto-generate the php and ini files. See [database's schema]() for more info.

##### DataObjects auto-generated files:
- `db_schema.ini` is generated from the Database XML manifest.
- `db_schema.links.ini` is generated from the Database XML manifest.
- `$DATAOBJECT_NAME.php` is generated from the Database XML manifest.

### How to auto generate the DataObject files:
In order to auto generate the dataobject and database schema files, the following steps are required:
1. Use a browser to go to Revive Adserver's /www/devel directory
2. In the sidebar, dropdown the "Generate DataObjects" section
3. Look for your Plugin, and click it.
4. Done. DataObjects should be generated accordingly. 

!> Please note that the '/www/devel' directory is not included in the production version of the Revive Adserver, it is available on the [ReviveAdserver GitHub repository](https://github.com/revive-adserver/revive-adserver).

### DataObject XML Attributes
```xml
<?xml version="1.0" encoding="utf-8" ?>
<?xml-stylesheet type="text/xsl" href="xsl/mdb2_schema.xsl"?>
<database>
 ...
 <table>
  <name>$TABLE_NAME</name>
  <declaration>
   <field>
    <primary>$IS_PRIMARY</primary>
    <name>$FIELD_NAME</name>
    <type>$FIELD_TYPE</type>
    <length>$FIELD_LENGTH</length>
    <notnull>$NOT_NULL</notnull>
    <default>$DEFAULT</default>
    <autoincrement>$AUTO_INCREMENT</autoincrement>
   </field>
   <index>
    <name>$PREFIX_$FIELD_NAME</name>
    <field>
     <name>$FIELD_NAME</name>
     <sorting>$SORTING_TYPE</sorting>
    </field>
   </index>
  </declaration>
 </table>
    ...
 </table>
</database>
```
!> Please note that in this example, we are only explaning the `<table>` part of the [XML Database Manifest]().

### Explanation
- `$TABLE_NAME`is the name the table on the mysql database will have.
- `<field>`is used to declare a row in the table.
    * `$IS_PRIMARY`is a`boolean`which defines if this field is the primary key.
    * `$FIELD_NAME`is a`string`which defines the name of the row.
    * `$FIELD_TYPE`defines the type of the row, may be `a`,`b`,`c`... see [DataTypes](/plugins/database/DataTypes.md) for more available types.
    * `$FIELD_LENGTH`is a`number`which defines the length of the row, for example `9`.
    * `$NOT_NULL`is a`boolean`to determine if this row can be null(`false`) or not(`true`).
    * `default` ...
- `<index>`is to define an index
    * `$PREFIX_`should be the same as the `$TABLE_NAME` as a good practice, this is just to avoid conflicts during dataobject generation or duplicate index errors.
    * `$FIELD_NAME`must tbe an existing field name (defined in `<field>`)
    * `$SORTING_TYPE`may be `ascending` or `descending`
    * `$DEFAULT`is the default value of the field, leave empty if none.
    * `$AUTO_INCREMENT`is a`number`that defines if this is an auto-increment field. `1` for true, `0` for false.
