# Implementações Collections e Streams com Java

## Collections - List

- Implementações
  - **java.util.ArrayList**
  
  - **java.util.Vector**
  
- Garante Ordem de inserção

- Permite adição, atualização, leitura e remoção sem regras adicionais

- Permite ordenação através de comparativos

Exemplo com List:

```java
import java.util.ArrayList;
import java.util.List;

public class Exemplo{
    public static void main(String[] args){
        List<String> nomes = new ArrayList<>();
    }
    
    //.add() adiciona o valor na lista
    nomes.add("Marcos"); 
    nomes.add("Anna");
    nomes.add("john");
    nomes.add("Maria");
    
    //.set() adiciona o valor na posição indicada
    nomes.set(2,"Paulo");
    
    //Collecitons sort, embaralha os nomes
    Collections.sort(nomes);
    
    //.remove(), remove tanto indicando o valor quanto a posição
    nomes.remove(2);
    nomes.remove("Maria");
    
    //.get(), retorna a uma variável o valor da lista dado o índice
    var nome = nomes.get(2);
    
    //.size(), retorna um número inteiro como o tamanho da lista
    int tamanho = nomes.size();
    
    //.contains(), retorna um booleano que indica se o valor inidicado existe
    boolean temValor = nomes.contains("Marcos"); //true
    
    //.isEmpty(), verifica se a lista está vazia
    boolean listaEstaVazia = nomes.isEmpty();
    
    //.clear(), limpa a lista
    nomes.clear();
    
    //.indexOf(), retorna o índice em que o valor foi especificado
    int posicao = nomes.indexOf("Marcos"); // 0
    
    //foreach
    for(String nomeDoItem: nomes){
        System.out.println(nomeDoItem);
    }
    
    //com o iterator
    Iterator<String> iterator = nomes.iterator();
    
    while(iterator.hasNext()){
        System.out.println(iterator.next());
    }
}
```

Exemplo com Vector:

```java
import java.util.List;
import java.util.Vector;

public class Exemplo{
    public static void main(String[] args){
        List<String> esportes = new Vector<>();
        
        //Adiciono quatro esportes
        esportes.add("Soccer");
        esportes.add("Football");
        esportes.add("Handball");
        esportes.add("Basketball");
        
        //Altera valor do vetor
        esportes.set(2, "Biloca");
        
        //Remove o valor(por índice ou valor) do vetor
        esportes.remove(2);
        esportes.remove("Football");
        
        //Retorna valor do vetor
        var itenVetor = esportes.get(0);
        
        //Navega nos esportes
        for(String esporte: esportes){
            System.out.println(esporte);
        }
    }
}
```

## Collections - Queue

- Implementações:
  - **java.util.LinkedList**
- Garante ordem de inserção
- Permite adição, leitura e remoção considerando a regra básica de uma fila: Primeiro que entra, primeiro que sai.
- Não permite mudança de ordenação.

```java
import java.util.LinkedList;

public class Exemplo{
    public static void main(String[] args){
        Queue<String> filaBanco = new LinkedList<>();
        
        filaBanco.add("Patricia");
        filaBanco.add("Roberto");
        filaBanco.add("Flávio");
        filaBanco.add("Pamela");
        filaBanco.add("Anderson");
        
        //Como é uma fila a remoção desses elementos vão partir do primeiro elemento
        
        // .poll(), retorna o primeiro elemento e é retirado da fila
        String clienteASerAtendido = filaBanco.poll();
        
        // .peek(), retorna o primeiro elemento mas não remove da fila
        String primeiroCliente = filaBanco.peek();
        
        // .element(), retorna o elemento e não remove da fila - Caso elemento não exista ou fila vazia, retorna um erro
        String primeiroClienteOuErro = filaBanco.element();
        
        //Navegando nos elementos
        for(String client: filaBanco){
            System.out.println(client);
        }
        
        //Iterator
        Iterator<String> iteratorFilaBanco = filaBanco.iterator();
        
        while(iteratorFilaBanco.hasNext()){
            System.out.println(iteratorFilaBanco.next());
        }
        
        // .size()
        var tamanho = filaBanco.size();
        
        // .isEmpty()
        var vazio = filaBanco.isEmpty();
        
        // .clear()
        filaBanco.clear();
    }
}
```

## Collections - Set

- Implementações:
  - **java.util.HashSet**
  - **java.util.TreeSet**
  - **java.util.LinkedHashSet**
- Por padrão, não garante ordem.
- Não permite itens repetidos.
- Permite adição e remoção normalmente. Não possui busca por item e atualização. Para leitura, apenas navegação.
- Não permite mudança de ordenação.

|                   | Quando Utilizar                                              | Ordenação                                   | Perfomance                                                   |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------- | ------------------------------------------------------------ |
| **HashSet**       | Quando  não é necessário manter uma ordenação                | Não é ordenado, e permite valores repetidos | Por não ter repetição de valores e não ser ordenado, é implementação mais performática |
| **LinkedHashSet** | Quando é necessário manter a ordem de inserção dos elementos | Mantém a ordem de inserção dos elementos    | É a implementação mais lenta por ser necessária manter ordem |
| **TreeSet**       | Quando é necessário alterar a ordem através do uso de comparators | Mantém a ordem e pode ser reordenado        | É performático para leitura. Para a modificação tem a necessidade de reordenar, sendo mais lento que LinkedHashSet |

### *Implementação HashSet*

```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

public class Exemplo{
    public static void main(String[] args){
        
        Set<Double> notasAlunos = new HashSet<>();
        
        notasAlunos.add(10.0);
        notasAlunos.add(9.5);
        notasAlunos.add(5.3);
        notasAlunos.add(7.3);
        
        notasAlunos.remove(5.3);
        
        var tamanho = notasAlunos.size();
        
        Iterator<Double> iterator = notasAlunos.iterator();
        
        while(iterator.hashNext()){
            System.out.println(iterator.next());
        }
        
        notasAlunos.clear();
        
        var vazio = notasAlunos.isEmpty();
    }
}
```

### *Implementação LinkedHashSet*

```java
import java.util.Iterator;
import java.util.LinkedHashSet;

public class Exemplo{
    public static void main(String[] args){
        
        LinkedHashSet<Integer> sequenciaNumerica = new LinkedHashSet<>();
        
        sequenciaNumerica.add(6);
        sequenciaNumerica.add(4);
        sequenciaNumerica.add(10);
        sequenciaNumerica.add(1);
        
        sequenciaNumerica.remove(10);
        
        var tamanho = sequenciaNumerica.size();
        
        Iterator<Integer> iterator = sequenciaNumerica.iterator();
        
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
        
        sequenciaNumerica.clear();
        
        var vazio = sequenciaNumerica.isEmpty();
    }
}
```

### Implementação TreeSet

```java
import java.util.Iterator;
import java.util.TreeSet;

public class Exemplo{
    public static void main(String[] args){
        
        TreeSet<String> treeCapitais = new TreeSet<>();
        
        treeCapitais.add("Goiânia");
        treeCapitais.add("São Paulo");
        treeCapitais.add("Salvador");
        treeCapitais.add("Palmas");
        
        var primeira = treeCapitais.first();
        
        var ultima = treeCapitais.last();
        
        var abaixo = treeCapitais.lower("Salvador");
        
        var acima = treeCapitais.higher("Salvador");
        
        var retornaPimeiraRemove = treeCapitais.pollFirts();
        
        var retornaUltimaRemove = treeCapitais.pollLast();
        
        Iterator<String> iterator = treeCapitais.iterator();
        
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
}
```

## Collections - Map

- Implementações:
  - **java.util.HashMap**
  - **java.util.TreeMap**
  - **java.util.HashTable**
- Entrada de chave e valor.
- Permite valores repetidos, mas não permite repetição de chave.
- Permite adição, busca por chave ou valor, atualização, remoção e navegação.
- Pode ser ordenado.

### HashMap

```java
import java.util.HashMap;
import java.util.Map;

public class Exemplo{
    public static void main(String[] args){
		Map<String, Integer> campeoesMudialFifa = new HashMap<>();
        //Neste modo a é passado como parâmetro uma lista
		Map<String, List<Integer>> campeoesMudialFifa = new HashMap<>();
        
        
        //Insere os valores
        campeoesMundialFifa.put("Brasil", 5);
        campeoesMundialFifa.put("Alemanha", 4);
        campeoesMundialFifa.put("Argentina", 2);
        campeoesMundialFifa.put("Uruguai", 2);
        campeoesMundialFifa.put("Itália", 4);
        
        //Executar o put novamente atualiza o valor
        campeoesMundialFifa.put("Brasil",6);
        
        //Retorno de valores
        campeoesMundialFifa.get("Argentina");
        
        //Retorna caso exista
        var existeSeleção = campeosMundialFifa.containsKey("França");
        
        //Retorma caso exista Valor
        var existeQuantidade = campeosMundialFifa.containsValue(6);
        
        //Remove
        campeoesMundialFifa.remove("Françã");
        
        //Tamanho
        var tamanho = campeoesMundialFifa.size();
        
        //Navega nos registros do map
        for(Map.Entry<String, Integer> entry: campeoesMundialFifa.entrySet()){
            System.out.println(entry.getKey() + entry.getValue());
        }
        for(String key: campeoesMundialFifa.keySet()){
            System.out.println(key + campeoesMundialFifa.get(key));
        }
        
        //Verifica se contém a chave
        var contemChave = campeoesMundialFifa.containsKey("Marrocos");
        
        //Verifica se contém o valor
        var contemValor = campeoesMundialFifa.containsValue(5);
        
        //Limpa o mapa
        campeoesMundialFifa.clear();
    }
}
```

### TreeMap

```java
import java.util.Iterator;
import java.util.Map;
import java.util.TreeMap;

public class Exemplo{
    public static void main(String[] args){
		TreeMap<String, String> treeCapitais = new TreeMap<>();
        
        
        //Insere os valores
        campeoesMundialFifa.put("BR", "Brasília");
        campeoesMundialFifa.put("GE", "Berlin");
        campeoesMundialFifa.put("AR", "Buenos Aires");
        campeoesMundialFifa.put("UR", "Montevideo");
        campeoesMundialFifa.put("IT", "Roma");
        
        //Topo da árvore
        var primeiraCapital = treeCapitais.firstKey();
        
        //Final da árvore
        var ultimaCapital = treeCapitais.lastKey();
        
        var abaixo = treeCapitais.lowerKey("");
        
        var acima = treeCapitais.higherKey();
        
        var primeiroNoTopo = treeCapitais.firstEntry().getKey() + " " + treeCapitais.firstEntry().getValue();
        
        var ultimaNoTopo = treeCapitais.lastEntry().getKey() + " " + treeCapitais.lastEntry().getValue();
        
        var abaixoDoValor = treeCapitais.lowerEntry("AR").getKey() + " " + treeCapitais.lowerEntry("AR").getValue();
        
        var acimaDoValor = treeCapitais.higherEntry("AR").getKey() + " " + treeCapitais.higherEntry("AR").getValue();
        
        //Neste caso eles serão REMOVIDOS da árvore
        Map.Entry<String, String> firstEntry = treeCapitais.pollFirstEntry();
        Map.Entry<String, String> lastEntry = treeCapitais.pollLastEntry();
        
        //Iterators
        Iterator<String> iterator = treeCapitais.keySet().iterator();
        
        while(iterator.hasNext()){
            String key = iterator.next();
            System.out.println(key + treeCapitais.get(key));
        }
        
        for(String capital : threeCapitais.keySet()){
            System.out.println(capital + treeCapitais.get(capital));
        }
        
        for(Map.Entry<String, String> capital : treeCapitais.entrySet()){
            System.out.println(capital.getKey() + capital.getValue());
        }
    }
}
```

### HashTable

Utilizado em ambiente com ocorrência de Thread. Possui os mesmo métodos do HashMap.

## Collections - Comparators

- Interfaces:
  - **java.util.Comparator** - Interface para definir classe com regra de ordenação.
  - **java.util.Comparable** - Interface para definir regra de ordenação em uma classe de domínio.
- Algoritmos de ordenação.
- Utilizado primariamente em **java.util.List**.
- Permite a ordenação de objetos complexos (criados pelo usuário).

Criando um exemplo de implementação:

```java
//Classe Estudante Implementando a interface  Comparable
public class Estudante implements Comparable<Estudante>{
     private final String nome;
     private final Integer idade;

     public Estudante(String nome, Integer idade){
         this.nome = nome;
         this.idade = idade;
     }

    public String getNome() {
        return nome;
    }

    public Integer getIdade() {
        return idade;
    }

    @Override
    public String toString() {
        return "Estudante{" +
                "nome='" + nome + '\'' +
                ", idade=" + idade +
                '}';
    }

    @Override
    public int compareTo(Estudante o) {
        return this.getIdade() - o.getIdade();
    }
}
```

```java
//Classe para inverter ordem implementando também a interface Comparator
import java.util.Comparator;

public class EstudanteOrdemIdadeReversaComparator implements Comparator<Estudante> {
    @Override
    public int compare(Estudante o1, Estudante o2){
        return o2.getIdade() - o1.getIdade();
    }
}
```

```java
//Por fim, a implementação dessas duas classes, utilizando o comparator
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class ComparatorsExample{

    public static void main(String[] args) {
        List<Estudante> estudantes = new ArrayList<>();

        estudantes.add(new Estudante("Marcos", 21));
        estudantes.add(new Estudante("Ana", 23));
        estudantes.add(new Estudante("Paulo", 53));
        estudantes.add(new Estudante("Lessandra", 42));
        estudantes.add(new Estudante("Thales", 28));

        System.out.println(estudantes);

        //Ordem natural
        estudantes.sort((first,second) -> first.getIdade() - second.getIdade());
        System.out.println(estudantes);

        //Ordem inversa
        estudantes.sort((first,second) -> second.getIdade() - first.getIdade());
        System.out.println(estudantes);

        //Ordem natual - Method Reference
        estudantes.sort(Comparator.comparingInt(Estudante::getIdade));
        System.out.println(estudantes);

        //Ordem inversa - Method Reference
        estudantes.sort(Comparator.comparingInt(Estudante::getIdade).reversed());
        System.out.println(estudantes);

        //Ordem natural - Inteface Comparable
        Collections.sort(estudantes);
        System.out.println(estudantes);
        
        //Ordem inversa - Interface Comparable
        Collections.sort(estudantes,new EstudanteOrdemIdadeReversaComparator());
        System.out.println(estudantes);

    }
}
```

## Optionals

- Tratamento para valores que podem ser nulos.
- Possui 2 estados.
  - Presente
  - Vazio
- Permite que você execute operações em valores que podem ser nulos sem preocupação com as famosas NullPointerExceptions.

## Stream API

- Manipulação de coleções com o paradigma funcional de forma paralela.
- Imutável - Não altera a coleção origem, sempre cria uma nova coleção.
- Principais funcionalidades.
  - ***Mapping*** - retorna uma coleção com mesmo tamanho da origem com os elementos alterados.
  - ***Filtering*** - retorna uma coleção igual ou menos que a coleção origem, com os elementos intactos.
  - ***ForEach*** - executa uma determinada lógica para cada elemento, retornando nada.
  - ***Peek*** - executa uma determinada lógica para cada elemento, retornando a própria coleção.
  - ***Counting*** - retorna um inteiro que representa a contagem de elementos.
  - ***Grouping*** - retorna uma coleção agrupada de acordo com a regra definida.
