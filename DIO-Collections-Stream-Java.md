# Implementações Collections e Streams com Java

## Collections - List

- Implementações
  1. java.util.ArrayList
  2. java.util.Vector
- Garante Ordem de inserção
- Permite adição, atualização, leitura e remoção sem regras adicionais
- Permite ordenação através de comparativos

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
}
```

