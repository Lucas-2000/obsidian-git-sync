Condensa a maior parte de lógica das rotas, tem o papel de enviar e esperar resposta do banco de dados, além de receber e enviar resposta para as views, pode-se criar controler via artisan. É comum retornar uma view ou redirecionar para uma url pelo controller.

Para criar um controller devemos utilizar o comando:

```
php artisan make:controller NomeController
```