Ling Breeze Generator config
=================
2019-09-13


Config example
-------------

```yaml
breeze_generator:
    instance: Ling\Light_BreezeGenerator\Service\LightBreezeGeneratorService
    methods:
        setContainer:
            container: @container()
        setConf:
            conf:
                ling:
                    class: Ling\Light_BreezeGenerator\Generator\LingBreezeGenerator
                    conf:
                        dir: ${app_dir}/tmp/Light_BreezeGenerator
                        # prefix is always separated from the table by one underscore
                        prefix: lud
                        factoryClassName: LightKitAdmin
                        namespace: Ling\Test\$prefix
                        # The suffix to add to the class name.
                        # For instance if the class is User and the suffix is Object,
                        # The class name will be UserObject
                        # The default value is Object
                        classSuffix: Object
                        # Whether to overwrite existing files (if false, skip them)
                        # Used mainly for debugging purposes, in production you probably should set this to false
                        # The default value is false
                        overwriteExisting: true
                        generate:
                            prefix: lud

```



In a nutshell
----------

This generator generates some objects based on a table selection.
So the first step is to select the tables you want to generate the objects for.
Then generate the objects.


The generated objects are:

- an XXXObject (one per table)
- an XXXObjectInterface (one per table)
- an YYYObjectFactory (only one)



The configuration
------------

### Dir

The directory where all classes will be generated.


### Prefix

The prefix to strip from the table name, in order to compute the class name (the class name is guessed
from the table name).


### factoryClassName

The first part of the generated factory class name.
The complete factory class name is computed like this:

- $factoryClassName . $classSuffix . "Factory"


### namespace

The namespace to add at the top of the generated classes.


### classSuffix

By default, the generated XXXObjects class name is computed like this:

- $className . $classSuffix

$className is derived from the table name, and $classSuffix defaults to "Object" (but you can change it if you want).

If you change it, it will affect the name of all generated objects (XXXObject, XXXObjectInterface and YYYObjectFactory).

For instance if you set it to Item, the generated objects will be XXXItem, XXXItemInterface and YYYItemFactory.


### overwriteExisting

Whether to overwrite an existing file.

The default value is false.

If true, the generated objects will overwrite previously the generated objects (based on the configuration).


### generate

Array.

Defines the tables selection.

Two options are possible:

- prefix: string, use this to specify the prefix of the tables you want to select
- tables: array, specify the tables that you want manually


Note: the prefix is always separated from the rest of the table name by an underscore.
In other words, if your prefix is lud, then the **generate** option will select all the tables which name starts
with "lud_" (for instance lud_user, lud_permission, ...).








 