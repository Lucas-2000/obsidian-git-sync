“core” é nome do seu projeto e quando colocamos um “.” depois do nome do projeto significa que é para criar os arquivos na raiz da pasta. Assim não cria subpasta do projeto.

```
django-admin startproject core .
```

**Testar a aplicação**

```
python manage.py runserver
```

![[tela_inicial_django.png]]
Caso funcione irá aparecer essa tela acessando a url http://127.0.0.1:8000/
