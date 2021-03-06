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
  	diretoria   |   marcos          |  pg_diretoria
  	comercial   |   fulano          |  pg-comercial
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

`Site oficial`: [https://www.pgadmin.org/]()

`Documentação`:[https://www.pgadmin.org/docs/pgadmin4/latest/index.html]()

**Importante para conexão:**

1. Liberar acesso ao cluster em `postgresql.conf`
2. Liberar acesso ao cluster para o usuário do banco de dados em `pg_hba.conf`
3. Criar/editar usuários

*Não tem muito o que falar sobre pois é interface gráfica, geralmente a documentação possui tudo.*

## Configurando Usuários

- #### `Conceitos de Users/Roles/Groups`

  `Definição`:

  ​	**Roles** (*papéis ou funções*), **users** (*usuários*) e **grupo de usuários** são "*contas*", perfis de atuação em um bando de dados, que possuem permissões em comum ou específicas.

  *Há a possibilidade de que roles pertençam a outras roles.*

- #### `Administrando Users/Roles/Groups`

  Alguns privilégios de controle de roles:

  ```sql
  CREATE ROLE name [[WITH] option [...]];
  
  -- Daqui para baixo são comentários V
  -- where option can be:
  -- SUPERUSER    | NOSUPERUSER
  -- | CREATEDB   | NOCREATEDB
  -- | CREATEROLE | NOCREATEROLE
  -- | INHERIT    | NOINHERIT
  -- | LOGIN      | NOLOGIN
  -- | REPLICATION | NOREPLICATION
  -- | BYPASSRLS  | NOBYPASSRLS
  -- | CONNECTION LIMIT conlimit
  -- | [ECRYPTED] PASSWORD 'password' | PASSWORD NULL
  -- | VALID UNTIL 'timestamp'
  -- | IN ROLE role_name [...]
  -- | IN GROUP role_name [...]
  -- | ROLE role_name [...]
  -- | ADMIN role_name [...]
  -- | USER role_name [...]
  -- | SYSSID uid
  ```

  **Exemplo:**

  ```sql
  CREATE ROLE administradores
  	CREATEDB
  	CREATEROLE
  	INHERIT
  	NOLOGIN
  	REPLICATION
  	BYPASSRLS
  	CONECTION LIMIT -1;
  ```

  - #### `Associação entre roles`

    Quando uma role assume as permissões de outra role. Necessário a opção ***INHERIT***.

    No momento da criação da role:

    - `IN ROLE`: passa a pertencer a role informada.
    - `ROLE`: a role informada passa a pertencer a nova role.

    Após a criação da role:

    ```sql
    GRANT [role a ser concedida] TO [role a assumir permissões];
    ```

  - #### `Desassociar membros entre roles`

    ```sql
    REVOKE [role a ser revogada] FROM [ role que terá suas permissões revogadas];
    ```

  - #### `Alteração de roles`

    ```sql
    ALTER ROLE role_specification [WITH] option [...];
    -- Option possui as mesmas chaves o create
    ```

  - #### `Exluindo uma role`

    ```sql
    DROP ROLE role_specification;
    ```

- ### `Grant`

  `Definição`: são privilégios de acesso aos objetos do banco de dados.

  Privilégios:

  **--tabela**                                                      **--function**

  --coluna                                                      --language
  --sequence                                                --large object
  **--database**                                               **--schema**
  --domain                                                  --tablespace
  --foreign data wrapper                          --type
  --foreign server

  `DATABASE`:

  ```sql
  DATABASE GRANT {{CREATE|CONNECT|TEMPORARY|TEMP} [...] | ALL [PRIVILEGES]]} ON DATABASE database_name [...] TO role_specification [...] [WITH GRANT OPTION];
  ```

  `SCHEMA`:

  ```sql
  SCHEMA GRANT {{CREATE|USAGE}[...] | ALL [PRIVILEGES]} ON SCHEMA schema_name [...] TO role_specification [...] [WITH GRANT OPTION];
  ```

  `TABLE`:

  ```sql
  TABLE {{SELECT|INSERT|UPDATE|TRUNCATE|REFERENCES|TRIGGER} [...] | ALL [PRIVILEGES]} ON {[TABLE] table_name [...] | AL TABLES IN SCHEMA schema_name [...]} TO role_specification [...] [WITH GRANT OPTION];
  ```

  Para remover privilégios utiliza-se o `Revoke`:

  Por exemplo:

  ```SQL
  {DATABASE|SCHEMA|TABLE} REVOKE [GRANT OPTION FOR] {{TODAS AS OPÇÕES DAS RESPCTIVAS} [...] | ALL [PRIVILEGES] ON {DATABASE|SCHEMA|TABLE} {database|schema|table}_name[...] FROM {[GROUP] role_name | PUBLIC} [...] [CASCADE | RESTRICT];
  ```

  *Onde possui mais de uma opção, significa a escolha de somente uma e não possui chaves*.

  

## Objetos e comandos do banco de dados

- #### `Database`: é o banco de dados. Grupo de schemas e seus objetos, como tabelas, types, views, funções, entre outros. Seus schemas e objetos não podem ser compartilhados entre si. Cada database é separado um do outro compartilhando apenas usuários/roles e configurações do cluster PostgreSQL.

  - Criar database:

    ```sql
    CREATE DATABASE name [[WITH] 
        [OWNER [=] user_name]
    	[TEMPLATE [=] template]
    	[ENCODIN] [=] encodin]
    	[LC_COLLATE [=] lc_collate]
    	[LC_CTYPE [=] lc_ctype]
    	[TABELSPACE [=] tablespace_name]
    	[ALLOW_CONNECTIONS [=] allowconn]
    	[CONNECTION LIMIT [=] connlimit]
    	[IS_TEMPLATE [=] istemplate]];
    ```

  - Alterar database:

    ```sql
    ALTER DATABASE name RENAME TO new_name;
    ALTER DATABASE name OWNER TO {new_owner | CURRENT_USER | SESSION_USER};
    ALTER DATABASE name SET TABLESPACE new_tablespace;
    ```

  - Deletar database:

    ```sql
    DROP DATABASE [name];
    ```

    

- #### `Schemas`: é um grupo de objetos, como tabelas, types, views, funções, entre outros. É possível relacionar objetos entre diversos schemas. Por exemplo: schema public e schema curso podem ter tabelas com o mesmo nome (teste por exemplo) relacionando-se entre si.

  - Criar schema: 

    ```sql
    CREATE SCHEMA schema_name [AUTHORIZATION role_specification];
    ```

  - Alterar schema:

    ```sql
    ALTER SCHEMA name RENAME TO new_name;
    ALTER SCHEMA name OWNER TO {new_owner | CURRENT_USER | SESSION_USER};
    ```

  - Deletar schema:

    ```sql
    DROP SCHEMA [name];
    ```

  - Boas práticas:

    ```sql
    CREATE SCHEMA IF NOT EXISTS schema_name [AUTHORIZATION role_specification];
    DROP SCHEMA IF EXISTS [name];
    ```

    

- #### `Objetos`: são tabelas, views, funções, types, sequences, entre outros, pertencentes aos schemas.

- #### `Tabelas`: conjunto de dados dispostos em colunas e linhas referentes a um objetivo comum.

- #### `Colunas`: as colunas são consideradas como "campos de tabela", como atributos da tabela.

- #### `Linhas`: as linhas de uma tabela são chamadas também de tuplas, e é onde estão contidos os valores, os dados.

- #### `Primary Key / Chave Primária / PK`: no conceito de modelo de dados relacional e obedecendo as regras de normalização, uma PK é um conjunto de um ou mais campos que nunca se repetem em uma tabela e que seus valores garantem a integridade do dado único e a utilização do mesmo como referência para o relacionamento entre demais tabelas.

  - Não pode haver duas ocorrências de uma mesma entidade com o mesmo conteúdo na PK.
  - A chave primária não pode ser composta por atributo opcional, ou seja, atributo que aceite nulo.
  - Os atributos identificadores devem ser o conjunto mínimo que pode identificar cada instância de uma entidade.
  - Não devem ser usadas como chaves internas.
  - Não devem conter informação volátil.

- #### `Foreign Key / Chave Estrangeira / FK`: campo, ou conjunto de campos que são referência de chaves primárias de outras tabelas ou da mesma tabela. Sua principal função é garantir a integridade referencial entre tabelas.

- #### `Tipos`:

  **Numeric Types**                                       UUID Types

  Monetary Types                                      XML Types

  **Character Types**                                    JSON Types

  Binary Data Types                                  Arrays

  **Date/Time Types**                                   Composite Types

  **Boolean Types**                                       Range Types

  Enumerated Types                                 Domain Types

  Geometric Types                                    Object Identifier Types

  Network Address Types                       pg_Isn Types

  Bit String Types                                     Pseudo-Types

  Text Search Types

  - Numéricos:

    - smallint
    - integer
    - bigint
    - decimal
    - numeric
    - real
    - double precision
    - smallserial
    - serial
    - bigserial

  - Caracteres:

    - charcater varying / varchar
    - character  / char
    - text

  - Datas:

    - timestamp [without time zone]
    - timestamp [with time zone]
    - date
    - time [without time zone]
    - time [with time zone]
    - interval

  - Booleanos

    - boolean

  - #### `DML`: Data manipulation Language - linguagem de manipulação de dados - INSERT, UPDATE, DELETE, SELECT(consideram também como DQL, data query language).

    ```sql
    CREATE TABLE [IF NOT EXISTS] [nome da tabela] (
    	[nome do campo] [tipo] [regras] [opções],
    	[nome do campo] [tipo] [regras] [opções],
    	[nome do campo] [tipo] [regras] [opções]
    );
    ```

    ```sql
    ALTER TABLE [nome da tabela] [opções];
    ```

    ```sql
    DROP TABLE [nome da tabela];
    ```

    ```sql
    INSERT INTO [nome da tabela] ([campos da tabela,]) VALUES ([valores de acordo com a ordem dos campos da tabela]);
    INSERT INTO [nome da tabela] ([campos da tabela,]) SELECT ([valores de acordo com a ordem dos campos da tabela]);
    ```

    ```sql
    UPDATE [nome da tabela] SET 
    	[campo1] = [novo valor],
    	[campo2] = [novo valor],
    	...
    	[WHERE + condições];
    ```

    *O update deve ser sempre utilizado com **Condição***.

    ```sql
    DELETE FROM [nome da tabela] [WHERE + condiçoes];
    ```

    *O delete deve ser sempre utilizado com **Condição***.

    ```sql
    SELECT [campos da tabela] FROM [nome da tabela] [WHERE + condições];
    ```

    *Evite sempre que puder o `SELECT *`*

  - #### `DDL`: Data Definition Language - linguagem de definição de dados - CREATE, ALTER, DROP.

    ```sql
    CREATE [objeto] [nome do objeto] [opções];
    ALTER [objeto] [nome do objeto] [opções];
    DROP [objeto] [nome do objeto] [opções];
    ```

    Boas práticas:

    ```sql
    CREATE [objeto] IF NOT EXISTS [nome do objeto] [opções];
    ALTER [objeto] [nome do objeto] OWNER TO [role];
    DROP [objeto] IF EXISTS [nome do objeto];
    ```


## DML e o Truncate

- #### `Idempotência`: 

  `Definição`: propriedade que algumas ações/operações possuem possibilitando-as de serem executadas diversas vezes sem alterar o resultado após a aplicação inicial.

- ### Melhores práticas em DDL

  Importante as tabelas possuírem campos que realmente  serão utilizados e que sirvam de atributo direto a um objetivo em comum.

  - Criar/Acrescentar colunas que são "atributos básicos" do objetivo; Exemplo: tabela CLIENTE: coluna TELEFONE / coluna AGENCIA_BANCARIA.
  - Cuidado com regras (constraints).
  - Cuidado com o excesso de FKs.
  - Cuidado com o tamanho indevido de colunas. Exemplo: coluna CEP VARCHAR (255).

- ### **DML - CRUD**

  - #### `SELECT`

  ```sql
  SELECT (campos) FROM tablea [condições];
  Condições: 
  	WHERE campo IS TRUE;
  	WHERE campo LIKE "condição do campo";
  ```
   - #### Condições:

     - `WHERE (coluna/condição)`:
       - =
       - .> /  >=
       - < / <=
       - <> / !=
       - LIKE
       - ILIKE
       - IN
     
      Primeiro condição sempre WHERE. Demais condições, AND ou OR.
     
  - SELECT - Idempotência

    ```sql
    SELECT (campos)
    FROM tabela
    WHERE EXISTIS (
    	SELECT (campo)
        FROM tabela
        WHERE campo = valor
        [AND/OR campoN = valorN]
    );
    ```

    Não é uma boa prática. A melhor é utilizar o `LEFT JOIN`.

    WARNING :warning: : SELECT * (Evitar)

  - #### `INSERT`

    ```sql
    INSERT (campos da tabela) VALUES (values);
    INSERT (campos da tabela) SELECT (values);
    ```

  - INSERT - Idempotência

    ```sql
    INSERT INTO tabela (campos da tabela) VALUES (values);
    
    INSERT INTO tabela (campos da tabela)
    	SELECT {dados a serem inseridos: dado1,dado2,dado3}
    	WHERE NOT EXISTS (SELECT (campos da tabela) WHERE campo1 = dado1 AND campo2 = dado2 AND campo3 = dado3);
    ```

    - ON CONFLICT

    ```sql
    INSERT INTO tabela (campos da tabela) VALUES (values) ON CONFLICT (campos tabela) DO NOTHING;
    ```

  - #### `UPDATE`

    ```sql
    UPDATE (tabela) SET campo1= valor WHERE (condição);
    ```

  - #### `DELETE`

    ```sql
    DELETE FROM (tabela) SET campo1 = valor WHERE (condição);
    ```

- ### Truncate

  `Definição`: esvazia a tabela.

  ```sql
  TRUNCATE [TABLE] [ONLY] name [*] [...]
  	[RESTART IDENTITY | CONTINUE IDENTITY] 
  	[CASCADE | RESTRICT]
  ```

## Funções Agregadas

Como são muitas funções o site oficial para consulta é o seguinte : [https://www.postgresql.org/docs/13/functions-aggregate.html]()

Alguns exemplos de funções agregadas:

- AVG

  ```sql
  SELECT AVG(valor) FROM cliente_transacoes;
  ```

- COUNT

  ```sql
  SELECT COUNT(numero)
  	FROM cliente;
  ```

  Com condições:

  ```sql
  SELECT COUNT(numero), email
  	FROM cliente
  	WHERE email ILIKE '%gmail.com'
  	GROUP BY email;
  ```

- MAX

  ```sql
  SELECT MAX(numero)
  	FROM cliente;
  ```

  Com o `GROUP BY`:

  ```sql
  SELECT MAX(valor) tipo_transacao_id
  	FROM cliente_transacoes
  	GROUP BY tipo_transacao_id;
  ```

- MIN

  ```sql
  SELECT MIN(numero)
  	FROM cliente;
  ```

  Com o `GROUP BY`:

  ```sql
  SELECT MIN(valor) tipo_transacao_id
  	FROM cliente_transacoes
  	GROUP BY tipo_transacao_id;
  ```

- COUNT

  ```sql
  SELECT COUNT (id), tipo_transacao_id
  	FROM cliente_transacoes
  	GROUP BY tipo_transacao_id;
  ```

  Como o `HAVING`:

  ```sql
  SELECT COUNT (id), tipo_transacao_id
  	FROM cliente_transacoes
  	GROUP BY tipo_transacao_id
  	HAVING COUNT (id) > 150;
  ```

- SUM

  ```sql
  SELECT SUM(valor)
  	FROM cliente_transacoes;
  ```

  Com o `ORDER BY`:

  - Ascendente:

    ```sql
    SELECT SUM(valor), tipo_transacao_id
    	FROM cliente_transacoes
    	GROUP BY tipo_transacao_id
    	ORDER BY tipo_transacao_id ASC;
    ```

  - Descendente:

    ```sql
    SELECT SUM(valor), tipo_transacao_id
    	FROM cliente_transacoes
    	GROUP BY tipo_transacao_id
    	ORDER BY tipo_transacao_id DESC;
    ```

## JOINS

- ### JOIN (INNER JOIN)

  ```sql
  SELECT tabela1.campos, tabela2.campos 
  FROM tabela1 
  JOIN tabela2 ON tabela2.campos = tabela1.campos;
  ```

  

- ### LEFT JOIN ( LEFT OUTER JOIN)

  ```sql
  SELECT tabela1.campos, tabela2.campos 
  FROM tabela1 
  LEFT JOIN tabela2 
  ON tabela2.campos = tabela1.campos;
  ```

  

- ### RIGHT JOIN (RIGHT OUTER JOIN)

  ```sql
  SELECT tabela1.campos, tabela2.campos 
  FROM tabela1 
  RIGHT JOIN tabela2 
  ON tabela2.campos = tabela1.campos;
  ```

  

- ### FULL JOIN (FULL OUTER JOIN)

  ```sql
  SELECT tabela1.campos, tabela2.campos 
  FROM tabela1 
  FULL JOIN tabela2 
  ON tabela2.campos = tabela1.campos;
  ```

  

- ### CROSS JOIN (CROSS OUTER JOIN)

  Todos os dados de uma tabela serão cruzados com todos os dados da tabela referenciada no CROSS JOIN criando uma matriz. 

  ```sql
  SELECT tabela1.campos, tabela2.campos 
  FROM tabela1 
  CROSS JOIN tabela2;
  ```

  

## Commom Table Expression - CTE

`Definição`: forma auxiliar de organizar "statements", ou seja, blocos de códigos, para consultas muitos grandes, gerando tabelas temporárias e criando relacionamento entre elas.

Dentro dos statements podem ter SELECTs, INSERTs, UPDATEs ou DELETEs.

- `WITH STATEMENTS`:

  ```sql
  WITH [nomeTempTable1] AS (
  	SELECT (campos)
      FROM tabela_a
      [WHERE]
  ), [nomeTempTable2] AS (
  	SELECT (campos)
      FROM table_b
      [WHERE]
  )
  SELECT [nomeTempTable1].(campos),[nomeTempTable2].(campos) 
  FROM [nomeTempTable1]
  JOIN [nomeTempTable2];
  ```

  

## VIEWS

`Definição`: são visões, "camadas" para as tabelas, "alias" para uma ou mais queries. Aceitam comando de SELECT, INSERT, UPDATE e DELETE.

```sql
CREATE [OR REPLACE] [TEMP | TEMPORARY] [RECURSIVE] VIEW name [(column_name[...])]
	[WITH (view_option_name [= view_option_value] [...])]
	AS query
	[WITH [CASCADED | LOCAL] CHECK OPTION]
```

- #### IDEMPOTÊNCIA

  ```sql
  CREATE OR REPLACE VIEW vw_bancos AS (
  	SELECT numero,nome,ativo
      FROM banco
  );
  
  SELECT numero, nome, ativo
  	FROM vw_bancos;
  	
  CREATE OR REPLACE VIEW vw_bancos (banco_numero, banco_nome, banco_ativo) AS (
  	SELECT numero, nome, ativo
      FROM banco
  );
  
  SELECT banco_numero, bano_nome, banco_ativo
  	FROM vw_bancos;
  ```

- #### INSERT, UPDATE e DELETE

  ```sql
  CREATE OR REPLACE VIEW vw_bancos AS(
  	SELECT numero,nome,ativo
      FROM banco
  );
  
  SELECT numero,nome,ativo
  FROM vw_bancos;
  ```

  - Funcionam apenas para VIEWs com apenas 1 tabela.

  ```sql
  INSERT INTO vw_bancos (numero,nome,ativo) VALUES (100, 'Banco CEM', TRUE);
  
  UPDATE vw_bancos SET nome = 'Banco 100' WHERE numero = 100;
  
  DELETE FROM vw_bancos WHERE numero = 100;
  ```

- #### TEMPORARY

  ```sql
  CREATE OR REPLACE TEMPORARY VIEW vw_bancos AS (
  	SELECT numero, nome, ativo
  	FROM banco
  );
  
  SELECT numero, nome, ativo
  FROM vw_bancos;
  ```

  VIEW presente apenas na sessão do usuário. Se você se desconectar e conectar novamente, a VIEW não estará disponível.

- #### RECURSIVE

  ```sql
  CREATE OR REPLACE RECURSIVE VIEW (nome_da_view)(campos_da_view) AS (
  	SELECT base
      UNION ALL
      SELECT campos
      FROM tabela_base
      JOIN (nome_da_view)
  );
  ```

  - Obrigatório a existência dos campos da VIEW.
  - UNION ALL - não unifica resultados iguais

  ```SQL
  CREATE TABLE IF NOT EXISTS funcionarios(
  	id SERIAL NOT NULL,
      nome VARCHAR(50),
      gerente INTEGER,
      PRIMARY KEY (id),
      FOREIGN KEY (gerente) REFERENCES funcionarios (id)
  );
  
  CREATE OR REPLACE RECURSIVE VIEW vw_funcionarios(id,gerente,funcionario) AS (
  	SELECT id,gerente,nome
      FROM funcionarios
      WHERE gerente IS NULL
      UNION ALL
      SELECT funcionarios.id,funcionarios.gerente, funcionarios.nome
      FROM funcionarios
      JOIN vw_funcionarios ON vw_funcionarios.id = funcionarios.gerente
  );
  
  SELECT id,gerente,funcionario
  	FROM vw_funcionarios
  	
  -- or
  
  CREATE OR REPLACE RECURSIVE VIEW vw_funcionarios(id,gerente,funcionario) AS (
  	SELECT id,CAST(AS VARCHAR) AS gerente,nome
      FROM funcionarios
      WHERE gerente IS NULL
      UNION ALL
      SELECT funcionarios.id,funcionarios.gerente, funcionarios.nome
      FROM funcionarios
      JOIN vw_funcionarios ON vw_funcionarios.id = funcionarios.gerente
      JOIN funcionarios gerentes ON gerentes.id = vw_funcionarios.id
  );
  
  SELECT id,gerente,funcionario
  	FROM vw_funcionarios
  ```

  

- #### WITH OPTIONS

  ```sql
  CREATE OR REPLACE VIEW vw_bancos AS (
  	SELECT numero,nome,ativo
      FROM banco
  );
  
  INSERT INTO vw_bancos (numero, nome, ativo) VALUES (100, 'Banco CEM', FALSE);
  
  -- OK
  
  CREATE OR REPLACE VIEW vw_bancos AS (
  	SELECT numero,nome,ativo
      FROM banco
      WHERE ativo IS TRUE
  ) WHIT LOCAL CHECK OPTION;
  
  INSERT INTO vw_bancos (numero, nome, ativo) VALUES (100, 'Banco CEM', FALSE);
  
  -- ERRO
  ```

  ```sql
  CREATE OR REPLACE VIEW vw_bancos_ativos AS (
  	SELECT numero,nome,ativo
      FROM banco
      WHERE ativo IS TRUE
  ) WHIT LOCAL CHECK OPTION;
  
  CREATE OR REPLACE VIEW vw_bancos_maiores_que_100 AS (
  	SELECT numero,nome,ativo
      FROM banco
      WHERE numero > 100
  ) WHIT LOCAL CHECK OPTION;
  
  INSERT INTO vw_bancos_maiores_que_100 (numero, nome, ativo) VALUES (99, 'Banco CEM', FALSE);
  -- ERRO
  
  INSERT INTO vw_bancos (numero, nome, ativo) VALUES (200, 'Banco CEM', FALSE);
  -- ERRO
  ```

  ```sql
  CREATE OR REPLACE VIEW vw_bancos_ativos AS (
  	SELECT numero,nome,ativo
      FROM banco
      WHERE ativo IS TRUE
  );
  
  CREATE OR REPLACE VIEW vw_bancos_maiores_que_100 AS (
  	SELECT numero,nome,ativo
      FROM banco
      WHERE numero > 100
  ) WHIT CASCADE CHECK OPTION;
  
  INSERT INTO vw_bancos_maiores_que_100 (numero, nome, ativo) VALUES (99, 'Banco CEM', FALSE);
  -- ERRO
  
  INSERT INTO vw_bancos (numero, nome, ativo) VALUES (200, 'Banco CEM', FALSE);
  -- OK
  ```

  


## Transações

`Definição`: conceito fundamental de todos os sistemas de banco de dados. Conceito de múltiplas etapas/códigos reunidos em apenas 1 transação, onde o resultado precisa ser **tudo ou nada**.

Exemplo:

```sql
BEGIN; -- caso de erro é executado um ROLLBACK
	
		UPDATE conta SET valor = valor - 100
		WHERE nome = 'Alice';
		
		UPDATE conta SET valor = valor + 100
		WHERE nome = 'Bob';
		
ROLLBACK; -- Desfraz as transações
```

```sql
BEGIN; -- caso de erro é executado um ROLLBACK
	
		UPDATE conta SET valor = valor - 100
		WHERE nome = 'Alice';
		
SAVEPOINT my_savepoint; -- Declara o save point

		UPDATE conta SET valor = valor + 100
		WHERE nome = 'Bob';
		-- ops ... não era para o Bob, é para a Wally

ROLLBACK TO my_savepoint; -- cancela o save point

		UPDATE conta SET valor = valor + 100
		WHERE nome = 'Wally';
		
COMMIT; -- Mostra a alteração a outros devs.
```



## Funções

`Definição`: conjunto de códigos que são executados **dentro de uma transação** com a finalidade de facilitar a programação e obter o reaproveitamento/reutilização de códigos.

Existem 4 tipos de funções:

- query language functions (funções escritas em SQL).
- procedural language functions (funções escritas em, por exemplo, PL/pgSQL ou PL/py).
- Internal functions.
- C-language functions.

Porém o foco aqui é falar sobre **USER DEFINED FUNCTIONS**. Funções que podem ser criados pelo usuário.



### **PL/pgSQL**:

```sql
CREATE [OR REPLACE] FUNCTION
	name ([argmode] [argname] argtype[{DEFAULT | =} default_expr][...])
	[RETURNS TABLE (column_name column_type [...])]
	{ LANGUAGE lang_name
		| 	TRANSFORM {FOR TYPE type_name} [...]
		| WINDOW
		| IMMUTABLE | STABLE | VOLATILE | [NOT] LEAKPROOF
		|CALLED ON NULL INPUT | RETURNS NULL ON NULL INPUT | STRICT
		| [EXTERNAL] SECURITY INVOKER | [EXTERNAL] SECURITY DEFINER
		| PARALLEL {UNSAFE | RESTRICTED | SAFE}
		| COST exection_cost
		| ROWS result_rows
		| SET configuration_parameter {TO value | = value| FROM CURRENT}
		| AS 'definition'
		| AS 'obj_file', 'link_symbol'
	} ...
```

- ### IDEMPOTÊNCIA

  CREATE **OR REPLACE** FUNCTION [nome da função]

  - Mesmo nome
  - Mesmo tipo de retorno
  - Mesmo número de parâmetros/argumentos

- ### Returns

  - #### Tipo de retorno (data type)

    - INTEGER
    - CHAR/ VARCHAR
    - BOOLEAN
    - ROW
    - TABLE
    - JSON

- ### Language

  - **SQL**
  - **PLPGSQL**
  - PLJAVA
  - PLPY

- ### Security

  - INVOKER
  - DEFINER

- ### Comportamento

  - **IMMUTABLE**: não pode alterar o banco de dados. Funções que garantem o mesmo resultado para os mesmos argumentos/parâmetros da função. Evitar a utilização de selects, pois tabelas podem sofrer alterações.
  - **STABLE**: não pode alterar banco de dados. Funções que garantem o mesmo resultado para os mesmo argumentos/parâmetros da função. Trabalha melhor com tipos de current_timestamp e outros tipos de vaiáveis. Podem conter selects.
  - **VOLATILLE**: comportamento padrão. Aceita todos os cenários.

- ### Segurança e boas práticas

  - **CALLED ON NULL INPUT**: padrão. Se qualquer um dos parâmetros/argumentos for NULL, a função será executada.
  - **RETURNS NULL ON NULL INPUT**: se qualquer um dos parâmetros/argumentos for NULL, a função retornará NULL.
  - **SECURITY INVOKER**: padrão. A função é executada com as permissões de quem executa.
  - **SECURITY DEFINER**: a função é executada com as permissões de quem criou a função.

- ### Recursos

  - **COST**: custo/row em unidades de CPU.
  - **ROWS**: número estimado de linhas que será analisada pelo planner.

- ### SQL FUNCTIONS

  ```sql
  CREATE OR REPLACE fc_bancos_add(p_numero INTEGER, p_nome VARCHAR, p_ativo BOOLEAN)
  RETURNS TABLE (numero INTEGER, nome VARCHAR)
  RETURNS NULL ON NULL INPUT
  LANGUAGE SQL
  AS $$
  		INSERT INTO banco(numero,nome,ativo)
  		VALUES (p_numero,p_nome,p_ativo);
  		
  		SELECT numero, nome
  		FROM banco
  		WHERE numer = p_numero;
  		
  $$;
  ```

- ### PLPGSQL

  ```sql
  CREATE OR REPLACE FUNCTION banco_add (p_numero INTEGER, p_nome VARCHAR, p_ativo BOOLEAN)
  RETURNS BOOLEAN
  LANGUAGE PLPGSQL
  AS $$
  DECLARE variavel_id INTEGER;
  BEGIN
  		SELECT INTO variavel_id numero FROM banco WHERE nome = p_nome;
  		
  		IF variavel_id IS NULL THEN
  				INSERT INTO banco(numero, nome, ativo) VALUES (p_numero,p_nome,p_ativo);
  		ELSE
  				RETURN FALSE;
  				
  		END IF;
  		
  		SELECT INTO variavel_id nuemro FROM banco WHERE nome = p_nome;
  		
  		IF variavel_id IS NULL THEN
  				RETURN FALSE;
  		ELSE
  				RETURN TRUE;
  				
  		END IF;
  END; $$;
  
  SELECT banco_add(13,'Banco azarado', true);
  ```

  
