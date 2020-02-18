# Laravel 5 Probe Detection
Log and ban known website probing attacks and eliminate wasted site resources

## Minimum Requirements

Laravel 5.1 and PHP 5.5.9

## Installation

You can install the package via composer:

``` bash
composer require seanhayes-com/laravel5-probe-detection
```

## Step 2: Configuration

Add the following to your `config/app.php` in the `providers` array:

```php
SeanHayes\Probe\ProbeServiceProvider::class,
Torann\GeoIP\GeoIPServiceProvider::class,
```

You should also add the following to the `aliases` array:

```php
'Probe'     => SeanHayes\Probe\ProbeFacade::class,
'GeoIP'     => Torann\GeoIP\GeoIPFacade::class,
```

You can then publish the migration with:
```bash
php artisan vendor:publish --provider="SeanHayes\Probe\ProbeServiceProvider" --tag="migrations"
```

After the migration has been published you can create the `prob_log` table by running the migrations:

```bash
php artisan migrate
```

You can optionally publish the config file with:
```bash
php artisan vendor:publish --provider="SeanHayes\Probe\ProbeServiceProvider" --tag="config"
```

## Configuration

Change settings in config/probe.php

Add routes to handle certain common attack vectors or URIs added to watch_uris in config/probe.php

```php
Route::get('/wp-login.php', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
Route::get('/{name}/wp-login.php', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
Route::get('/wp-admin/', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
Route::get('/{name}/wp-admin/', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
Route::post('/wp-login.php', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
Route::post('/{name}/wp-login.php', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
Route::post('/wp-admin/', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
Route::post('/{name}/wp-admin/', function () {
	\SeanHayes\Probe\Probe::logRequest();
});
```

## Usage
Include the path in your Controller or AppServiceProvider

```php
use SeanHayes\Probe\Probe;
```
And the call to process the request in your method

```php
Probe::logRequest();
```
