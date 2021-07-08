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

  `Site oficial`: [https://www.postgresql.org/download/linux/ubuntu/]()

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

  `Site Oficial`: [https://www.postgresql.org/download/windows/]()

  O passo a passo do Windows não tem muito segredo. Geralmente segue o padrão de instalação indicado.

  Possíveis alterações:

  - Diretório de DATA, onde irá armazenar os dados
  - Senha do usuário Postgres
  - Pode modificar a porta (5432 - Porta padrão de instalação)

  Após a instalação, você pode procurar pelos services do Windows, `Win+P` e digite "services", para modificar a inicialização automática (Recomendado manter o automático).



## Configurações do PostgreSQL

- ### `postgresql.conf`

  `Definição`: arquivo onde estão definidas e armazenadas todas as configurações do servidor PorstgreSQL.

  Alguns parâmetros só podem ser alterados com um reinicialização do banco de dados.

  A view `pg_settings`, acessada por dentro do banco de dados, guarda todas as configurações atuais.

  - Configurações mais importantes

    As configurações de `conexão`:

    - `LISTEN_ADDRESSES`: endereços TCP/IP das interfaces que o servidor PostgreSQL vai escutar/liberar conexões.
    - `PORT`: porta TCP que o servidor PostgreSQL via ouvir. (A padrão é a 5432).
    - `MAX_CONNECTIONS`: número máximo de conexões simultâneas no servidor PostgreSQL.
    - `SUPERUSER_RESERVED_CONNECTIONS`: número de conexões (slots) reservados para conexão ao banco de dados de super usuários.

    As configurações de `autenticação`:

    - `AUTHENTICATION_TIMEOUT`: tempo máximo em segundos para o cliente conseguir uma conexão com o servidor.
    - `PASSWORD_ENCRYPTION`: algoritmo de criptografia das senhas dos novos usuários criados no banco de dados.
    - `SLL`: habilita a conexão criptografada por SLL. (caso se o PostgreSQL foi compilado com o suporte SSL)

    As configurações de `memória`:

    - `SHARED_BUFFERS`: tamanho da memória compartilhada do servidor PostgreSQL para cache/buffer de tabelas, índices e demais relações.
    - `WORK_MEM`: tamanho da memória para operações de agrupamento e ordenação (*ORDER BY*, *DISTINCT*,*MERGE JOINS*).
    - `MAINTENCE_WORK_MEM`: tamanho da memória para operações com *VACUUM*, *INDEX*, *ALTER TABLE*.

- ### `pg_hba.conf`

  `Definição`: arquivo responsável pelo controle de autenticação dos usuários no servidor PostgreSQL.

  - Métodos de `autenticação`:

    - `TRUST`: conexão sem requisição de senha. 
    - `REJECT`: rejeitar conexões;
    - `MD5`: criptografia md5
    - `PASSWORD`: senha sem criptografia
    - `GSS`: generic security service application program interface.
    - `SSPI`: security suporte provider interface - *somente para windows*.
    - `KRB5`: kerberos V5.
    - `IDENT`: utiliza o usuário do sistema operacional do cliente via ident server;
    - `PEER`: utiliza o usuário do sistema operacional do cliente.
    - `LDAP`: ldap server.
    - `RAIUS`: radius server.
    - `CERT`: autenticação via certificado ssl do cliente.
    - `PAM`: pluggable authentication modules. O usuário precisa estar no banco.

    **Exemplo:**

    ```shell
    #TYPE   |   DATABASE |   USER  | ADDRESS     | METHOD
    local   |   all      |   all   |             | peer
    #IPv4 local connections:
    host    |   all      |   all   | 127.0.0.1/32|	md5
    ```
  
- ### `pg_ident.conf`

  `Definição`: arquivo responsável por mapear os usuários do sistema operacional como os usuários do banco de dados. Localizado no diretório de dados PGDATA de sua instalação. A opção ident deve ser utilizada no arquivo pg_hba.conf.

  **Exemplo:**

  ```shell
  #	MAPNAME	    |  SYSTEM-USERNAME	|  PG-USERNAME
  	diretoria   |   marcos			|  pg_diretoria
  	comercial   |   fulano			|  pg-comercial
  ```

- ### `Comandos administrativos`

  **Ubuntu**:

  - `pg_lscluters`: lista todos os clusters PostgreSQL.
  - `pg_createcluster <version> <cluster name>`: cria um novo cluster PostgreSQL.
  - `pg_dropcluster <version> <cluster>`: apaga um cluster PostgreSQL
  - `pg_cllcluster <version> <cluster> <action>`: *START*, *STOP*, *STATUS*, *RESTART* de clusters PostgreSQL.

  **Windows**:

  Como dito antes é simples, basta iniciar o serviço do postgresql-<versão> no sistema de serviços do Windows, caso ele não esteja com inicialização automática.

- ### `Binários PostgreSQL`

  - `ceatedb`
  - `createuser`
  - `dropdb`
  - `dropuser`
  - `initdb`
  - `pg_clt`
  - `pg_basebackup`
  - `pg_dump / pg_dumpall`
  - `pg_restore`
  - `psql`
  - `reindexdb`
  - `vacuumdb`

- ### `Arquitetura / Hierarquia`

  - `Cluster`: coleção de banco de dados que compartilhamos as mesmas configurações (arquivos de configuração) do PostgreSQL e do sistema operacional (porta, listen_addresses, etc).
  - `Banco de dados (Database)`:  conjunto de **schemas** com seus objetos/relações (tabelas, funções, views, etc).
  - `Schema`: conjunto de objetos/relações (tabelas, funções, views, etc).

## PGAdmin

