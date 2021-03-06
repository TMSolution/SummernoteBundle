SummernoteBundle
================

What is SummernoteBundle?
-------------------------
Summernotebundle integrates [SummerNote](http://hackerwins.github.io/summernote/) WYSIWYG Editor into Symfony form type.

Status
------
[![Build Status](https://travis-ci.org/solilokiam/SummernoteBundle.svg?branch=master)](https://travis-ci.org/solilokiam/SummernoteBundle)
[![SensioLabsInsight](https://insight.sensiolabs.com/projects/5ac190d8-368d-463e-bdcf-eb414242de47/mini.png)](https://insight.sensiolabs.com/projects/5ac190d8-368d-463e-bdcf-eb414242de47)
[![Latest Stable Version](https://poser.pugx.org/solilokiam/summernotebundle/v/stable.png)](https://packagist.org/packages/solilokiam/summernotebundle)
[![Total Downloads](https://poser.pugx.org/solilokiam/summernotebundle/downloads.png)](https://packagist.org/packages/solilokiam/summernotebundle)
[![Latest Unstable Version](https://poser.pugx.org/solilokiam/summernotebundle/v/unstable.png)](https://packagist.org/packages/solilokiam/summernotebundle)
[![License](https://poser.pugx.org/solilokiam/summernotebundle/license.png)](https://packagist.org/packages/solilokiam/summernotebundle)

Requirements
------------
Minimum requirements for this bundle are:
- Symfony 2.3
- Twitter's Bootstrap 3.0
- jQuery 1.9

Installation
------------
Add SummernoteBundle to your application's `composer.json` file

```json
{
    "require": {
        "solilokiam/summernotebundle": "dev-master"
    }
}
```

Add SummernoteBundle to your application's `AppKernel.php` file

```php
new Solilokiam\SummernoteBundle\SolilokiamSummernoteBundle()
```

Add Routing information to your application's `routing.yml`:

```yml
solilokiam_summernote_bundle:
    resource: "@SolilokiamSummernoteBundle/Resources/config/routing.xml"
    prefix: /summernote
```

Minimal Configuration
---------------------
You must determine which object manager are you using. Currently it only supports Doctrine ODM, and doctrine ORM.

`app/config/config.yml`

```yml
solilokiam_summernote:
    db_driver: mongodb #supported orm,mongodb for odm
```

You must also tell which class is going to inherit the bundle asset class.

```yml
solilokiam_summernote:
    asset_class: Acme\DemoBundle\Document\Asset
```

An example for the asset class can be like this (doctrine odm):

```php
<?php

namespace Acme\DemoBundle\Document;


use Solilokiam\SummernoteBundle\Model\SummernoteAsset;
use Doctrine\ODM\MongoDB\Mapping\Annotations as MongoDB;

/**
 * Class Asset
 * @package Acme\DemoBundle\Document
 * @MongoDB\Document(collection="assets")
 */
class Asset extends SummernoteAsset
{
    /**
     * @MongoDB\Id(strategy="auto")
     */
    protected $id;

    ...
}

```

Additional Configuration
------------------------
Summernote supports some configuration parameters. This parameters can configured application wide in config.yml.

* **width**: This is the width of summernote widget
```yml
solilokiam_summernote:
   ...
   width: 500
```
* **focus**: Autofocus the widget.
```yml
 solilokiam_summernote:
    ...
    focus: true
```
* **toolbar**: Configure toolbars of the widget.Every line in toolbar config is a different button group. You can check available buttons at [summernote documentation](http://hackerwins.github.io/summernote/features.html#customtoolbar)
```yml
  solilokiam_summernote:
    ...
    toolbar:
        - { name: style, buttons: ['bold', 'italic', 'underline', 'clear'] }
        - { name: paragraph, buttons: ['ul', 'ol', 'paragraph']}
```

Usage
-----

Summernote bundle provides a formtype. This example form uses it:

```php
class TestFormType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        ...
        $builder->add('test_text', 'summernote');
        ...

    }
    ...

}
```

You need also to add some twig tags in your templates to import all CSS and JS needed to make summernote work:
```twig
...
{% block stylesheets %}
    {{ summernote_form_stylesheet(form) }}
{% endblock %}

{% block javascripts %}
    {{ summernote_form_javascript(form) }}
{% endblock %}
```

