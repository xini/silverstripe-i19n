# i19n - Innternationalization editor
I19n enables you to collect and edit system translations used on Silverstripe website (both backend and frontend).

## Requirements
- silverstripe/framework ~4
- silverstripe-terraformers/gridfield-rich-filter-header ~2

## Installation
1) run `composer require innovatif/i19n-editor "~1"` to install module
2) run `dev/build?flush=1`

For more see Configuration section.

## Configuration
### Translating themes folder
Silverstripe can treat folders as module if folder contains `_config.php`. You need to create empty config file inside `/themes` folder in order for text translator to be able to scan your templates.
Create empty file: `<your_project>/themes/_config.php`
Run `?flush=1`

### Default preselected modules
By default `app` and `themes` folder are pre-selected in scan for new translations popup. You can modify the list with:
```YAML
Innovatif\i19n\GridField\Button\GridFieldTranslateButton:
  preselected_modules:
    - app
    - themes
```

### Multi-server environment
Clear cache action clears cache on server side. You need additional controls on multi-server environment so all servers are notified to clear cache on their SS instance too.

You should set up a Cron job on every server (back-end and front-end servers) to executes task `/dev/tasks/i19nClearCacheTask` on every X minutes.

Enable setting in CMS
```YAML
Innovatif\i19n\Library\i19nLibrary:
  enable_clear_cache_task: true
```
Clear cache action now creates object in database which will tell all servers to clear cache when Cron job runs.

## Features
- export translations
	- downloads `.yml` if one locale is currently filtered
	- download  `.zip`  if more than one locale is filtered
- import translations 
	- only `.yml` files are currently supported so you can upload one language per import
	- language must exist in Fluent
- collector task for new translations
	- you can target CMS translations only or template translations only (this won't collect `db_`/`has_many_`/... field labels)
- you can manually add multiple translations for single i18n variable at once
	- can be disabled
- clear cache after changes
	- multi-server environment is supported
  
## Versioning
This library follows [Semver](http://semver.org) from tag 1.0. According to Semver, you will be able to upgrade to any minor or patch version of this library without any breaking changes to the public API. Semver also requires that we clearly define the public API for this library.

All methods, with `public` visibility, are part of the public API. All other methods are not part of the public API. Where possible, we'll try to keep `protected` methods backwards-compatible in minor/patch versions, but if you're overriding methods then please test your work before upgrading.

## Changelog
See CHANGELOG.md
 
## FAQ
Module works great with tractorcow/silverstripe-fluent but currently works only with versions 4.x and 5.x. Fluent version 6.x is supported by Silverstripe 5 since i18nTaskCollector cannot work with `__TRAIT__ ` constant.

## Authors and maintainers

Klemen Dolinšek (t3hn0)

Aljoša Balažič (aljosab)