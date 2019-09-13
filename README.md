Light_BreezeGenerator
===========
2019-09-11



A simple orm generator service with different flavours, for the [light](https://github.com/lingtalfi/Light) framework.


This is a [Light framework plugin](https://github.com/lingtalfi/Light/blob/master/doc/pages/plugin.md).

This is part of the [universe framework](https://github.com/karayabin/universe-snapshot).


Install
==========
Using the [uni](https://github.com/lingtalfi/universe-naive-importer) command.
```bash
uni import Ling/BreezeGenerator
```

Or just download it and place it where you want otherwise.






Summary
===========
- [BreezeGenerator api](https://github.com/lingtalfi/BreezeGenerator/blob/master/doc/api/Ling/BreezeGenerator.md) (generated with [DocTools](https://github.com/lingtalfi/DocTools))
- Pages
    - [Conception notes](https://github.com/lingtalfi/BreezeGenerator/blob/master/doc/pages/conception-notes.md)
    - [Ling breeze generator](https://github.com/lingtalfi/BreezeGenerator/blob/master/doc/pages/ling-breeze-generator.md)
- [Services](#services)



Services
=========


This plugin provides the following services:

- breeze_generator



Here is an example of the service configuration:

```yaml
breeze_generator:
    instance: Ling\Light_Bullsheet\Service\LightBullsheetService
    methods:
        setContainer:
            container: @container()
        setSilentMode:
            mode: true



```




History Log
=============

- 1.0.0 -- 2019-09-13

    - initial commit