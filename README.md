###Why is this useful?

The RedisStore that comes with the Laravel Cache uses does not compress string data out of the box.
  The RedisStore in this package does. Caching string data may or may not make sense for your use case, 
  but can save a ton memory and/or network bandwidth depending on cached item size and request frequency.

###How do I use it?

Add a [custom cache driver](https://laravel.com/docs/5.3/cache#adding-custom-cache-drivers), like this...

```php
Cache::extend('ehann-redis', function ($app) {
    return Cache::repository(new \Ehann\Cache\RedisStore(
        app('redis'),
        app('config')['cache']['prefix'],
        app('config')['connection']
    ));
});
```

Add the **ehann-redis** custom driver to the redis store config in config/cache.php...

```php
    'stores' => [
        'redis' => [
            'driver' => 'ehann-redis',
        ],
    ],
```
