# Laravel

## Instalação com Composer
Instale a ultima versão do composer (https://getcomposer.org/) e crie/instale com o comando:
* `composer create-project laravel/laravel my_first_laravel`
  
## Configurar o aplicativo Laravel
* `laravel new {nome-do-projeto}`
* Acessa diretório do projeto `cd {nome-do-projeto}`

## Alterar dados de acesso ao BD 
* deve colocar as credenciais de acesso no `.env`

## Testar conexão com banco de dados
* `php artisan tinker`
* `DB::connection()->getPdo();`

### Tem que retornar um PDO:

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
## Rodar o Servidor
* `php artisan serve`

## Criar Model
```
php artisan make:model Student -m
```
Este comando irá criar o `Model Student` em `app\Models` e seu respectivo arquivo de `migration` em `database\migrations`:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Student extends Model
{
    use HasFactory;
    
    protected $table = 'students';

    // define os campos que podem ser atribuídos em massa
    protected $fillable = ['name', 'course'];
}
```
### Migration
```php
...
public function up(): void
{
   Schema::create('students', function (Blueprint $table) {
       $table->id();
       // estes campos (name e course) podem ser usados na propriedade fillable
       $table->string('name');
       $table->string('course');
       $table->timestamps();
   });
}
...
```
Então, já pode executar a migração usando o seguinte comando:
```
php artisan migrate
```
## Configurar as rotas
### Criar um controlador com o comando:
```
php artisan make:controller StudentController
```
* Criará um o controlado `StudentController.php` em `app\http\controllers`
* Então podemos criar os metodos nele:
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

use App\Models\Student;

class StudentController extends Controller
{
    public function getAllStudents() {
        $students = Student::get()->toJson(JSON_PRETTY_PRINT);
        return response($students, 200);
    }

    public function createStudent(Request $request) {
        $student = new Student;
        $student->name = $request->name;
        $student->course = $request->course;
        $student->save();

        return response()->json([
            "message" => "student record created"
        ], 201);
    }

    public function getStudent($id) {
        if (Student::where('id', $id)->exists()) {
            $student = Student::where('id', $id)->first()->toJson(JSON_PRETTY_PRINT);
            return response($student, 200);
        } else {
            return response()->json([
                "message" => "Student not found"
            ], 404);
        }
    }

    public function updateStudent(Request $request, $id) {
        if (Student::where('id', $id)->exists()) {
            $student = Student::find($id);
            $student->name = is_null($request->name) ? $student->name : $request->name;
            $student->course = is_null($request->course) ? $student->course : $request->course;
            $student->save();
    
            return response()->json([
                "message" => "records updated successfully"
            ], 200);
        } else {
            return response()->json([
                "message" => "Student not found"
            ], 404);   
        }
    }

    public function deleteStudent ($id) {
        if(Student::where('id', $id)->exists()) {
            $student = Student::find($id);
            $student->delete();
    
            return response()->json([
              "message" => "records deleted"
            ], 202);
        } else {
            return response()->json([
                "message" => "Student not found"
            ], 404);
        }
    }
}

```

### Criar as rotas
* Criamos as rotas em `routes\api.php`:
```php
...
Route::get('students', [ApiController::class, 'getAllStudents']);
Route::get('students/{id}', [ApiController::class, 'getStudent']);
Route::post('students', [ApiController::class, 'createStudent']);
Route::put('students/{id}', [ApiController::class, 'updateStudent']);
Route::delete('students/{id}',[ApiController::class, 'deleteStudent']);
...
```
