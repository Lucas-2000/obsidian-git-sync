Documentação: [https://docs.djangoproject.com/en/4.1/ref/contrib/messages/](https://docs.djangoproject.com/en/4.1/ref/contrib/messages/)

Nossa biblioteca tem essas configurações de mensagens ativas. Que funciona perfeitamente, mas precisamos renderizar isso no _frontend_. Como estamos utilizando _bootstrap_ precisamos adicionar essa configuração no _settings.py_ do seu projeto. Adicionando essa configuração as mensagens de alerta aparecerá com as classes do bootstrap.

_**core/settings.py**_

```
# --- Messages --- #
from django.contrib.messages import constants

MESSAGE_TAGS = {
	constants.ERROR: 'alert-danger',
	constants.WARNING: 'alert-warning',
	constants.DEBUG: 'alert-danger',
	constants.SUCCESS: 'alert-success',
	constants.INFO: 'alert-info',
}
```

Criei uma pasta **components** e dentro vou colocar os components que podem ser reutilizados em varias paginas. _**base/templates/components/message.html**_

```
{% if messages %}
<div class="messages">
    {% for message in messages %}
    <div {% if message.tags %} class="alert {{ message.tags }} alert-dismissible fade show"{% endif %} role="alert">
        {{ message }}
        <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
    </div>
    {% endfor %}
</div>
{% endif %}
```

**Adiciona na base**

```
<body> 
	{% include 'components/message.html' %} ## adiciona isso.
	{% block content %}{% endblock %} 
</body>
```

testar

```
messages.success(request, 'Esta é uma mensagem de sucesso!')
```

