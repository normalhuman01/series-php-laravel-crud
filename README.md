## Laravel: crear aplicaciones web en PHP

### Laravel: creando una aplicación con MVC

**¿Qué facilidades puede ofrecernos un framework full-stack como Laravel?**
- Ayuda con SQL (usando ORM), registros, manejo de errores, etc.

**Instalación de Laravel**
```
composer create-project laravel/laravel control-series ^9
```

**Definición de la primera ruta**
```php
php artisan
```

```php
php artisan serve
```

```php
php artisan serve --host=0.0.0.0 --port=8000
http://localhost:8000/series
```

**¿Cuál es la sintaxis para crear una nueva ruta en Laravel?**
```php
Route::{verbo http}('{tu ruta}', {Código a ejecutar});
```

- Podemos tener rutas con Route::get, Route::post, Route::put, Route::delete, etc.
- Todos los verbos HTTP son válidos aquí.

**Convenciones de nombres**
```php
php artisan make:controller SeriesController
```

```php
php artisan make:controller PhotoController --resource
```

**Manejo de Request y Response**
```php
$request->get('id');
$request->url();
$request->method();
$request->input();

response('', 302, ['Location' => 'https://google.com']);
redirect('https://google.com');
```

**¿Qué hace la función response?**
- Retorna un objeto de tipo ```Response``` con el cuerpo, estado y encabezados.

**Creación de un Layout**
```php
php artisan make:component Titulo
```

**¿Qué necesitamos hacer para tener un componente de blade?**
- Crear un archivo .blade.php en el directorio resources/views/components.

**Más funcionalidades**
```
@{{ nombre }}

const series = {{ json_encode($series) }};
const series = {{ Js::from($series) }};
```

**Entendiendo el concepto - Laravel Mix**
```
npm install
```

**Vite y Mix**
```
npm install laravel-mix --save-dev
```

**Laravel Mix**
- A pesar de ser recomendado por el equipo de Laravel, es un paquete de JavaScript.

**Instalación de Bootstrap**
```
npm install bootstrap
```

```
npm run dev
```

**¿Cuál es el propósito de la función asset?**
- Devolver la ruta de un recurso (archivo estático) que incluso puede estar en otro dominio.

**¿Por qué no debemos tener información sensible (como credenciales) en nuestro código?**
- Porque esto puede exponer nuestra seguridad.
- Porque podemos tener credenciales diferentes en entornos diferentes.

**Migraciones**
```php
php artisan make:migration create_series_table
php artisan migrate
```

**Además de simplemente ejecutar un CREATE TABLE, ¿qué otras ventajas obtenemos al utilizar migraciones?**
- Sincronización de bases de datos locales del equipo.
- Versionamiento de la base de datos.

**DB Facade**
```php
use Illuminate\Support\Facades\DB;

DB::select('SELECT nombre FROM series');
DB::insert('INSERT INTO series (nombre) VALUES (?)', [$nombreSerie]);
```

**CSRF (Cross-Site Request Forgery)**
- Laravel cuenta con protección contra un ataque llamado Cross-Site Request Forgery (CSRF).
- Cada formulario que enviamos a Laravel debe tener una información adicional: un token.
- Este token permite que Laravel verifique que la solicitud realmente fue enviada desde un formulario del sitio.
- Afortunadamente, agregar esta información es simple, simplemente utilizando la directiva ```@csrf``` de Blade.

**Eloquent ORM**
```php
php artisan make:model Serie
```

[Building Queries](https://laravel.com/docs/9.x/eloquent#building-queries)

### Laravel: validación de formularios, uso de sesiones y definición de relaciones

**Creación de series**
```php
Serie::create($request->all());
Serie::create($request->only(['nombre', 'genero']));
Serie::create($request->except(['_token']));
```
