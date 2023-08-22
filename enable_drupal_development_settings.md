# How to Enable Development Settings on a Drupal Project

In this guide, you will learn how to enable development settings on a Drupal project such as disabling caches, enabling Twig debug comments and displaying detailed error messages.

## Before You Begin

Set up a [new](set_up_new_drupal_project.md) or [existing](set_up_existing_drupal_project.md) Drupal project.

## Enabling Development Settings

### 1. Create `development.services.yml`

The `development.services.yml` file provides additional parameters and services for development environments.

Create a new file named `development.services.yml` in `web/sites/default` and insert the following text:

```
parameters:
  twig.config:
    debug: true
services:
  cache.backend.null:
    class: Drupal\Core\Cache\NullBackendFactory
```

This will enable Twig debug comments and provide a null cache to disable caching.

### 2. Create and edit `settings.local.php`

The `settings.local.php` file contains additional Drupal settings for development environments.

Copy the example file to `web/sites/default`:

```
cp web/sites/example.settings.local.php web/sites/default/settings.local.php
```

Open the file and make the following edits:

**a) Update the path to `development.services.yml`**

Change this:

```
$settings['container_yamls'][] = DRUPAL_ROOT . '/sites/development.services.yml';
```

To this:

```
$settings['container_yamls'][] = DRUPAL_ROOT . '/sites/default/development.services.yml';
```

**b) Uncomment the lines that disable caches**

Find these lines and uncomment them (remove the leading `#`):

```
# $settings['cache']['bins']['render'] = 'cache.backend.null';
```

```
# $settings['cache']['bins']['discovery_migration'] = 'cache.backend.memory';
```

```
# $settings['cache']['bins']['page'] = 'cache.backend.null';
```

```
# $settings['cache']['bins']['dynamic_page_cache'] = 'cache.backend.null';
```

### 3. Load the `settings.local.php` file

Open the `settings.php` file in `web/sites/default` and uncomment the following lines at the bottom of the file (remove the leading `#`):

```
#
# if (file_exists($app_root . '/' . $site_path . '/settings.local.php')) {
#   include $app_root . '/' . $site_path . '/settings.local.php';
# }
```
