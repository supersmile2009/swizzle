# Swizzle

Build [Guzzle](http://guzzlephp.org) service descriptions from [Swagger](https://helloreverb.com/developers/swagger) compliant APIs.

### What?

 - Guzzle is a framework for building HTTP clients in PHP.
 - Swagger is a specification for describing RESTful services.

Although Guzzle's service descriptions are [heavily inspiried](http://docs.guzzlephp.org/en/latest/webservice-client/guzzle-service-descriptions.html) by the Swagger spec, they are different enough that we need something to bridge the divide.

Swizzle crawls JSON Swagger docs ([such as ours](https://localise.biz/api/swagger)) and transforms it into a Guzzle service description for output into your client code.


## Installation

Installation is via [Composer](http://getcomposer.org/doc/00-intro.md#using-composer).

Add the latest stable version of [loco/swizzle](https://packagist.org/packages/loco/swizzle) to your project's composer.json file as follows:

```json
{
  "require": {
    "loco/swizzle": "~2.0"
  }
}
```

If you want to install straight from Github you'll have to write your own [autoloader](https://gist.github.com/jwage/221634) for now.


## Usage 

Basic usage is to configure, build and export - as follows:

```php 
$service = new Loco\Utils\Swizzle\Swizzle( 'foo', 'Foo API' );
$service->build('http://foo.bar/path/to/swagger/docs/');
// Serialize Guzzle service config to json
$json = $service->toJson();
file_put_contents('/path/to/config.json', $builder->toJson());
// Now use saved config.json in your project/library to create Guzzle service.
```

More advanced usage includes registering custom Guzzle classes for commands and responses. See [example](https://github.com/loco/swizzle/tree/master/example) directory for fuller, working examples.

Build the PHP API documentation with [apigen](http://apigen.org/) using `apigen -c apigen.yml`


### Limitations

This version was developed very quickly for our own API specifically. That means it's not guaranteed to support the whole Swagger spec. 

This library supports only version 1.2 of Swagger spec.
