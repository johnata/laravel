# Construindo uma API RESTful
## Instalação via composer
* `composer create-project laravel/laravel laravel-api`

## Configuração
Ao terminar a instalação, acesse a pasta criada (`laravel-api`) e abra o projeto em seu editor de preferência (ex. com vscode `code .`).

Antes de iniciar o desenvolvimento de nosso serviço RESTful, precisamos remover um middleware padrão a partir da versão 5 do Laravel. Vem como padrão um middleware para previnir CSRF. Como estamos construindo uma API, esse middleware não tem sentido.

Para remove-lo, vamos até a pasta app/Http e abrimos o arquivo Kernel.php e removemos a seguinte linha:
* `\App\Http\Middleware\VerifyCsrfToken::class,`

Também podemos remover alguns arquivos inuteis como nossa view default `welcome.blade.php` dentro de `resources/views` e qualquer controller default que a app tenha criado dentro de `app/Http/Controllers`.

Vamos configurações da nossa API utilizando o `.env`, recurso adicionado na versão 5 do framework. Vamos renomear o arquivo `.env.example` para apenas `.env`, e adicionar algumas como banco de dados:
`
APP_ENV=local
APP_DEBUG=true
APP_KEY=8952SICq2sEylIP3C5LSInEnjIRwaeFT

DB_HOST=localhost
DB_DATABASE=laravel-api
DB_USERNAME=root
DB_PASSWORD=root

CACHE_DRIVER=file
SESSION_DRIVER=file
QUEUE_DRIVER=sync

MAIL_DRIVER=smtp
MAIL_HOST=mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
`
