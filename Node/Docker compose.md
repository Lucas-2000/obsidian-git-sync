Abaixo tem um exemplo de arquivo docker-compose.yml para criação de um container simples contendo o postgres.

```
version: '3.7'

  

services:

  postgres:

    image: bitnami/postgresql:latest

    ports:

      - '5433:5432'

    environment:

      - POSTGRES_USER=postgres

      - POSTGRES_PASSWORD=docker

      - POSTGRES_DB=nome_do_banco

    volumes:

      - obreron_pg_data:/bitnami/postgresql

  

volumes:

  obreron_pg_data:
```