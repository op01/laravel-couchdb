# laravel-couchdb

CouchDB database driver for Laravel 5.5+

## Dependencies

*laravel-couchdb* uses [doctrine/couchdb](https://github.com/doctrine/couchdb).

## Installation

`composer require bnbwebexpertise/laravel-couchdb`.

For laravel 5.5 and older, add the service provider in `app/config/app.php`:

```php
'Bnb\Laravel\CouchDb\CouchDbServiceProvider',
```

When using CouchDB connections, Laravel will automatically provide you with the corresponding CouchDB objects.

## Configuration

Change your default database connection name in `app/config/database.php`:

```php
'default' => 'couchdb',
```

And add a new couchdb connection:

```php
'couchdb' => [
    'driver'   => 'couchdb',
    'type'     => 'socket',
    'host'     => 'localhost',
    'ip'       => null,
    'port'     => 5984,
    'dbname'   => 'database',
    'user'     => 'username',
    'password' => 'password',
    'ssl'      => false,
    'logging'  => false,
    'timeout'  => 15,
],
```
## Examples

```php
/**
 * @var \Bnb\Laravel\CouchDb\CouchDbConnection
 */
$connection = DB::connection('couchdb');

/**
 * @var \Doctrine\CouchDB\CouchDBClient
 */
$couchdb = $connection->getCouchDB();
```

**Create/Update/Find Document example**

```php
$connection = DB::connection('couchdb');
$couchdb = $connection->getCouchDB();

list($id, $rev) = $connection->postDocument(array('foo' => 'bar'));
$couchdb->putDocument(array('foo' => 'baz'), $id, $rev);
$doc = DB::connection('couchdb')->findDocument($id);
```

All three methods can be called on $connection or $couchdb.

