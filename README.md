## Run source
First please copy .env.example to .env
```
cd storage/
mkdir -p framework/{sessions,views,cache}
chmod -R 775 framework

cd ..
docker-compose up --build
docker-compose exec php bash

composer install
composer dump-autoload

php artisan key:generate
php artisan migrate:fresh --seed

```

## Notes
- API url: http://localhost:8080
- PHP myAdmin url: http://localhost:8888

## API endpoints
```
+--------+-----------+------------------+---------------+------------------------------------------------+------------+
| Domain | Method    | URI              | Name          | Action                                         | Middleware |
+--------+-----------+------------------+---------------+------------------------------------------------+------------+
|        | GET|HEAD  | api/users        | users.index   | App\Http\Controllers\V1\UserController@index   | api        |
|        | POST      | api/users        | users.store   | App\Http\Controllers\V1\UserController@store   | api        |
|        | GET|HEAD  | api/users/{user} | users.show    | App\Http\Controllers\V1\UserController@show    | api        |
|        | PUT|PATCH | api/users/{user} | users.update  | App\Http\Controllers\V1\UserController@update  | api        |
|        | DELETE    | api/users/{user} | users.destroy | App\Http\Controllers\V1\UserController@destroy | api        |
+--------+-----------+------------------+---------------+------------------------------------------------+------------+
```

## Run Unit Test

    docker-compose exec php bash
    php -dxdebug.mode=coverage vendor/bin/phpunit --coverage-clover='reports/coverage/coverage.xml' --coverage-html='reports/coverage'

## Run Unit Test with Coverage Reports

    docker-compose exec php bash
    php artisan test

