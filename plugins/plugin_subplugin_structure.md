# Plugin subplugin's structure
!> ***Documentation is incomplete***

## Getting Started
This page explains the structure of a subplugin (group) of a Plugin.
### Subplugin structure
A common subplugin structure may be the following:

```
  /plugins
    /etc
      /{$SUBPLUGIN_NAME} [1]
        /{$SUBPLUGIN_NAME}.xml [1.1]
        /_lang [1.2]
        /etc [2]
          /DataObjects [2.1] 
            ...
          /changes [2.2]
            ...
          /tables_{$SUBPLUGIN_NAME}.xml [2.3]
    /{$SUBPLUGIN_NAME} [3]
    ...
  /www
    /admin
      /plugins [4]
        /{$SUBPLUGIN_NAME} [4.1]
```
#### Variable Definitions
- `{$SUBPLUGIN_NAME}` is an alphanumeric name of the "subplugin" (known as group), it highly recommended that this has an alphanumeric name without special characters on it and describes what the subplugin has/do.


#### Structure Explanation
> The structure of the subplugin is somehow similar and dependant to the main plugin's structure. Take care of this to avoid confusion.

1. This is the top level directory of the subplugin, must match the `{$SUBPLUGIN_NAME}`
  1. This is the XML manifest of the subplugin that describes:
    - The subplugin details (version, name, description, author, etc.)
    - All files packaged in the subplugin (at the subplugin top-level, if any)
    - The navigation menus, and more.
  2. `/_lang` is an optional directory that contains the translation files for the subplugin.
2. This is the folder where xml manifest files and auto-generated files are placed.
  1. `/DataObjects`is an optional directory containing all the auto-generated files for database dataobjects.
  2. `/changes`is an optional directory containing the migration ...
  3. This is the [Database's XML Manifest File](/plugins/database/Manifest) which is used to generate the `DataObjects` files.
3. `/{$SUBPLUGIN_NAME}` is an optional directory in which code which provides shared functionality to the main plugin or other subplugins should be placed, if required. (Most of the subplugin source code is usually placed there)
4. is an optional directory that comes along with the main plugin in which code required for use in the user interface is located. (www accessable).
    1. `/{$SUBPLUGIN_NAME}` is an optional directory to store code that relates to the subplugin's www resources (such an index.php, or other stuff that will be accessable through *youradserver.com/www/admin/`${SUBPLUGIN_NAME}`/index.php*)



