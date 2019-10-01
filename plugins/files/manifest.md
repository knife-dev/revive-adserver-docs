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
