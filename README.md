Bugsnag Notifier for Laravel
============================

The Bugsnag Notifier for Laravel gives you instant notification of errors and
exceptions in your Laravel PHP applications.

[Bugsnag](https://bugsnag.com) captures errors in real-time from your web, 
mobile and desktop applications, helping you to understand and resolve them 
as fast as possible. [Create a free account](https://bugsnag.com) to start 
capturing errors from your applications.

Check out this excellent [Laracasts screencast](https://laracasts.com/lessons/better-error-tracking-with-bugsnag) for a quick overview of how to use Bugsnag with your Laravel apps.


How to Install
--------------

### Using [Laravel Package Installer](https://github.com/rtablada/package-installer) (Recommended)

1.  Install the bugsnag/bugsnag-laravel package

    ```shell
    $ php artisan package:install bugsnag/bugsnag-laravel
    ```

### Using [Composer](http://getcomposer.org/)

1.  Install the `bugsnag/bugsnag-laravel` package

    ```shell
    $ composer require "bugsnag/bugsnag-laravel:1.*"
    ```

2.  Update `app/config/app.php` and add a new item to the providers array:

    ```
    'Bugsnag\BugsnagLaravel\BugsnagLaravelServiceProvider'
    ```
    
3.  Finally update `app/config/app.php` and add a new item to the aliases array:

    ```
    'Bugsnag' => 'Bugsnag\BugsnagLaravel\BugsnagFacade'
    ```


Configuration
-------------

1.  Generate a template Bugsnag config file

    ```shell
    $ php artisan config:publish bugsnag/bugsnag-laravel
    ```

2.  Update `app/config/packages/bugsnag/bugsnag-laravel/config.php` with your
    Bugsnag API key:

    ```php
    return array(
        'api_key' => 'YOUR-API-KEY-HERE'
    );
    ```


Sending Custom Data With Exceptions
-----------------------------------

It is often useful to send additional meta-data about your app, such as 
information about the currently logged in user, along with any
error or exceptions, to help debug problems. 

To send custom data, you should define a *before-notify* function, 
adding an array of "tabs" of custom data to the $metaData parameter. For example:

```php
Bugsnag::setBeforeNotifyFunction("before_bugsnag_notify");

function before_bugsnag_notify($error) {
    // Do any custom error handling here

    // Also add some meta data to each error
    $error->setMetaData(array(
        "user" => array(
            "name" => "James",
            "email" => "james@example.com"
        )
    ));
}
```

See the [setBeforeNotifyFunction](https://bugsnag.com/docs/notifiers/php#setbeforenotifyfunction)
documentation on the `bugsnag-php` library for more information.


Sending Custom Errors or Non-Fatal Exceptions
---------------------------------------------

You can easily tell Bugsnag about non-fatal or caught exceptions by 
calling `Bugsnag::notifyException`:

```php
Bugsnag::notifyException(new Exception("Something bad happened"));
```

You can also send custom errors to Bugsnag with `Bugsnag::notifyError`:

```php
Bugsnag::notifyError("ErrorType", "Something bad happened here too");
```

Both of these functions can also be passed an optional `$metaData` parameter,
which should take the following format:

```php
$metaData =  array(
    "user" => array(
        "name" => "James",
        "email" => "james@example.com"
    )
);
```


Additional Configuration
------------------------

The [Bugsnag PHP Client](https://bugsnag.com/docs/notifiers/php)
is available as `Bugsnag`, which allows you to set various
configuration options, for example:

```php
Bugsnag::setReleaseStage("production");
```

See the [Bugsnag Notifier for PHP documentation](https://bugsnag.com/docs/notifiers/php#additional-configuration)
for full configuration details.


Reporting Bugs or Feature Requests
----------------------------------

Please report any bugs or feature requests on the github issues page for this
project here:

<https://github.com/bugsnag/bugsnag-laravel/issues>


Contributing
------------

-   [Fork](https://help.github.com/articles/fork-a-repo) the [notifier on github](https://github.com/bugsnag/bugsnag-laravel)
-   Commit and push until you are happy with your contribution
-   Run the tests to make sure they all pass: `composer install && ./vendor/bin/phpunit`
-   [Make a pull request](https://help.github.com/articles/using-pull-requests)
-   Thanks!


License
-------

The Bugsnag Laravel notifier is free software released under the MIT License. 
See [LICENSE.txt](https://github.com/bugsnag/bugsnag-php/blob/master/LICENSE.txt) for details.