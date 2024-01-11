As páginas dos projetos são acessadas por meio de rotas, as rotas chamam as views.
Em casa view teremos os templates estruturando uma página HTML além de renderizar dados dinamicamente por meio do PHP.

Para criar uma view deve-se criar o arquivo dentro do diretório resources/views e usar a nomenclatura:
**exemplo.blade.php**

Para a view ser reconhecida como uma rota, deve-se acessar o diretório routes/web.php e adicionar a rota desejada:

```
Route::get('/', function () {

    return view('welcome');

});
```
