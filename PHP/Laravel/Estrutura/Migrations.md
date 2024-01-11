As migrations funcionam como versionamento do banco de dados, podendo avançar e retroceder por elas a qualquer momento. Vantagens de utilizar migrations:
- Adicionar e remover colunas de forma facilitada.
- Fazer o setup do banco de uma nova instalação em apenas um comando.

Para criar uma migration devemos executar o comando:

```
php artisan make:migration nome_migration
```

Para verificar as migrations podemos utilizar o comando:

```
migration:status
```

Quando precisamos adicionar um novo campo a uma tabela, devemos utilizar uma migration. Porém devemos tomar cuidado para não rodar o comando fresh e apagar os dados já existentes.

O comando rollback pode ser utilizado para voltar uma migration. Para voltar todas devemos utilizar o comando reset. Para voltar todas e rodar o migrate novamente devemos utilizar o comando refresh.