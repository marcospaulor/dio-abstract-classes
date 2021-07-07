# DIO - Conceitos e melhores práticas com bancos de dados PostgreSQL :elephant:

## Fundamentos

- ### O que são dados?

  Valores brutos,  fatos brutos, observações documentadas, registros soltos, que são recolhidos e armazenados sem sofre qualquer tratamentos. 

- ### O que são informações?

  Estruturação de dados, organização de dados. Conjunto de dados relacionados entre si que geram valor, que criam sentidos aos dados. "Material do conhecimento".

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

  <u>Exemplo: Oracle Database, MySQL, Microsoft SQL Server, mongoDB e o próprio PostgreSQL</u>

## Instalação PostgreSQL

- ### Ubuntu

  `Site oficial`: [https://www.postgresql.org/download/linux/ubuntu/](PostgreSQL - Ubuntu)

  `Documentação`: [https://www.postgresql.org/docs/](Docs)

  Primeiro insira o seguinte comando para criar um arquivo, já inserindo o conteúdo necessário:

  ```bash
  sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
  ```

  A importação do repositório:

  ```bash
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
  ```

  Para melhor efetuar a instalação efetue um `update`:

  ```bash
  sudo apt-get update
  ```

  E por fim a instalação da última versão:

  ```
  sudo apt-get -y install postgresql
  ```

  

- ### Windows

  Utilizando os mesmo sites para modificando somente o endereço de instalação

  `Site Oficial`: [https://www.postgresql.org/download/windows/](PostgreSQL - Windows)

  O passo a passo do Windows não tem muito segredo. Geralmente segue o padrão de instalação indicado.

  Possíveis alterações:

  - Diretório de DATA, onde irá armazenar os dados
  - Senha do usuário Postgres
  - Pode modificar a porta (5432 - Porta padrão de instalação)

  Após a instalação, você pode procurar pelos services do Windows, `Win+P` e digite "services", para modificar a inicialização automática (Recomendado manter o automático).



