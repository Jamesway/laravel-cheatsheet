## Laravel Cheatsheet

### Routes  
```
# routes/web.php
# {data} becomes a variable named $data and MyController@lookup specifies calls the lookup method in MyController
Route::get('{data}', 'MyController@lookup')->where('data', '^(?:10\.[^\s]+\/)[^\s]+$');
```  

### Controllers  
```
php artisan make:controller DoiController

class DoiController extends Controller
{

    public function __construct()
    {

      //
    }

    public function lookup($data) {

        return "helloworld";
    }
}
```


### Dependency Container
```
# you can make your own service provider
php artisan make:provider MyAppProvider

# or use the default AppServiceProvider class included in Laravel
# App\Providers\AppServiceProvider {}

# singleton
$this->app->singleton('App\DoiService\IDoiRepo', function () {

    return new \App\Infrastructure\RedisRepo(
        new \Predis\Client([
            "scheme" => "tcp",
            "host" => getenv("REDIS_HOST"),
            "port" => getenv("REDIS_PORT"),
            "password" => getenv("REDIS_PASSWORD")
        ])
    );
});

# bind
$this->app->bind('App\ICurlRequest', 'App\Infrastructure\Curl');
```
