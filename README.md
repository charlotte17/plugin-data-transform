# Data Transform Plugin for Pattern Lab

This plugin now only works with Twig PatternEngine. You can use old 0.x versions of the plugin for Mustache PatternEngine.


## Installation

To install and use the plugin run:

```sh
composer require aleksip/plugin-data-transform
```


## Features

### Pattern-specific data file support for included patterns

Pattern Lab core only supports global data files and a pattern-specific data file for the main pattern. This plugin adds pattern-specific data file support for included patterns.


### Data transform functions

Currently the plugin provides 3 transform functions for the data read by Pattern Lab. The examples provided are in JSON but Pattern Lab supports YAML too!


#### Include pattern files

If a value contains the name of a pattern in shorthand partials syntax, the plugin will replace the value with the rendered pattern:

```json
{
    "key": "atoms-form-element-label.html"
}
```

Advanced syntax with support for passing variables and disabling access to the default data:

```json
{
    "key": {
        "include()": {
            "pattern": "atoms-form-element-label.html",
            "with": {
                "title": "Textfield label"
            },
            "only": true
        }
    }
}
```

In both examples the value of `key` will replaced with the rendered pattern.


#### Join text values

```json
{
    "key": {
        "join()": [
            "molecules-comment.html",
            "<div class=\"indented\">",
            "molecules-comment.html",
            "</div>",
            "molecules-comment.html"
        ]
    }
}
```

The value of `key` will be replaced with the joined strings. Note that in the example `molecules-comment.html` is the name of a pattern in shorthand partials syntax. These will be replaced with the rendered pattern before the join.


#### Create Drupal `Attribute` objects

```json
{
    "key": {
        "Attribute()": {
            "id": ["edit-submit"],
            "type": ["submit"],
            "value": ["Submit"],
            "class": ["button", "button-primary"]
        }
    }
}
```

The value of `key` will be replaced with an [Attribute object](https://www.drupal.org/node/2513632).


## Global data and includes

Please note that global data from the `_data` directory is considered to be pattern-specific data and will overwrite data inherited from a parent pattern. If you want to override data of an included pattern you can use the `with` keyword.


## More examples

All features provided by this plugin are used extensively in [Shila Drupal Theme StarterKit](https://github.com/aleksip/starterkit-shila-drupal-theme).
