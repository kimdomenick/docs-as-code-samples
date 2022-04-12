# Running and maintaining a local Drupal site

**This is sample developer instructional doc with code/bash examples**

# Assumptions

* A container-based solution, like Lando, is installed and configured 

# Composer

Composer is a tool for dependency management in PHP. It allows you to
declare the libraries your project depends on and it will manage
(install/update) them for you.

See formal documentation: [Composer External Documentation][]

## The composer.lock file

Some projects version the composer.lock file. Others do not.  When the .lock file
is versioned, changes to it should be committed to the repository.

## Repositories

This project's `composer.json` file is configured to use packages.drupal.org and
asset-packagist.org to pull in dependencies through Composer. Drupal
extensions can be installed via Composer using the `drupal/*` package name.
Likewise, npm and packages can be installed from asset-packagist.org using
the `npm-asset/*` package name.

## Patches

You can patch composer dependencies with a local or remote patch file by
defining patches in `composer.json`. Patches are defined as follows:

```json
{
    "extra": {
        "patches": {
            "vendor/package": {
                "Description of patch": "https://domain.tld/files/file.patch"
            }
        }
    }
}
```

## Preserve paths

Drupal core files by default are ignored from version control, but there may be
a need to customize a file like `.htaccess`. If you add changes to a file like
`.htaccess` you will need to add it to the `preserve-paths` directive in
`composer.json` to prevent Composer from overwriting your changes. Preserved
paths are defined as follows:

```json
{
    "extra": {
        "preserve-paths": [
            "web/.htaccess"
        ]
    }
}
```

## Updating Drupal Core
For Drupal's full documentation, review the following:
[Updating Core][]

In summary, the following command can be run to update core, followed by the
command to run any database updates and export any changed configuration:
```bash
$ lando composer update drupal/core "drupal/core-*" --with-all-dependencies
$ lando drush updb && lando drush cr && lando drush cex
```

## Updating Contributed Modules
Before updating contrib modules, review the following document for information
on any locked versions, patches or special considerations:
[Cheap Home Staging][]

In summary, the following command can be run to update contrib modules, followed
by the command to run any database update and export any changed configuration.
```bash
$ lando composer update drupal/modulename --with-all-dependencies
$ lando drush updb && lando drush cr && lando drush cex
```


[Composer External Documentation]: https://getcomposer.org
[Cheap Home Staging]: /docs-as-code-samples/cheap-home-staging.html
[Updating Core]: https://www.drupal.org/docs/updating-drupal/updating-drupal-core-via-composer
