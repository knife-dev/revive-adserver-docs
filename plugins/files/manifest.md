# Plugin XML Manifest
This page describes how the XML Manifest of a plugin is structured.

!> Documentation is incomplete.

### Explainable Example
```xml
<?xml version="1.0" encoding="ISO-8859-1" ?>
<?xml-stylesheet type="text/xsl" href=""?>
<plugin>
    <name>$PLUGIN_NAME</name>
    <displayName>Example Revive Plugin</displayName>
    <creationDate>2019-09-10</creationDate>
    <author>Someone (someone@somewhere.com)</author>
    <authorEmail>someone@somewhere.com</authorEmail>
    <authorUrl>https://someone.com/</authorUrl>
    <license>GNU General Public License v2.0</license>
    <description>This is an example plugin for the Revive Adserver</description>
    <version>0.0.1-dev</version>
    <oxversion>3.2.0-beta-rc3</oxversion>
    <type>extension</type>
    <install>
        <files>
            <file path="{PLUGINPATH}">$PLUGIN_NAME.readme.txt</file>
            <file path="{PLUGINPATH}">$PLUGIN_NAME.uninstall.txt</file>

            <!-- Plugin www -->
            <file path="{MODULEPATH}$PLUGIN_NAME/">somefile.php</file>
            <file path="{ADMINPATH}/">someotherfile.php</file>
        </files>
        <contents>
            <group name="$SUBPLUGIN_NAME">$PRIORITY</group>
        </contents>
    </install>
</plugin>
```
### Explanation:
- `$PLUGIN_NAME`is the plugin's name and must match and follow the [Plugin's Structure]()
- `<displayName>`allows to set the Plugin's name (displayed on the admin UI).
- `<creationDate>`allows to set the Plugin's creation date(displayed on the admin UI).
- `<author>`allows to set the Plugin author's name(displayed on the admin UI).
- `<authorEmail>`allows to set the Plugin author's email(displayed on the admin UI).
- `<authorUrl>`sets the Plugin author's url (also displayed on the admin UI).
- `<license>`is used to license the plugin. (displayed in the admin UI).
- `<version>`sets the version of the plugin.
- `<oxversion>`sets the adserver's version which this plugin was designed for.
- `<type>`sets the type of the plugin, can be: `extension`, `package`
- `<install>`
    - `<files>` contains all the files packaged in for the Plugin only. This does not include the files for subplugins, if any. Each file must be declared here, one by one.
        - `<file>` declares a file packaged in the plugin, where:
            - `{PLUGINPATH}`is equivalent to the `/plugins/etc/` directory of the plugin.
            - `{MODULEPATH}`is equivalent to the plugin's `/plugins/` directory. That's why in this example we use `$PLUGIN_NAME` at the end, to declare files from the folder of this plugin only. 
            - `{ADMINPATH}`is equivalent to the `/www/admin/plugins/$PLUGIN_NAME` directory. 
    - `<contents>`Contains all the plugins packaged with the Plugin.
        - `<group>` declares a subplugin where:
            - `$SUBPLUGIN_NAME`is the subplugin's name and must match and follow the [SubPlugin's Structure]()
            - `$PRIORITY`is the priority of the subplugin. (Loading order, from 1 to 999....)
- `<readme>`is used to set the Plugin's readme text, however if not specified, the readme file from the top-level plugin's directory will be used.

# SubPlugin XML Manifest
This page describes how the XML Manifest of a subplugin is structured.

!> Documentation is incomplete.

### Explainable Example
```xml
<?xml version="1.0" encoding="ISO-8859-1" ?>
<?xml-stylesheet type="text/xsl" href=""?>
<plugin>
    <name>$SUBPLUGIN_NAME</name>
    <displayName>Example Revive Plugin</displayName>
    <creationDate>2019-09-10</creationDate>
    <author>Someone (someone@somewhere.com)</author>
    <authorEmail>someone@somewhere.com</authorEmail>
    <authorUrl>https://someone.com/</authorUrl>
    <license>GNU General Public License v2.0</license>
    <description>This is an example plugin for the Revive Adserver</description>
    <version>0.0.1-dev</version>
    <oxversion>3.2.0-beta-rc3</oxversion>

    <install>
        <files>
            <file path="{PLUGINPATH}">SUBPLUGIN_NAME.readme.txt</file>
            <file path="{PLUGINPATH}">SUBPLUGIN_NAME.uninstall.txt</file>

            <!-- Plugin www -->
            <file path="{MODULEPATH}$SUBPLUGIN_NAME/">somefile.php</file>
            <file path="{ADMINPATH}/">someotherfile.php</file>
        </files>
        <contents>
            <group name="$SUBPLUGIN_NAME">$PRIORITY</group>
        </contents>
    </install>
</plugin>
```
### Explanation:
- `$PLUGIN_NAME`is the plugin's name and must match and follow the [Plugin's Structure]()
- `<displayName>`allows to set the Plugin's name (displayed on the admin UI).
- `<creationDate>`allows to set the Plugin's creation date(displayed on the admin UI).
- `<author>`allows to set the Plugin author's name(displayed on the admin UI).
- `<authorEmail>`allows to set the Plugin author's email(displayed on the admin UI).
- `<authorUrl>`sets the Plugin author's url (also displayed on the admin UI).
- `<license>`is used to license the plugin. (displayed in the admin UI).
- `<version>`sets the version of the plugin.
- `<oxversion>`sets the adserver's version which this plugin was designed for.
- `<extends>`if the subplugin extends an existing functionality of the adserver, can be: `api`, `bannerTypeHtml` and so on.
- `<install>`
    - `<files>` contains all the files packaged in for this subplugin only, if any. This does not include the files of other subplugins or plugins. Each file must be declared here, one by one.
        - `<file>` declares a file packaged in the subplugin, where:
            - `{MODULEPATH}`is equivalent to the plugin's `/plugins/` directory. That's why in this example we use `$SUBPLUGIN_NAME` at the end, to declare files under this subplugin only. 
            - `{ADMINPATH}`is equivalent to the `/www/admin/plugins/$SUBPLUGIN_NAME` directory. 
    - `<schema>`declares the schema modifications this subplugin has.
        - `<mdb2schema>`***tables_`$SUBPLUGIN_NAME`.xml***`</mdb2schema>` specifies the [Database's XML Manifest](). 
        - `<dboschema>`***db_schema***`</dboschema>` declares database schema. (from file path ***plugins/etc/`$SUBPLUGIN_NAME`/etc/DataObjects/db_schema.ini***). See [Database Schema]() for more info.
        - `<dbolinks>`***db_schema.links***`</dbolinks>` declares the schema's foreign keys (from file path ***/plugins/etc/`$SUBPLUGIN_NAME`/etc/DataObjects/db_schema.links.ini***). See [Database Links]() for more info.
        - `<dataobject>` Declares a data object file (`$DATAOBJECT_NAME`). (from file path ***/plugins/etc/`$SUBPLUGIN_NAME`/etc/DataObjects/`$DATAOBJECT_NAME`.php***). See [Database DataObjects]() for more info.
    - `<configuration>`declares the settings of this subplugin, displayed in the admin UI. 
    Only administrator has permissions to change settings in config file. Settings are written to a group section [`$SUBPLUGIN_NAME`]
        - `<setting key="mySetting1" type="checkbox" label="Description" required="0" size="1" visible="1">0</setting>`Declares a setting for the subplugin
- `<readme>`is used to set the Subplugin's readme text, however if not specified, the readme file from the top-level plugin's directory will be used.
- `<components>`...




