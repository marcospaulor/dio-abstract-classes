# DIO - Conceitos e melhores práticas com bancos de dados PostgreSQL :elephant:

## Fundamentos

- ### O que são dados?

  Valores brutos,  fatos brutos, observações documentadas, registros soltos, que são recolhidos e armazenados sem sofre qualquer tratamentos. 

  [^Esta é uma de muitas definições.]: 

- ### O que são informações?

  Estruturação de dados, organização de dados. Conjunto de dados relacionados entre si que geram valor, que criam sentidos aos dados. "Material do conhecimento".

  [^Está é uma de muitas definições]:  

## Modelo Relacional

- ### Definição

  Modelo mais comum, que classifica e organiza as informações em tabelas com linhas e colunas. As `linhas`, ou `tuplas`, são os dados organizados, são o valores das tabelas, e as `colunas`  são os `atributos` destes dados.

- ### Tabelas

  Conjunto de dados dispostos em colunas e linhas referentes a um objetivo comum.

  - As `colunas` são consideradas como "campos da tabela", como atributos da tabela.

  - As `linhas` de uma tabela são chamados também de `tupulas`, e é onde estão contidos os valores, os dados.

- ### O que pode ser definido como tabelas?

  - Coisas tangíveis (Elementos físicos {carro, produto, animal});
  - Funções (Perfis de usuário, status de compra);
  - Eventos ou ocorrências (produtos de uma pedido, histórico de dados);

- ### Colunas importantes

  - `Chave Primária / Primary Key / PK`: conjunto de um ou mais campos que nunca se repetem. Identidade da tabela. São utilizados como índice de referência na criação de relacionamentos entre tabelas.
  - `Chave Estrangeira / Foreign Key / FK`: valor de referência a uma `PK` de outra tabela ou da mesma tabela para criar um relacionamento.

- ### Sistema de Gerenciamento de Banco de Dados

  Chamado pela sigla `SGBD`, é um conjunto de programas ou softwares responsáveis pelo gerenciamento de um banco de dados. Ou seja, programas que facilitam a administração de um banco de dados.

  [^Exemplo: Oracle Database, MySQL, Microsoft SQL Server, mongoDB e o próprio PostgreSQL ]: 

