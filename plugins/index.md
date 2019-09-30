# Plugin Development
!> ***Documentation is incomplete***

## Getting Started
This page will introdce you into the revive adserver plugin development. 
### Plugin Structure
A common plugin structure may be the following:

```
{$PLUGIN_NAME} [1]
  /plugins
    /etc
      /{$PLUGIN_NAME}.xml [2]
      /{$PLUGIN_NAME}.readme.txt [3]
      /{$PLUGIN_NAME}.uninstall.txt [4]
      /{$PLUGIN_GROUP} [5]
        /_lang [5.1]
        /etc [5.2]
          /DataObjects [5.3]
          /changes [5.4]
          /tables_{$PLUGIN_GROUP}.xml [5.6]
        /{$PLUGIN_GROUP}.xml [5.7]
      ...
    /{$PLUGIN_NAME} [6]
    /{$PLUGIN_HOOK} [7]
      /{$PLUGIN_GROUP} [7.1]
      ...
    ...
  /www
    /admin
      /plugins [8]
        /{$PLUGIN_NAME} [8.1]
        /{$PLUGIN_NAME} [8.2]
```
#### Variable Definitions
- `PLUGIN_NAME` is an alphanumeric name of the plugin. It is recommended that this doesn't include spaces or any other characters.
- `PLUGIN_GROUP` is an alphanumeric name of a "subplugin" (known as group)
- `PLUGIN_HOOK` is an optional directory where the name of the directory corresponds to one of the [Plugin Hooks supported](plugins/hooks/index)
    - The directory name must match the hook name.

    Plugins can have multiple hooks, however the plugin does not have to contain any directories based on plugin hook names if the plugin does not provide functionality via any plugin hooks.

#### Structure Explanation
1. This is the top level directory of the plugin, it highly recommended that this has an alphanumeric name without special characters on it and describes what the plugin has/do. 
2. This is the top-level 'manifest' of the plugin that describes:
    - The plugin details (version, name, description, author, etc.)
    - All files packaged in the plugin (at the top-level, if any)
    - The subplugins (plugin groups).
3. This is an optional file containing readme information for the plugin (available at the Plugin's page when installed on the adserver).
4. Optional file, containing information which will be displayed during uninstallation process.
5. `/PLUGIN_GROUP` this a "sub-plugin" top-level directory. Contains all files related to this specific group. The name of this directory must match one in the top-level manifest of the Plugin (`$PLUGIN_NAME`/plugins/etc/`$PLUGIN_NAME`.xml ).
    - **5.1**) `/_lang` is an optional directory that contains the translation files of the subplugin. 
    - **5.2**) `/etc` is an optional directory containing details relating to database tables created and managed by the plugin.
    - **5.7**) `/{$PLUGIN_GROUP}.xml` is the top-level 'manifest' of the subplugin that describes:
        - The subplugin details (version, name, description, author, etc.)
        - All the files packaged in the subplugin's top-level directory.
        - The plugin components that the subplugin provides.
6. `/{$PLUGIN_NAME}` is an optional directory in which code which provides shared functionality to the plugin should be placed, if required. For example, database access code which is shared by all hooks, etc.
7. Is an optional directory where the name of it corresponds to one of the Plugin Hooks supported.
    - **7.1**) `{$PLUGIN_GROUP}` is an optional directory to store code that relates both to the plugin hook, and to the plugin group of the same name. That is:
        - If the plugin has a subplugin, and the plugin provides functionality based on a plugin hook, then the code for that subplugin/plugin hook must be located in this directory.
        - If the plugin has a subplugin, and provides functionality for multiple plugin hooks, then the subplugin directory will exist under each plugin hook directory for which there is functionality being provided. 
8. is an optional directory in which code required for use in the user interface is located. (www accessable).
    - **8.1**) `/{$PLUGIN_NAME}` is an optional directory to store code that relates to the Plugin's www resources (such an index.php, or other stuff that will be accessable via *youradserver.com/www/admin/`${PLUGIN_NAME}`/index.php*)
    - **8.2**) `/{$PLUGIN_GROUP}` is an optional directory to store code that relates to a Subplugin's www resources (such an index.php, or other stuff that will be accessable via *youradserver.com/www/admin/`${PLUGIN_GROUP}`/index.php*)




