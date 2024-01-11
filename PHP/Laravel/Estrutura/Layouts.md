Para criar códigos reutilizáveis, precisamos criar um diretório layouts dentro de resources/views.

Criamos um arquivo com o nome exemplo.blade.php e digitamos um código base para ser reutilizado na aplicação, nesse aqui usaremos um body com um footer e todas informações de js e css.

```
<!DOCTYPE html>

<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">

    <head>

        <meta charset="utf-8">

        <meta name="viewport" content="width=device-width, initial-scale=1">

  

        <title>@yield("title")</title>

  

        <!-- Fonts -->

        <link rel="preconnect" href="https://fonts.bunny.net">

        <link href="https://fonts.bunny.net/css?family=figtree:400,600&display=swap" rel="stylesheet" />

  

        <link rel="stylesheet" href="/css/styles.css">

    </head>

    <body>

        @yield("content")

        <footer>

            <p>Foodshop &copy; 2024</p>

        </footer>

    </body>

    <script src="/js/script.js"></script>

</html>
```

Para deixar partes do código dinâmicas, utilizamos a diretiva yield e dentro dos () damos o nome para aquela sessão. Ou seja, nesse caso poderemos definir dinamicamente todo o conteúdo da página que obrigatoriamente terá um footer embaixo e o título da página.

Segue o código como exemplo para reutilização desse layout:

```
@extends("layouts.main")

  

@section("title", "Foodshop")

  

@section("content")

<body>

    <div class="container">

  

    <h1 class="text-3xl">Algum titulo</h1>

    @if (10 > 5)

    <p>Maior que 5</p>

     @endif

</div>

@endsection
```

Devemos fazer a extensão desse layout e definir os valores para cada section, assim tornando os dados dela dinâmico de acordo com sua página.