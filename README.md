

# generator Laravel package 


## Overview
This is a Laravel package to generate your code 



## Installation :
You can install `asz/generator` via Composer by adding `"asz/generator": "^1.0"` 
as requirement to your composer.json. 
OR : 
```bash
composer require asz/generator
```
```bash
composer dump-autoload
```

### Service Provider:

go to your config/app.php file and add : 
```bash
 generator\GenServiceProvider::class ,
```
#### Publishing Config file :
```bash 
$ php artisan vendor:publish --tag="config.generator"
```
```bash
$ php artisan config:cache
```


this packege will generate :
* Migration file with data type  columns 
Here is example when Generate TestingTable : 
```bash 
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTestingTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('testing', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email');
            $table->string('phone_number');
            $table->string('slug');
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('testing');
    }
}

```
* Model with specific table name and fillable all table columns  .
continue with same  example when Generate TestTable : 
```bash 
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Testing extends Model
{

    protected $table = 'Testing';
    protected $fillable=["name","email","phone_number","slug"] ;


}

```

* Request File with default required validation.
continue with same  example when Generate TestTable : 
```bash
<?php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class TestingRequests extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize()
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            'name' => 'required',
            'email' => 'required',
            'phone_number' => 'required',
            'slug' => 'required'
        ];
    }
}
```

* controller with default methods and generate.
continue with same  example when Generate TestTable : 
```bash
<?php
namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use Illuminate\Http\Request;
use App\Models\Testing;
use App\Http\Requests\TestingRequests;

class TestingController extends Controller
{

    public function index()
    {
        //
    }

    public function create()
    {
        //
    }


    public function store(TestingRequests $request )
    {
        Testing::create($request->all());
    }


    public function show($id)
    {
        $Testing = Testing::findOrFail($id);
    }

    public function edit($id)
    {
        $Testing = Testing::findOrFail($id);
    }


    public function update(TestingRequests $request, $id)
    {
         $Testing = Testing::findOrFail($id);
         $Testing->update($request->all());

    }


    public function destroy($id)
    {
       $Testing = Testing::findOrFail($id);
       $Testing->delete();
    }
}
```

*Routes Generates and can choose your middleware "default null"
continue with same  example when Generate TestTable : 

```bash 
Route::group(['prefix' => 'testing', 'middleware' => ''], function () {
    Route::get('/', [App\Http\Controllers\testingController::class, 'index']);
    Route::post('/store', [App\Http\Controllers\testingController::class, 'store']);
    Route::post('/edit/{id}', [App\Http\Controllers\testingController::class, 'edit']);
    Route::put('/update/{id}', [App\Http\Controllers\testingController::class, 'update']);
    Route::delete('/destroy/{id}', [App\Http\Controllers\testingController::class, 'destroy']);
    Route::get('/show/{id}', [App\Http\Controllers\testingController::class, 'show']);
});
```

