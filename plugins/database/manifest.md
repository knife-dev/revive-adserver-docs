# Database XML Manifest
!> Documentation is incomplete.

### Getting Started
This manifest defines the tables a plugin uses.

> ALERT

### Database XML Manifest Attributes
```xml
<?xml version="1.0" encoding="utf-8" ?>
<?xml-stylesheet type="text/xsl" href="xsl/mdb2_schema.xsl"?>
<database>
    <name>$NAME</name>
    <create>$CREATE</create>
    <overwrite>$OVERWRITE</overwrite>
    <version>$VERSION</version>
    <status>$STATUS</status>
    
    <table>...</table>
    ...
    <table>...</table>
    <table>...</table>
</database>
```
!> Please note that in this example, we are only explaning the `<database>` path. For `<table>` explanation see [DataObject](/plugins/database/DataObject).

### Explanation
- `$NAME`is the name for this database scheme (it is not the databasen name).
- `$CREATE`is a`boolean`to define if this scheme should be created or not.
- `$OVERWRITE`is a`boolean`to define if this scheme should be overwritten if already exists.
- `$VERSION`is a`number`used for versioning the scheme.
- `$STATUS`defines the status of the scheme.`final`or`transitional`
