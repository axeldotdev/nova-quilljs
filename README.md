# Nova Quilljs

[![Latest Version on Packagist](https://img.shields.io/packagist/v/axeldotdev/quilljs.svg?style=flat-square)](https://packagist.org/packages/axeldotdev/quilljs)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/axeldotdev/quilljs/run-tests?label=tests)](https://github.com/axeldotdev/quilljs/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/axeldotdev/quilljs/Check%20&%20fix%20styling?label=code%20style)](https://github.com/axeldotdev/quilljs/actions?query=workflow%3A"Check+%26+fix+styling"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/axeldotdev/quilljs.svg?style=flat-square)](https://packagist.org/packages/axeldotdev/quilljs)

This package brings SEO tools like redirections manager, robot.txt manager, metadata field, structured data field.


## Installation

Install via composer
```
composer require axeldotdev/quilljs
```

## Modify quill's height, width, padding bottom

### **paddingBottom**(integer)
In nova interface was not easy to set css about quill padding bottom, at some resolution maybe can overlaps, you can use **paddingBottom** to modify.
```php
Quilljs::make(__('Content'), 'content')
        ->paddingBottom(30)
        ->withFiles('public')
        ->placeholder('please enter here')
        ->height(300)
        ->rules('required'),
```
### **fullWidth(value)**
Boolean

### **height(value)**
Number (unit px)
```
use Axeldotdev\Quilljs\Quilljs;

Quilljs::make('content')
        ->withFiles('public')
        ->fullWidth(false) (option, default full-width)
        ->height(500) (option, default 300px)
        ->rules('required'),
```

## **resize** and **align** image

I add this module https://github.com/Fandom-OSS/quill-blot-formatter , thanks for https://github.com/Fandom-OSS

## Image upload size

### **maxFileSize(size)**
size : Number, default 2(MB)
**example**
```
use Axeldotdev\Quilljs\Quilljs;

Quilljs::make('content')
        ->withFiles('public')
        ->maxFileSize(3)
        ->rules('required'),
```

## Image upload

This Nova field provides native attachments driver which works similar to [Trix File Uploads](https://nova.laravel.com/docs/4.0/resources/fields.html#trix-field).

To use this attachments driver, publish and run the migration(also publish quilljs config to set [toolbar](https://quilljs.com/docs/modules/toolbar/)):

```
php artisan vendor:publish --provider="Axeldotdev\Quilljs\FieldServiceProvider"
php artisan migrate
```

Then, allow users to upload images, just like with Trix field, chaining the withFiles method onto the field's definition. When calling this method, you should pass the name of the filesystem disk that images should be stored on(in this example, we use **public**, please use this command `php artisan storage:link` ):

```
use Axeldotdev\Quilljs\Quilljs;

Quilljs::make('content')
        ->withFiles('public')
        ->placeholder('please enter here')
        ->rules('required'),

```

### Work with other package [nova-translatable](https://github.com/optimistdigital/nova-translatable) and [nova-flexible-content](https://github.com/whitecube/nova-flexible-content)

When you use other packages like [nova-translatable](https://github.com/optimistdigital/nova-translatable) and [nova-flexible-content](https://github.com/whitecube/nova-flexible-content), they will overwrite upload api.

Ex: origin `your_host/nova-vendor/quilljs/articles/upload/content` ,
maybe overwrite to
`/nova-vendor/quilljs/articles/upload/content.en` or
`/nova-vendor/quilljs/articles/upload/content__SDAcscsdw`.

You can use
### **uploadUrlSplit(split_string)**
split_string : String
**example**

```
use Axeldotdev\Quilljs\Quilljs;

Quilljs::make('content')
        ->withFiles('public')
        ->placeholder('please enter here')
        ->uploadUrlSplit('.')
        ->rules('required')
        ->translatable(), // nova-translatable's method


```

## Customizing Tooltips

![](https://i.imgur.com/kSNwoUO.png)

In default, tooltip was disabled, if you want to use, in **Resource** add **->tooltip(true)**

```php=
Quilljs::make(__('Content'), 'content')
                ->withFiles('public')
                ->tooltip(true)
```

**in config/tooltip.php**

You can use favorite description of tooltip.

```php=
<?php

return [
        ['Choice' =>'.ql-bold','title' =>'bold'],
        ['Choice' =>'.ql-italic','title' =>'italic'],
        ['Choice' =>'.ql-underline','title' =>'underline'],
        ['Choice' =>'.ql-header','title' =>'header'],
        ['Choice' =>'.ql-strike','title' =>'strike'],
        ['Choice' =>'.ql-blockquote','title' =>'blockquote'],
        ['Choice' =>'.ql-code-block','title' =>'code-block'],
        ['Choice' =>'.ql-size','title' =>'font-size'],
        ['Choice' =>'.ql-list[value="ordered"]','title' =>'order list'],
        ['Choice' =>'.ql-list[value="bullet"]','title' =>'bulleted list'],
        ['Choice' =>'.ql-header[value="1"]','title' =>'h1'],
        ['Choice' =>'.ql-header[value="2"]','title' =>'h2'],
        ['Choice' =>'.ql-align','title' =>'align'],
        ['Choice' =>'.ql-color','title' =>'color'],
        ['Choice' =>'.ql-background','title' =>'background'],
        ['Choice' =>'.ql-image','title' =>'image'],
        ['Choice' =>'.ql-video','title' =>'video'],
        ['Choice' =>'.ql-link','title' =>'link'],
        ['Choice' =>'.ql-formula','title' =>'formula'],
        ['Choice' =>'.ql-clean','title' =>'clean'],
        ['Choice' =>'.ql-indent[value="-1"]','title' =>'indent left'],
        ['Choice' =>'.ql-indent[value="+1"]','title' =>'indent right'],
        ['Choice' =>'.ql-header .ql-picker-label','title' =>'header size'],
        ['Choice' =>'.ql-header .ql-picker-item[data-value="1"]','title' =>'H1'],
        ['Choice' =>'.ql-header .ql-picker-item[data-value="2"]','title' =>'H2'],
        ['Choice' =>'.ql-header .ql-picker-item[data-value="3"]','title' =>'H3'],
        ['Choice' =>'.ql-header .ql-picker-item[data-value="4"]','title' =>'H4'],
        ['Choice' =>'.ql-header .ql-picker-item[data-value="5"]','title' =>'H5'],
        ['Choice' =>'.ql-header .ql-picker-item[data-value="6"]','title' =>'H6'],
        ['Choice' =>'.ql-header .ql-picker-item:last-child','title' =>'normal'],
        ['Choice' =>'.ql-size .ql-picker-item[data-value="small"]','title' =>'small'],
        ['Choice' =>'.ql-size .ql-picker-item[data-value="large"]','title' =>'large'],
        ['Choice' =>'.ql-size .ql-picker-item[data-value="huge"]','title' =>'xlarge'],
        ['Choice' =>'.ql-size .ql-picker-item:nth-child(2)','title' =>'normal'],
        ['Choice' =>'.ql-align .ql-picker-item:first-child','title' =>'align left'],
        ['Choice' =>'.ql-align .ql-picker-item[data-value="center"]','title' =>'align center'],
        ['Choice' =>'.ql-align .ql-picker-item[data-value="right"]','title' =>'align right'],
        ['Choice' =>'.ql-align .ql-picker-item[data-value="justify"]','title' =>'justify']
];
```

## Customizing Quilljs Toolbar

If you want to change toolbar's setting, you can change quilljs.php in config folder, reference quilljs's web site https://quilljs.com/docs/modules/toolbar

```php=
return [
    ["bold", "italic", "underline", "strike"],
    ["blockquote", "code-block"],
    [ ['header'=> 1 ], ['header'=> 2]],
    [['list'=> "ordered" ], ['list'=> "bullet" ]],
    [[ 'script'=> "sub" ], [ 'script'=> "super" ]],
    [[ 'indent'=> "-1" ], [ 'indent'=> "+1" ]],
    [[ 'direction'=> "rtl" ]],
    [[ 'size'=> ["small", false, "large", "huge"] ]],
    [[ 'header'=> [1, 2, 3, 4, 5, 6, false] ]],
    [[ 'color'=> [] ], [ 'background'=> [] ]],
    [[ 'font'=> [] ]],
    [[ 'align'=> [] ]],
    ["clean"],
    ["link", "image", "video"]
];
```

or you can use new api `->config(array [])`.
```php=
Quilljs::make(__('Content'), 'content')
        ->config([
                ["bold", "italic", "underline", "strike"],
                ["blockquote", "code-block"],
                [ ['header'=> 1 ], ['header'=> 2]],
                [['list'=> "ordered" ], ['list'=> "bullet" ]],
                [[ 'script'=> "sub" ], [ 'script'=> "super" ]],
                [[ 'indent'=> "-1" ], [ 'indent'=> "+1" ]],
                [[ 'direction'=> "rtl" ]],
                [[ 'size'=> ["small", false, "large", "huge"] ]],
                [[ 'header'=> [1, 2, 3, 4, 5, 6, false] ]],
                [[ 'color'=> [] ], [ 'background'=> [] ]],
                [[ 'font'=> [] ]],
                [[ 'align'=> [] ]],
                ["clean"],
                ["link", "image", "video"]
        ]),

```

## Video embed

Only support **Youtube** **Facebook**，default size in Nova was **width 800px** and **height 450px**，define in css
```css
.ql-video{
  width: 800px;
  height: 450px;
}
```

### Youtube

* Example url https://www.youtube.com/watch?v=rgHqK6Dge4w

![](https://i.imgur.com/qNYYk91.png)

### Facebook

* Example Url https://www.facebook.com/standnewshk/videos/272770540314346/UzpfSTEzODQ4NjU1NDY6MTAyMjEzMDE0MDExMDk2MDM/

![](https://i.imgur.com/lqDj6Y4.png)

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](SECURITY.md) on how to report security vulnerabilities.

## Credits

- [axeldotdev](https://github.com/axeldotdev)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
