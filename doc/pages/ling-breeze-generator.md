Ling Breeze Generator config
=================
2019-09-13 -> 2019-12-19


Config example
-------------
2019-12-19

```yaml

breeze_generator:
    instance: Ling\Light_BreezeGenerator\Service\LightBreezeGeneratorService
    methods:
        setContainer:
            container: @container()
        setConf:
            conf:
                lud:
                    class: Ling\Light_BreezeGenerator\Generator\LingBreezeGenerator
                    conf:
                        dir: ${app_dir}/tmp/Light_BreezeGenerator
                        prefix: lud
                        usePrefixInClassName: false
                        factoryClassName: LightUserDatabaseApiFactory
                        baseClassName: BaseLightUserDatabaseApi
                        namespace: Ling\Light_UserDatabase\Api\Mysql
                        classSuffix: Api
                        overwriteExisting: true
                        useMicroPermission: false
                        generate:
                            prefix: lud


```



The configuration
------------
2019-12-19


### Dir

Mandatory.
The directory which will contain all the generated classes.



### Prefix

Optional = null.

The prefix to strip from the table name, in order to compute the class name (the class name is guessed
from the table name).


### usePrefixInClassName

Optional = false.

Whether to keep the prefix in the generated class name. 


### factoryClassName

Mandatory.
The name of the generated factory class.



### baseClassName

Mandatory.
The name of the generated base class, which is the parent for all table based generated classes.


### namespace

Mandatory.
The namespace of all generated classes.


### classSuffix

Optional = "Object".


By default, the generated XXXObjects class name is computed like this:

- $className . $classSuffix

Note: $className is derived from the table name.



### overwriteExisting

Optional = false.

Whether to overwrite an existing file.

If true, the generated objects will overwrite previously the generated objects (based on the configuration).


### useMicroPermission

Optional = false.

Whether to use the micro-permission checking.
We use the [micro-permission recommended notation for database](https://github.com/lingtalfi/Light_MicroPermission/blob/master/doc/pages/recommended-micropermission-notation.md#database-interaction).



### generate

Mandatory.

It's an array which defines the tables selection.

Two options are possible, you must use one of them:

- prefix: string, use this to specify the prefix of the tables you want to select
- tables: array, specify the tables that you want manually


Note: the prefix is always separated from the rest of the table name by an underscore.
In other words, if your prefix is lud, then the **generate** option will select all the tables which name starts
with "lud_" (for instance lud_user, lud_permission, ...) in your database.




 
 
Adding custom methods
---------------------
2019-10-17


The generated code is a good start, but pretty soon a developer will want to add new methods.

At a semantic/organizational level, it makes sense that these developer "custom" methods are added to the api.

However, if we add them directly to the generated code, a problem occurs: what if we inadvertently make the 
generator overwrite the class? Well then we loose the custom code as well, that's not an option.

And so therefore let me introduce the concept of **Custom** methods.

The main idea is that the developer can add methods to the class, but without the risk to have his code overwritten.

For that, we choose a **custom** prefix, which defaults to "Custom", and can be changed from the configuration (customPrefix key).

Then in terms of organization we create a "Custom" (or whatever prefix you chose) directory where the class to are generated,
and inside this Custom directory we create our custom classes, which extend the class that we want to add methods to,
and which name is the custom prefix followed by the extended class name.


So for instance, let's say that we have the following generated structure:

```text
- app/universe/My/Path/Api/
----- DirectoryMapApi.php
----- DirectoryMapApiInterface.php
----- GeneratedApiFactory.php
```

To extend the DirectoryMapApi class, we transform the above structure into this:

```text
- app/universe/My/Path/Api/
----- DirectoryMapApi.php
----- DirectoryMapApiInterface.php
----- GeneratedApiFactory.php
----- Custom/
--------- CustomDirectoryMapApi.php
```

The generator will never overwrite whatever is in the "Custom" directory.

As a bonus, the generated factory will detect the custom classes and provide them if they exist.




 






  