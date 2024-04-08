## Requisitos Funcionais

- [ ] Deve ser possível controlar todos os grupos, pessoas e usuários a partir do painel de controle;
- [ ] A equipe Halley deve poder controlar todos os cadastros e indicadores a partir de um painel de administrador;
- [ ] Deve ser possível criar tickets;
- [ ] Deve ser possível categorizar tickets;
- [ ] Deve ser possível cadastrar grupos e pessoas (que abriram chamados e quem irá atender os chamados);
- [ ] Deve ser possível cadastrar empresa;
- [ ] Deve ser possível vincular pessoa e grupos a essa empresa;
- [ ] Deve ser possível rotear automaticamente para pessoas;
- [ ] Deve ser possível acompanhar/rastrear o status;
- [ ] Deve ser possível informar o usuário de atualização de status e notas;
- [ ] Deve ser possível definir SLAs personalizados;
- [ ] Deve ser possível registrar o histórico dos tickets;
- [ ] Deve ser possível visualizar um dashboard contendo informações sobre o atendimento dos; tickets;
- [ ] Deve ser possível filtrar tickets;
- [ ] Deve ser possível enviar pesquisa de satisfação para o usuário pós atendimento;
- [ ] Deve ser possível fazer upload de imagens para compor o ticket;

## Requisitos Não Funcionais

- [ ] Cadastro do administrador da empresa deve ser feito pela equipe do Halley;
- [ ] Backend deverá ser feito em Node utilizando Fastify como framework e Prisma como ORM;
- [ ] Frontend deverá ser feito em Vue;
- [ ] Banco de dados deverá ser Postgres;

## Regras de Negócio

- [ ] Deve ser possível visualizar chamados ativos e inativos;
- [ ] Só deve ser possível fazer upload de imagens de até 10 mb;
- [ ] Apenas o administrador da empresa pode controlar os cadastros existentes;