Para configurar envio de email precisamos colocar os campos no settings.py

```
# Email

EMAIL_BACKEND = os.getenv("EMAIL_BACKEND")

EMAIL_HOST = os.getenv("EMAIL_HOST")

EMAIL_PORT = os.getenv("EMAIL_PORT")

EMAIL_USE_TLS = os.getenv("EMAIL_USE_TLS")

EMAIL_HOST_USER = os.getenv("EMAIL_HOST_USER")

EMAIL_HOST_PASSWORD = os.getenv("EMAIL_HOST_PASSWORD")
```

```
# Reset senha

PASSWORD_RESET_SUBJECT = os.getenv("PASSWORD_RESET_SUBJECT")

PASSWORD_RESET_MESSAGE = os.getenv("PASSWORD_RESET_MESSAGE")
```

em views.py

```
    path("reset-senha/", auth_views.PasswordResetView.as_view(), name='password_reset'),

    path('reset-senha-enviar/', auth_views.PasswordResetDoneView.as_view(), name='password_reset_done'),

    path('reset-senha/<uidb64>/<token>/', auth_views.PasswordResetConfirmView.as_view(), name='password_reset_confirm'),

    path('reset-senha-completado/', auth_views.PasswordResetCompleteView.as_view(), name='password_reset_complete'),
```

Podemos ter views personalizadas utilizando a propriedade template_name dentro do as_views().