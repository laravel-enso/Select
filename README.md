<!--h-->
# Select
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/c6799b0705d34fdab5cd100e7cfe6312)](https://www.codacy.com/app/laravel-enso/Select?utm_source=github.com&utm_medium=referral&utm_content=laravel-enso/Select&utm_campaign=badger)
[![StyleCI](https://styleci.io/repos/85489940/shield?branch=master)](https://styleci.io/repos/85489940)
[![License](https://poser.pugx.org/laravel-enso/select/license)](https://packagist.org/packages/laravel-enso/select)
[![Total Downloads](https://poser.pugx.org/laravel-enso/select/downloads)](https://packagist.org/packages/laravel-enso/select)
[![Latest Stable Version](https://poser.pugx.org/laravel-enso/select/version)](https://packagist.org/packages/laravel-enso/select)
<!--/h-->

Bulma Select based on [vue-multiselect](https://github.com/monterail/vue-multiselect) with a server side option list builder

[![Watch the demo](https://laravel-enso.github.io/select/screenshots/bulma_031.png)](https://laravel-enso.github.io/select/videos/bulma_demo_01.webm)

<sup>click on the photo to view a short demo in compatible browsers</sup>

### Features

- a VueJS wrapper component for [vue-multiselect](https://github.com/shentao/vue-multiselect)
- CSS styling matches the beautiful [Bulma](https://bulma.io/) forms design
- the select options can be retrieved via ajax calls or, given directly, via a parameter
- when getting the data via ajax, the component can take various parameters for results filtering
- for the back-end, the package comes with a trait for easy retrieval and formatting of the data 
as expected by the VueJS component
- can filter the option list dynamically even based on the model’s one-to-many / many-to-many relationships
- can search in multiple attributes of a model
- can specify the attribute used as label for the select options

### Usage

The VueJS component is already included in the Enso install and should not require any additional installation steps

1. Use the `OptionBuilder` trait in your desired Controller

2. Define an `options` route for your Controller (and permissions as required)

3. Declare inside your controller the `$class` property as shown below:
	
	`protected $class = Model::class`
	
	where `Model::class` will be the Model used by the builder to extract the list of options
	
	By default it will use the model’s `name` attribute as a label for the select option list - but this is customizable - and the `id` for the key. 
	See the options bellow for details.
	
5. In your page/component add:

    ```
    <vue-select 
        source="/pathForSelectOptionsRoute" multiple        
        :selected="selectedOption"
        :params="params"
        :pivot-params="pivotParams"        
        :custom-params="customParams">
    </vue-select>
    ```

### Options

#### VueSelect VueJS component options 

In order to work, the component needs a data source. The data source can be a path for server-side, OR a formatted object. 
Either a `source` or an `options` parameter is required.

- `source` - string, route to use when getting the select options **only for server-side**. | default `null`
- `options` - object, list of options, **only where you don't need server-side**. Options must be properly formatted | default `{}`
- `value` - the selected option(s). Can be a single value or an Array if the select is used as a multi-select | default `null` |  (optional)
- `disabled` - boolean, flag that sets the element as disabled | default `false` | (optional)
- `multiple` - boolean, flag that makes the element work as a multiselect, if omitted, the select acts as single select | default `false` | (optional)
- `taggable` - boolean, flag the allows the creation of new tags | default `false` | (optional)
- `hasError` - boolean, flag sets an error styling for the select, like when validation fails | default `false` | (optional)
- `optionsLimit` - number, parameter that limits the number of options loaded from the backend and is synchronized with multiselect's own limit | default `100` | (optional)
- `params` - object, attributes from the same table/model used for filtering results in server-side mode. 
Format: `params: { 'fieldName': fieldValue }` | default `null` | (optional)
- `pivotParams` - object, attributes from linked tables/models used for filtering results in server-side mode. 
Format: `pivotParams: { 'table': {'attribute':value} }` | default `null` | (optional)
- `customParams` - object, can be anything. 
Using customParams implies that you rewrite the 'options' method from the OptionBuilder Trait. 
- `placeholder` - custom placeholder when no option is selected | default 'Please choose' | (optional)
- `labels` - object, the labels used inside the component | default `{ selected: 'Selected', select: 'Press enter to select', deselect: 'Press enter to deselect', noResult: 'No Elements Found' }` | (optional)


#### VueSelectFilter component options 
Takes the following parameters:	
- `title` - string, the title to display above the options | default `null` | (optional)	
- `value` -  the selected value from the list of options | default null | required	
	
Since this component is a wrapper for `VueSelect`, and all listeners and attributes are passed-through,	
the regular `VueSelect` options are available

#### OptionBuilder trait options

- `$class`, string, the fully qualified namespace of the class that we're querying on, in order to get the select options | default `null` | required
- `$queryAttributes`, array with the list of attributes we're searching in, when getting the select options | default `['name']` | (optional) 
- `$label`, string, the attribute that we're going to be using for the label of each option | default `'name'` | (optional)
- `$appends`, array, list of appended attributes that need to be added to the query results. Note that the appended attributes are available from the main query model | default `[]` | (optional)
- `query()`, a method the will return the query builder that we're using when querying for options | default `null` | (optional)

Note: If a query method is provided, it's going to be used, if it's not given, a query will be constructed, using the given class and other values.

### Publishes

- `php artisan vendor:publish --tag=select-assets` - the main VueJS components and their dependencies
- `php artisan vendor:publish --tag=enso-assets` - a common alias for when wanting to update the VueJS assets,
once a newer version is released, can be used with the `--force` flag

### Notes

You cannot use model computed attributes to display attributes when using the server-side mode of the select.

When using within [Laravel Enso](https://github.com/laravel-enso/enso), you can have the server-side route permissions generated automatically, when creating permissions for a resource controller, from the System/permissions menu.

The [Laravel Enso Core](https://github.com/laravel-enso/Core) package comes with this package included.

<!--h-->
### Contributions

are welcome. Pull requests are great, but issues are good too.

### License

This package is released under the MIT license.
<!--/h-->