# Laravel

## Instalação com Composer
Instale a ultima versão do composer (https://getcomposer.org/) e crie/instale com o comando:
* `composer create-project laravel/laravel my_first_laravel`

## Testar conexão com banco de dados
* `php artisan tinker`
* `DB::connection()->getPdo();`

tem que retornar um PDO:

```
PDO {#3334
     inTransaction: false,
     attributes: {
       CASE: NATURAL,
       ERRMODE: EXCEPTION,
       AUTOCOMMIT: 1,
       PERSISTENT: false,
       DRIVER_NAME: "mysql",
       SERVER_INFO: "Uptime: 8695  Threads: 2  Questions: 41  Slow queries: 0  Opens: 109  Flush tables: 1  Open tables: 18  Queries per second avg: 0.004",
       ORACLE_NULLS: NATURAL,
       CLIENT_VERSION: "mysqlnd 8.0.0",
       SERVER_VERSION: "5.7.24",
       STATEMENT_CLASS: [
         "PDOStatement",
       ],
       EMULATE_PREPARES: 0,
       CONNECTION_STATUS: "127.0.0.1 via TCP/IP",
       DEFAULT_FETCH_MODE: BOTH,
     },
   }
   ```
## Servidor
* `php artisan serve`

## Creating Model
```
php artisan make:model Student -m
```
This will create a model named `Student` and also its corresponding migration file in the database

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Student extends Model
{
    protected $table = 'students';

    protected $fillable = ['name', 'course'];
}

```
The `$fillable` property specifies which columns can be mass assigned to this table from an incoming

```php
...
public function up()
{
    Schema::create('students', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name');
        $table->string('course');
        $table->timestamps();
    });
}
...
```
In the above code, we have created two fields for our students' information. The first field is the student's name (`$table->string('name')`) while the second one is their course (`$table->string('course')`)). We've set these as fillable using the `$fillable property`.

```
php artisan migrate
```
## Creating Controller
```
php artisan make:controller ApiController
```
This will create a Control named `ApiController` in `app\http\controllers`

Create the methods
```php
...
class ApiController extends Controller
{
    public function getAllStudents() {
      // logic to get all students goes here
    }

    public function createStudent(Request $request) {
      // logic to create a student record goes here
    }

    public function getStudent($id) {
      // logic to get a student record goes here
    }

    public function updateStudent(Request $request, $id) {
      // logic to update a student record goes here
    }

    public function deleteStudent ($id) {
      // logic to delete a student record goes here
    }
}
```

