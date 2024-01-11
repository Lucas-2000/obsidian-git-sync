Temos vários tipos de organização do seu projeto backend em node:
- DDD:  Na domain drive design, possuímos a camada de aplicação, de domain e de infra.
![[DDD.png]]
- Clean Architeture: Na clean architeture possuímos 3 camadas, a core, a adapters e a external. 
![[Clean Architeture.png]]

Os princípios para utilização de uma arquitetura em camadas são:
- Tornar o codigo testavel sem qualquer interferência do usuário, de framework ou banco de dados.
- Independência da UI, a interface do usuário pode variar sem impactar no restante do sistema.
- Independência de bancos de dados, seu código deve funcionar sem qualquer interferência de bancos de dados, validando suas regras de negócios por meio de um repositório em memória.
- Independente do Framework, o código deve funcionar sem qualquer interferência de um sistema externo.

Independente da arquitetura selecionada, devemos utilizar esses princípios para tornar o codigo melhor, mais escalável, mais legível teztavel.
