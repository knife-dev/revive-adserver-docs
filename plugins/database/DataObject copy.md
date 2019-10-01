# Database DataObject
!> Documentation is incomplete.

### Getting Started
A DataObject is a "model" in the database.

> DataObject schema must be defined under the database's XML manifest file in order to auto-generate the php and ini files. See [database's schema]() for more info.

##### DataObjects auto-generated files:
- `db_schema.ini` is generated from the Database XML manifest.
- `db_schema.links.ini` is generated from the Database XML manifest.
- `$DATAOBJECT_NAME.php` is generated from the Database XML manifest.

### DataObject XML Attributes
```xml
<?xml version="1.0" encoding="utf-8" ?>
<?xml-stylesheet type="text/xsl" href="xsl/mdb2_schema.xsl"?>
<database>
 <name>$DB_NAME</name>
 <create>$CREATE</create>
 <overwrite>$OVERWRITE</overwrite>
 <version>$VERSION</version>
 <status>$STATUS</status>
 <table>
  <name>$TABLE_NAME</name>
  <declaration>
   <field>
    <name>$FIELD_NAME</name>
    <type>$FIELD_TYPE</type>
    <length>$FIELD_LENGTH</length>
    <notnull>$NOT_NULL</notnull>
    <default></default>
   </field>
   <index>
    <name>$PREFIX_id</name>
    <field>
     <name>$FIELD_NAME</name>
     <sorting>ascending</sorting>
    </field>
   </index>
  </declaration>
 </table>
    ...
 </table>
</database>
```