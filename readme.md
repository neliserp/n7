# test packages

```
composer require laravel/ui

composer require laravel/sanctum

php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
```

add `EnsureFrontendRequestsAreStateful` to the list of `api` middleware in `app/Http/Kernel.php`

```php
// app/Http/Kernel.php

namespace App\Http;

// ...
use Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful;

class Kernel extends HttpKernel
{
    // ...
    protected $middlewareGroups = [
        // ...
        'api' => [
            EnsureFrontendRequestsAreStateful::class,
            // ...
        ],
```

Edit `.env`

```
$ vi .env
...
SANCTUM_STATEFUL_DOMAINS=your-domain.test
SESSION_DOMAIN=.your-domain.test
```

Protect api route

```php
// routes/api.php

Route::middleware('auth:sanctum')->get('/user', function (Request $request) {
    return $request->user();
});
```


edit default redirect `HOME`

```php
// app/Providers/RouteServiceProvider.php

    public const HOME = '/api/user';
```

