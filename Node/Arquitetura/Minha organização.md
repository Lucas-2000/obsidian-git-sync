Para organizar meus diretórios, sigo os princípios de separação em camadas para ficar melhor a organização mas fiz umas adaptações para o meu caso.
Primeiramente crio uma pasta src para colocar todos os diretórios dentro desse.
Dentro do diretório src crio as pastas:
- config: para colocar os arquivos de configuração das libs.
- controllers: para colocar os arquivos controladores de cada entidade para seus respectivos casos de uso.
- models: para colocar as classes com as entidades.
- useCases: para colocar os casos de uso de cada entidade.
- utils: para colocar arquivos com funções que serão úteis em múltiplos arquivos de outros diretórios.
- repositories: para criar os repositórios de cada entidade, além de criar os repositórios em memória e para cada orm.
- factories: para colocar as factories que injetam os controladores, casos de uso e repositórios.
- routes: para colocar as rotas da aplicação.
- http: para colocar os arquivos referentes ao servidor (express, fastify, elysia, etc).

Depois na raiz do projeto crio uma pasta teste e recrio todos esses diretórios nela, para colocar os testes referentes a cada uma das funcionalidades do projeto.