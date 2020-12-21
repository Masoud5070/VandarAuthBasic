# VandarAuthBasic

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Total Downloads][ico-downloads]][link-downloads]
[![Build Status][ico-travis]][link-travis]
[![StyleCI][ico-styleci]][link-styleci]

This package implements the laravel's default `auth.basic` middleware for vandar services:

## Installation

Via Composer

```bash
$ composer require masoud5070/vandarauthbasic
```

If you do not run Laravel 5.5 (or higher), then add the service provider and alias in `config/app.php`:

On the `config\app.php` add this to the `providers` array value:

```php
"Masoud5070\VandarAuthBasic\VandarAuthBasicServiceProvider"
```

and this one on the `alias` array value:  

```php
"VandarAuthBasic" => "Masoud5070\VandarAuthBasic\Facades\VandarAuthBasic"
```

## Usage

First publish config file and select `vandarauthbasic.config` tag with the command below:

```bash
$ php artisan vendor:publish
```

After config file was published you can change `model_name` with your model and set your data that create into database with `database_records`.

**NOTE:** When change `model_name` with your model class, table name will automatically change with `$table` of model. 

**NOTE:** You should set `ADMINS_TABLE_EMAIL` and `ADMINS_TABLE_PASSWORD` on the `.env` file, then run the migration for creating the table:   

```bash
$ php artisan migrate
```

To generate the admin user into the `admins` table run the command below:  

```bash
$ php artisan vandar:admins-consideration
```

**NOTE:** This package uses `Admin` model and `admins` table by default.  

Then add guard and provider to 'auth.php' config file:

```php
'guards' => [
         'admin' => [
             'driver' => 'session',
             'provider' => 'admins',
         ],
    
         ...
    ],   

'providers' => [
         'admins' => [
             'driver' => 'eloquent',
             'model' => \Masoud5070\VandarAuthBasic\Models\Admin::class,
         ],
    ],
```


After running this command and setting the provider, you can set the `auth.basic:web` middleware on the routes you want:  

```php
$ Route::get('your-uri', 'YourController@method')->middleware('auth.basic:web');
```

## Change log

Please see the [changelog](changelog.md) for more information on what has changed recently.

## Testing

``` bash
$ composer test
```

## Contributing

Please see [contributing.md](contributing.md) for details and a todolist.

## Security

If you discover any security related issues, please email author email instead of using the issue tracker.

## Credits

- [Masoud Haji Ali Tajer][link-author]
- [All Contributors][link-contributors]

## License

MIT. Please see the [license file](license.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/masoud5070/vandarauthbasic.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/masoud5070/vandarauthbasic.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/masoud5070/vandarauthbasic/master.svg?style=flat-square
[ico-styleci]: https://styleci.io/repos/12345678/shield

[link-packagist]: https://packagist.org/packages/masoud5070/vandarauthbasic
[link-downloads]: https://packagist.org/packages/masoud5070/vandarauthbasic
[link-travis]: https://travis-ci.org/masoud5070/vandarauthbasic
[link-styleci]: https://styleci.io/repos/12345678
[link-author]: https://github.com/masoud5070
[link-contributors]: ../../contributors
