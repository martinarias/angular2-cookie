# angular2-cookie  [![Build Status](https://travis-ci.org/salemdar/angular2-cookie.svg?branch=1.0.0)](https://travis-ci.org/salemdar/angular2-cookie) [![npm version](https://badge.fury.io/js/angular2-cookie.svg)](http://badge.fury.io/js/angular2-cookie) [![Downloads](http://img.shields.io/npm/dm/angular2-cookie.svg)](https://npmjs.org/package/angular2-cookie)

> Implementation of Angular 1.x $cookies service to Angular 2 **v1.0.0**

## Table of contents:
- [Get Started](#get-started)
  - [Installation](#installation)
  - [Usage](#usage)
- [CookieService](#cookieservice)
  - [get()](#get)
  - [getObject()](#getobject)
  - [getAll()](#getall)
  - [put()](#put)
  - [putObject()](#putobject)
  - [remove()](#remove)
  - [removeAll()](#removeall)
- [Options](#options)
- [Overriding default options globally](#overriding-default-options-globally)

## <a name="get-started"></a> Get Started

### <a name="installation"></a> Installation

You can install this package locally with npm.

```bash
# To get the latest stable version and update package.json file:
npm install angular2-cookie --save
```

After installing the library, you should include it in the `index.html` file.

```html
<head>
  <base href="/">
  <title>My Very Cool App</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <link rel="stylesheet" href="styles.css">

  <!-- 1. Load libraries -->
  <!-- IE required polyfills, in this exact order -->
  <script src="node_modules/es6-shim/es6-shim.min.js"></script>
  <script src="node_modules/systemjs/dist/system-polyfills.js"></script>
  <script src="node_modules/angular2/es6/dev/src/testing/shims_for_IE.js"></script>

  <script src="node_modules/angular2/bundles/angular2-polyfills.js"></script>
  <script src="node_modules/systemjs/dist/system.src.js"></script>
  <script src="node_modules/rxjs/bundles/Rx.js"></script>
  <script src="node_modules/angular2/bundles/angular2.dev.js"></script>

  <!-- Include angular2-cookie library -->
  <script src="node_modules/angular2-cookie/bundles/angular2-cookie.min.js"></script>

  <!-- 2. Configure SystemJS -->
  <script>
    System.config({
      packages: {
        "app": {
          format: 'register',
          defaultExtension: 'js'
        }
      }
    });
    System.import('app/main')
            .then(null, console.error.bind(console));
  </script>

</head>
```

### <a name="usage"></a> Usage

**CookieService** class is an injectable service with angular `@Injectable()` decorator. Therefore, it needs to be registered in the providers array (encouraged way).
Then, it will be available in the constructor of the component class.

```typescript
import {Component} from 'angular2/core';
import {CookieService} from 'angular2-cookie/core';

@Component({
    selector: 'my-very-cool-app',
    template: '<h1>My Angular2 App with Cookies</h1>',
    providers: [CookieService]
})

export class AppComponent { 
  constructor(private _cookieService:CookieService){}
  
  getCookie(key: string){
    return this._cookieService.get(key);
  }
}
```

## <a name="cookieservice"></a> CookieService

There are 7 methods available in the `CookieService` (6 standard methods from **Angular 1** and 1 extra `removeAll()` method for convenience)

### <a name="get"></a> get()
Returns the value of given cookie key.

```typescript
/**
 * @param {string} key Id to use for lookup.
 * @returns {string} Raw cookie value.
 */
get(key: string): string;
```

### <a name="getobject"></a> getObject()
Returns the deserialized value of given cookie key.

```typescript
/**
 * @param {string} key Id to use for lookup.
 * @returns {Object} Deserialized cookie value.
 */
getObject(key: string): Object;
```

### <a name="getall"></a> getAll()
Returns a key value object with all the cookies.

```typescript
/**
 * @returns {Object} All cookies
 */
getAll(): any;
```

### <a name="put"></a> put()
Sets a value for given cookie key.

```typescript
/**
 * @param {string} key Id for the `value`.
 * @param {string} value Raw value to be stored.
 * @param {CookieOptionsArgs} options (Optional) Options object.
 */
put(key: string, value: string, options?: CookieOptionsArgs): void;
```

### <a name="putobject"></a> putObject()
Serializes and sets a value for given cookie key.

```typescript
/**
 * @param {string} key Id for the `value`.
 * @param {Object} value Value to be stored.
 * @param {CookieOptionsArgs} options (Optional) Options object.
 */
putObject(key: string, value: Object, options?: CookieOptionsArgs): void;
```

### <a name="remove"></a> remove()
Remove given cookie.

```typescript
/**
 * @param {string} key Id of the key-value pair to delete.
 * @param {CookieOptionsArgs} options (Optional) Options object.
 */
remove(key: string, options?: CookieOptionsArgs): void;
```

### <a name="removeall"></a> removeAll()
Remove all cookies.

```typescript
/**
 */
removeAll(): void;
```

## <a name="options"></a> Options

Options object should be a type of `CookieOptionsArgs` interface. The object may have following properties:

- **path** - {string} - The cookie will be available only for this path and its sub-paths. By default, this is the URL that appears in your `<base>` tag.
- **domain** - {string} - The cookie will be available only for this domain and its sub-domains. For security reasons the user agent will not accept the cookie if the current domain is not a sub-domain of this domain or equal to it.
- **expires** - {string|Date} - String of the form "Wdy, DD Mon YYYY HH:MM:SS GMT" or a Date object indicating the exact date/time this cookie will expire.
- **secure** - {boolean} - If `true`, then the cookie will only be available through a secured connection.

## <a name="overriding-default-options-globally"></a> Overriding default options globally

`CookieService` can use `ANGULAR2_COOKIES_PROVIDERS` to provide default options. Thus the default options can be altered by overriding the necessary class.
See [Angular dependency injection guide](https://angular.io/docs/ts/latest/guide/dependency-injection.html#the-provide-function) for more information on the topic.

```typescript
import {provide} from 'angular2/core';
import {bootstrap} from 'angular2/platform/browser';
import {App} from './myapp';

class MyOptions extends BaseCookieOptions {
  path: string = '/my/path/';
}

bootstrap(App, [ANGULAR2_COOKIES_PROVIDERS, provide(CookieOptions, {useClass: MyOptions})]);
```


### <a name="notes"></a> _Note_

_The build process and the file structure of this repository has respectively modeled after the awesome [angular2-google-maps](https://github.com/SebastianM/angular2-google-maps) project of [Sebastian Müller](http://twitter.com/Sebamueller)._