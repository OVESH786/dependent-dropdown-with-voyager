# dependent-dropdown-with-voyager
Dependent Dropdown with Voyager
 
# Install
Download zip https://github.com/d3turnes/dependent-dropdown-with-voyager/archive/master.zip or
composer require d3turnes/dependent-dropdown-with-voyager
 
Edit the file routes/api.php and add the following code

```php

use Illuminate\Http\Request;

/*
|--------------------------------------------------------------------------
| API Routes
|--------------------------------------------------------------------------
|
| Here is where you can register API routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| is assigned the "api" middleware group. Enjoy building your API!
|
*/

Route::middleware('auth:api')->get('/user', function (Request $request) {
   return $request->user();
});

Route::group(['prefix' => 'v1', 'as' => 'api.v1.', 'namespace' => 'Api\\V1\\'], function() {
   Route::post('/dependent-dropdown', ['uses' => 'DependentDropdownController@index', 'as' => 'dropdown']);
});

```

Edit the file app/Providers/AppServiceProvider.php and add the following code

```php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use TCG\Voyager\Facades\Voyager;

use App\FormFields\SelectDependentDropdown;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        Voyager::addFormField(SelectDependentDropdown::class);
    }

    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        //
    }
}

```
