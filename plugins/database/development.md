# Schema Development
Creating a custom schema (or extending/changing an existing one) is a "tricky" process. You must take attention and follow the steps correctly.

### Prerequisites
- `/scripts/` directory that have helpers to generate the DataObjects. Available at [Revive's Github Repository](https://github.com/revive-adserver/revive-adserver/tree/master/scripts)
- `www/devel/` directory that is a 'dashboard' to execute the helper /scripts/. Available at [Revive's Github Repository](https://github.com/revive-adserver/revive-adserver/tree/master/www/devel)
- The plugin you are creating the schema for installed.

### Prepare your subplugin to have it's own schema
Since you don't have the auto-generated files yet and we must install the plugin first, we will declare our files as "common files" in our subplugin's manifest to install it.

0. cd to: `/plugins/etc/your-subplugin-name/`
0. Locate your subplugin's manifest: [your-subplugin-name.xml](/plugins/files/subplugin_manifest)
    * Because we don't have our DataObject files yet, we must create an empty `db_schema.ini` file inside the `etc/DataObjects` directory.
    * If we use foreign keys, we should have our `db_schema.links.ini` file there too, **remember that this file is not auto-generated**, so you need to manage it by yourself.
0. Declare the schema files as common files in the subplugin's manifest inside `<files>`:
```xml
<files>
...
    <file path="{PLUGINPATH}your-subplugin-name/etc/">tables_your-subplugin-name.xml</file>
    <file path="{PLUGINPATH}your-subplugin-name/etc/DataObjects/">db_schema.links.ini</file>
    <file path="{PLUGINPATH}your-subplugin-name/etc/DataObjects/">db_schema.ini</file>
...
</files>
```
0. Verify that your [tables_your-subplugin-name.xml](/plugins/database/DataObject?id=table39s-manifest) is OK.
0. Zip the whole plugin and install it on your revive instance.

### Generate your schema file and DataObjects
0. Browse to you-reviveadserver.com/**www/devel** 
0. Dropdown the `Generate DataObjects` menu and select your recently installed subplugin from the list.
0. Wait until the script is executed. If everything is OK, you should see something like: 
```log
OA_DB_DataObject_Generator: 0: START
    ...
OA_DB_DataObject_Generator: 0: Writing ini as .../plugins/etc/your-subplugin-name/etc/DataObjects/db_schema.ini
    ...
OA_DB_DataObject_Generator: 0: DONE```
0. Done, the `db_schema.ini`file has been generated and all of your dataobjects as .php files. (Located in `.../plugins/etc/your-subplugin-name/etc/DataObjects/`)
0. Now you need to declare the auto-generated files in your _schema Table's manifest_, so when you install the plugin again, the schema is auto-created/modified.

### Declare your schema files into the subplugin's manifest
Once you have generated your DataObject files and db_schema.ini file, you will need to declare them in your subplugin's manifest.
0. cd to: `/plugins/etc/your-subplugin-name/`
0. Delete any declarations you made in [step 3](#prepare-your-subplugin-to-have-it39s-own-schema) when you prepared the subplugin
0. Locate your subplugin's manifest: `your-subplugin-name.xml` and open it:
0. Declare all the schema related files inside the`<schema>`path.
```
        <schema>
            <mdb2schema>tables_your-subplugin-name</mdb2schema>
            <dboschema>db_schema</dboschema>
            <dbolinks>db_schema.links</dbolinks>
            <dataobject>Somedataobject.php</dataobject>
            <dataobject>Blocker.php</dataobject>
            <dataobject>User.php</dataobject>
        </schema>
```

!> Note that there are `<dataobject>` for every php file. You will need to look into the DataObjects directory to see what DataObjects were generated and its names.
