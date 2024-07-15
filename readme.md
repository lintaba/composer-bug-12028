This is an issue repo for [composer/composer#12028](https://github.com/composer/composer/issues/12028) 

```shell
php composer-276.phar install -o

Composer could not detect the root package (lintaba/cfix) version, defaulting to '1.0.0'. See https://getcomposer.org/root-version
Installing dependencies from lock file (including require-dev)
Verifying lock file contents can be installed on current platform.
Nothing to install, update or remove
Generating optimized autoload files
Warning: Ambiguous class resolution, "Content" was found in both "~/classes/Content.php" and "~/vendor/x/y/classes/Content.php", the first will be used.
```

vs

```bash
php composer-277.phar install -o

Composer could not detect the root package (lintaba/cfix) version, defaulting to '1.0.0'. See https://getcomposer.org/root-version
Installing dependencies from lock file (including require-dev)
Verifying lock file contents can be installed on current platform.
Nothing to install, update or remove
Generating optimized autoload files
Warning: Ambiguous class resolution, "Content" was found in both "~/vendor/x/y/classes/Content.php" and "~/classes/Content.php", the first will be used.
```

Old version (2.7.6) resolved for ~/classes/Content.php first, new version (2.7.7) resolves for ~/vendor/x/y/classes/Content.php


Moreover, it's only in the optimize-autoload in 2.7.7:
```bash
> php composer-277.phar install
Installing dependencies from lock file (including require-dev)
Verifying lock file contents can be installed on current platform.
Nothing to install, update or remove
Generating autoload files
> php test.php
THIS

> php composer-277.phar install -o
Installing dependencies from lock file (including require-dev)
Verifying lock file contents can be installed on current platform.
Nothing to install, update or remove
Generating optimized autoload files
Warning: Ambiguous class resolution, "Content" was found in both "~/vendor/x/y/classes/Content.php" and "~/classes/Content.php", the first will be used.
> php test.php
THAT
```
