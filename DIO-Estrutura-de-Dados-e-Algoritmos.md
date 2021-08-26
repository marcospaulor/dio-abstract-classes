# Estrutura de Dados e Algoritmos

## Oque é?

Estrutura de Dados é uma estrutura organizada de dados na memória de uma computador ou em qualquer dispositivo de armazenamento, de forma que os dados possam ser utilizados de forma correta.

Essas estruturas encontram muitas aplicações no desenvolvimento de sistemas, sendo que algumas são altamente especializadas e utilizadas em tarefas específicas.

Usando as estruturas adequadas através de algoritmos, podemos trabalhar com uma grande quantidade de dados, como aplicação em bancos de dados ou serviços de busca.

Um **algoritmo** é um conjunto de instruções estruturadas e ordenadas, seu objetivo é realizar uma tarefa ou operação específica.

Os algoritmos são utilizado para manipular dados nas estruturas de várias formas, como por exemplo: inserir, excluir, procurar e ordenar dados.

E uma estrutura de dados devemos saber como realixar um determinado conjunto de operações básicas, como por exemplo:

- Inserir Dados.
- Excluir Dados.
- Localizar um elemento.
- Percorrer todos os itens constituintes da estrutura para visualização.
- Classificar, que se resume em colocar os itens de dados em uma determinada ordem(numérica, alfabética, etc.)

## Principais Estruturas de Dados

- Vetores e Matrizes
- Registro
- Lista
- Pilha
- Fila
- Árvore
- Tabela Hash
- Grafos

### Vetores e Matrizes

São estruturas de dados simples que podem auxiliar quando há muitas variáveis do mesmo tipo em um algoritmo.

**Vetor** ou **Array uni-dimensional** é uma variável que armazena várias variáveis do mesmo tipo.

O vetor é uma estrutura de dados indexada, que pode armazenar uma determinada quantidade de valores do mesmo tipo.

**Matriz** ou **Array multi-dimensional** é um vetor de vetores.

Uma matriz é um vetor que possui duas ou mais dimensões.

### Registro

É uma estrutura que fornece um formato especializado para armazenar informações em memória.

Enquanto Arrays no permitem armazenar vários dados de um único tipo de dados, o recurso de **Registro** nos permite armazenar mais de um topo de dado.

Um registro é composto pode campos que especificam cada uma das informações que o compõem.

Toda estrutura de registro tem um nome (ex.: livro), e sesu campos podem ser acessados por meio do uso do operador ponto (.). Por exemplo, para acessar o preço de um livro, poderíamos utilizar a seguinte declaração: *livro.preco*

### Listas

Armazena dados que um determinado tipo em uma ordem específica. A diferença entre listas e arrays é a de que as ***listas possuem tamanho ajustável***, enquanto arrays possuem tamanho fixo.

Existem dois tipos de lista:

- Listas Ligadas
- Listas Duplamente Ligadas

#### Lista Ligada

Na estrutura do tipo lista existem nós onde cada um dos nós conhece o valor que está sendo armazenado em seus interior além de conhecer o elemento posterior a ele: por isso ela é chamada de "lista ligada", pois os nós são amarrados com essa indicação de qual é o próximo nó.

#### Lista Duplamente Ligada

Constituem uma variação das listas ligadas. A grande diferença das listas duplamente ligadas para as listas ligadas é que elas são bidirecionais. Vimos que, naturalmente, não conseguimos "andar para trás" em listas ligadas, por os nós de uma lista ligada sabem somente quem é o próximo elemento. Nas listas duplamente ligadas, os nós sabem quem é o próximo elemento e também quem é o elemento anterior, o que permite a navegação reversa.

### Pilhas

Um pilha é uma estrutura de dados que serve como uma coleção de elementos, e permite o acesso a somente um item de dados armazenado.

O acesso aos itens de uma pilha é restrito - somente um item pode ser lido ou removido por vez.

Tipos de pilhas:

- LIFO ou UEPS
- FIFO ou PEPS

#### LIFO

A estrutura do tipo pilha LIFO (Last in First Out) ou UEPS (Último que Entra Primeiro que Sai), apresenta o seguinte critério: o primeiro elemento que a ser retirado é o último que tiver sido inserido.

#### FIFO

A estrutura do tipo pilha FIFO (First In First Out) ou PEPS (Primeiro que Entra Primeiro que Sai), apresenta o seguinte critério: o primeiro elemento a ser retirado é o primeiro que tiver sido inserido.

### Filas

A estrutura do tipo Fila admite remoção de elementos e inserção de novos sujeita à seguinte regra de operação: O elemento removido é o que está na estrutura há mais tempo ou seja, o primeiro objeto inserido na fila é também o primeiro a ser removido seguindo o conceito FIFO.

### Árvore

É uma estrutura de dados que organiza seus elementos de forma hierárquica, onde existe um elemento que fica no topo da árvore, chamado de raiz e existem os elementos subordinados a ele,que são chamados de nós ou folhas.

### Tabela Hash

Tabela de dispersão ou espalhamento da ideia de array, porém utiliza uma função denominada Hashing para espalhar os elementos, fazendo com que os mesmo fiquem de forma não ordenada dentro do "array" que define a tabela.

#### Porque espalhar?

A tabela hash permite a associação de "valores" a "chaves"

**Valores:** é a posição ou índice onde o elemento se encotra.

**Chave** parte da informação que compõe o elemento a ser manipulado.

Espalhar facilita a busca na estrutura de dados, pois a partir de uma chave podemos acessar de forma rápida uma posição do "array".

### Grafos

São estruturas que permitem programar a relação entre objetos. Os objetos são **vértices** ou "nós" do grafo. Os relacionamentos são as **arestas**.