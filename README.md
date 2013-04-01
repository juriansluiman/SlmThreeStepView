SlmThreeStepView
===
SlmThreeStepView is a module to abstract common parts of your layout script into a wrapper script. It lets you focus on the important things of the layout, leaving the general parts out of its scope. This helps with creation of new layouts (you need to remember less) and helps to concentrate on the important parts of the layout script.

The result is a wrapper view script, "surrounding" the layout. A wrapper might look something like this:

```html
<?= $this->doctype(); ?>

<html>
<head>
    <?= $this->headTitle() ?>
    <?= $this->headMeta() ?>
    <?= $this->headLink() ?>
    <?= $this->headScript() ?>
</head>

<body>
    <?= $this->content ?>
    <?= $this->inlineScript() ?>
</body>
</html>
```

The layout scripts you are used to work with, only need to contain the html within the `<body></body>` tags.

Installation
---
SlmThreeStepView is installable via composer. Require `slm/three-step-view` in your `composer.json`. You can use the development's version `dev-master` but also rely on the first tagged release (v0.1.0) by specifying `0.*` as version constraint. Then enable `SlmThreeStepView` in your `application.config.php`.

Usage
---
SlmThreeStepView let you configure the template of the wrapper script (defaults to `layout/wrapper`) and the variable the "inner" layout is captured to (defaults to `content`).

Furthermore, SlmThreeStepView allows a blacklist of layout scripts which are not turned into a three step version. This is useful when you use a module as ZfcAdmin for example, where the layout `layout/admin` is a full layout. By default, this blacklist is empty.

Create the file `slmthreestepview.config.global.php` in your `config/autoload` directory. You can use the following configuration options:

```php

return array(
    'slm_threestepview' => array(
        // Default value is layout/wrapper
        'template'   => 'layout/wrapper',

        // Default value is content
        'capture_to' => 'content',

        // Default value is empty array
        'blacklist'  => array('layout/admin')
    ),
);
```

Performance
---
You might wonder what the performance drop is by using this module. In a small-sized Zend Framework 2 application the module is benchmarked roughly with `ab`. In 1000 requests the drop in performance is on average 1ms (from 45.739ms to 46.649ms). The resolving of the templates is done via the template path stack (so no template map has been made). This means the real performance drop of this module is even less than the 1ms of the above benchmark.

Important!
---
This module requires a change in your Zend Framework 2 library. The change is requested to be pulled into the core via [this Pull Request](https://github.com/zendframework/zf2/pull/4164). Only after this merge has been made, this module is usable.

Development
---
This module is developed in a short time and might not be completely stable or ready for your needs. Please test is thoroughly befor you use it in production! If you have any problems, feel free to open an issue in the tracker. If you have questions, please mail them to jurian@juriansluiman.nl.