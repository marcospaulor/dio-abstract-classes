# Java Avançado

## Paradigma Funcional no Java

*Requisitos básicos:*

- Conceitos básicos de java
- Orientação a objeto
- Java Generics
- Collections: List e Set

O paradigma funcional é processo de construir software através de composição de funções puras, evitando compartilhamento de estados, dados mutáveis e efeitos colaterais. É declarativa ao invés de imperativa, essa é a definição de Eric Elliot.

**Paradigma Imperativo:** E aquele que expressa o código através de comandos ao computador, nele é possível ter controle de estado dos objetos.

```java
class Imperativo{
    public static void main(String[] args){
        int valor = 10; //Instrução
        int resultado = valor * 3; //Instrução
        System.out.println("O resultado é: " + resultado);
    }
}
```

**Paradigma funcional:** Damos uma regra, uma declaração de como queremos que o programa se comporte.

```java
class Funcional{
    public static void main(String[] args){
        UnaryOperator<Integer> calculaValorVezes3 = valor -> valor * 3; //Conceito Paradigma Funcional
        int valor = 10;
        System.out.println("O resultado é: " + calculaValorVezes3.apply(10));
    }
}
```

### Conceitos Fundamentais da Programação Funcional

**Composição de funções**: É criar uma nova função através da composição de outras. Ex.: vamos criar uma função que vai filtrar um array, filtrando somente os números pares e multiplicando por dois.

```java
package testes;

import java.util.Arrays;

public class Testes {
    public static void main(String[] args) {
        int[] valores = {1,2,3,4};

//        Paradigma Funcional
        Arrays.stream(valores)
                .filter(numero -> numero % 2 == 0)
                .map(numero -> numero * 2)
                .forEach(numero -> System.out.println(numero));

//       Paradigma Imperativo
        for (int i = 0; i < valores.length; i++) {
            int valor = 0;
            if (valores[i] == 0){
                valor = valores[i] * 2;

                if(valor != 0){
                    System.out.println(valor);
                }
            }
        }
    }
}
```

**Funções Puras**: É chamada de pura quando invocada mais de uma vez, produz exatamente o mesmo resultado.

```java
package testes;

import java.util.function.BiFunction;

public class FuncoesPuras {
    public static void main(String[] args) {
        BiFunction<Integer,Integer> verificaSeEMaior =
                (parametro, valorComparacao) -> parametro > valorComparacao;

        System.out.println(verificaSeEMaior.test(13,12));
        System.out.println(verificaSeEMaior.test(13,12));
    }
}
```

**Imutabilidade**: Significa que uma vez que uma variável que recebeu um valor, vai possuir o esse valor para sempre, ou quando criamos um objeto ele não pode ser modificado.

```java
package testes;

import java.util.function.UnaryOperator;

public class Imutabilidade {
    public static void main(String[] args) {
        int valor = 20;

        UnaryOperator<Integer> retornarDobro = v -> v * 2;
        System.out.println(retornarDobro.apply(valor)); //Altera valor
        System.out.println(valor); // Não altera valor
    }
}
```

**Imperativo X Declarativo**

É muito comum aprender a programar de forma imperativa, onde mandamos alguém fazer algo. Busque o usuáro 15 no banco de dados. Valide essas informações do usuário.

Na programação funcional tentamos programar de forma declarativa, onde declaramos o que desejamos, sem explicitar como será feito. Qual o número 15? Quais os erros dessas informações?

## Lambda no Java

Os lambdas obedecem o conceito do paradigma funcional, com eles podemos facilitar legibilidade do nosso código, além disso com a nova API Funcional do Java podemos ter uma alta produtividade para lidar com objetos. Primeiramente, devemos entender o que são interfaces funcionais.

**Interfaces funcionais**: São interfaces que possuem apenas um método abstrato. Ex.: 

```java
public interface Funcao{
	String gerar(String valor);
}
```

Geralmente as interfaces funcionais possuem uma anotação em nível de classe (@FuncionlInterface), para forçar o compilador a apontar um erro se a interface não estiver de acordo com as regras de uma interface funcional. Esta anotação não é obrigatória, pois o compilador consegue reconhecer uma interface em tempo de compilação.

```java
public class Exemplo{
    public static void main(String[] args){
        Funcao funcao = valor -> valor;
    }
}

@FunctionlInterface
interface Funcao{
    String gerar(String valor);
}
```

Agora sabemos como se define uma interface funcional, podemos aprender como se define uma lambda. **Estrutura lambda**: 

```java
InterfaceFuncional nomeVariavel = parametro -> lógica;
```

Código utilizando o lambda da Interface Função:

```java
class FuncaoComLambda{
    public static void main(String[] args){
        Funcao colocaPrefixoSenhorNaString = valor -> "Sr. " + valor;
        System.out.println(colocarPrefixoSenhorNaString.gerar("Joao"));
    }
}

@FuncionalInterface
interface Funcao{
    String gerar(String valor);
}
```

*Obs.: Quando a lambda possui apenas uma instrução no corpo de sua lógica não é necessário o uso de chaves.*

Se a função possui mais de uma instrução DEVEMOS utilizar chaves e além disso deve explicitar o retorno se o retorno for diferente de void. Ex.:

```java
Funcao colocarPrefixoSenhorNaString = valor -> {
    String valorComPrefixo = "Sr. " + valor;
    String valorComPrefixoEPontoFinal = valorComPrefixo + ".";
    return valorComPrefixoEPontoFinal;
}
```

### Recursividade

Na recursividade, uma função chama a si mesma repetidamente, até atingir uma condição de parada. No caso de Java, um método chama a si mesmo, passando para si objetos primitivos. Cada chamada gera uma nova entrada na pilha de execução, e alguns dados podem ser disponibilizados em um escopo global ou local, através de parâmetros em um escopo global ou local.

:exclamation: Recursividade tem um papel importante em programação funcional, facilitando que evitemos estados mutáveis e mantenhamos nosso programa mais declarativo, e menos imperativo.

Exemplo de calculo fatorial de forma recursiva:

```java
class FatorialRecursivo{
    public static void main(String[] args){
        System.out.println(fatorial(5));
    }
    
    public static int fatorial(int value){
        if(value == 1){
            return value;
        } else {
            return value * fatorial((value - 1));
        }
    }
}
```

**Tail Call (Recursividade em cauda)**: Recursão em cauda é uma recursão onde não há nenhuma linha de código após a chamada do próprio método e, sendo assim, não há nenhum tipo de processamento a ser feito após a chamada recursiva.

**Obs.: A JVM não suporta a recursão em cauda, ela lança um estouro de pilha (StackOverFlow).**

Exemplo de fatorial com Tail Call:

```java
class FatorialComTailCall{
     public static void main(String[] args){
        System.out.println(fatorial(5));
    }
    
    public static double fatorial(double valor){
        return fatorialComTailCall(valor,1);
    }
    
    public static double fatorialComTailCall(double valor, double numero){
        if(valor == 0){
            return numero;
        }
        return fatorialComTailCall(valor - 1, numero * valor);
    }
}
```

**Memoization:** é uma técnica de otimização que consiste no cache do resultado de uma função, baseado nos parâmetros de entrada. Com isso, nas seguintes execuções conseguimos ter uma resposta mais rápida.

```java
import java.util.HasMap;
import java.util.Map;

class FatorialMemoization{
    static Map<Integer,Integer> MAPA_FATORIAL = new HashMap<>();
    
    public static void main(String[] args){
        long I = System.nanoTime();
        System.out.println(fatorialComMemoization(15));
        long F = System.nanoTime();
        System.out.println("Fatorial 1: "(F - I));
        
        I = System.nanoTime();
        System.out.println(fatorialComMemoization(15));
        F = System.nanoTime();
        System.out.println("Fatorial 2: "(F - I));
    }
    
    public static Integer fatorialComMemoization(Integer value){
        if(value == 1){
            return value;
        } else {
            if(MAPA_FATORIA.containsKey(value)){
                return MAP_FATORIAL.get(value);
            } else {
                Integer resultado = value fatorialComMemoization(value - 1);
                MAPA_FATORIAL.put(value, resultado);
                return resultado;
            }
        }
    }
}
```

## Interfaces Funcionais

#### Funções de alta ordem

É uma função que retorna uma função ou que recebe uma função como parâmetro.

```java
public class FuncaoDeAltaOrdem {
    public static void main(String[] args) {
        Calculo SOMA = (a,b) -> a + b;
        Calculo SUB = (a,b) -> a - b;
        Calculo MULTI = (a,b) -> a * b;
        Calculo DIV = (a,b) -> a / b;

        System.out.println(executarOperacoes(SOMA, 1,3));
        System.out.println(executarOperacoes(SUB,4,3));
        System.out.println(executarOperacoes(MULTI,4,2));
        System.out.println(executarOperacoes(DIV,7,3));

    }

    public static int executarOperacoes(Calculo calculo, int a, int b){return calculo.calcular(a,b);};
}

@FunctionalInterface
interface Calculo{
    public int calcular(int a, int b);
}
```

#### Consumer

Interface funcional que recebe um parâmetro e não retorna nada.

```java
import java.util.function.Consumer;

public class Consumidores{
    public static void main(String[] args){
        Consumer<String> imprimirUmaFrase = System.out::println;
        imprimirUmaFrase.accept("Hello World");
    }
}
```

#### Function

Basicamente a mesma ideia do Consumer, mas as functions recebem o parâmetro, tendo que responder esses parâmetros também.

```java
import java.util.function.Function;

public class Funcao {
    public static void main(String[] args) {
        Function<String,String> retornarNomeAoContrario = texto -> new StringBuilder(texto).reverse().toString();
        Function<String,Integer> converterStringParaInteiroEDobrar = string -> Integer.valueOf(string) * 2;
        System.out.println(retornarNomeAoContrario.apply("Marcos"));
        System.out.println(converterStringParaInteiroEDobrar.apply("20"));
    }
}
```

#### Predicados

Recebem uma parâmetro qualquer e retorno booleano.

```java
import java.util.function.Predicate;

public class Predicados {
    public static void main(String[] args) {
        Predicate<String> estaVazio = valor -> valor.isEmpty();
        System.out.println(estaVazio.test("Marcos"));
        System.out.println(estaVazio.test(""));
    }
}
```

## Processamento Assíncrono e Paralelo

### Threads

É um pequeno programa que trabalha como um subsistema, sendo uma forma de um processo se autodividir em duas ou mais tarefas. Essas tarefas múltiplas podem ser executadas simultaneamente para rodar mais rápido do que um programa em um único bloco ou praticamente juntas.

**Processamento síncrono**: são todos os processamentos que ocorrem em sequência (sincronia). Os processos são executados em fila. É preciso que um processo termine para que outro processo seja executado.

**Processamento assíncrono**: é quando dois ou mais processos são realizados ao mesmo tempo. Os processos são realizados simultaneamente sem que um processo necessite que outro termine para ser executado.

Exemplo de Thread:

```java
public class ThreadExemplo {
    public static void main(String[] args) {
        GerarPDF inciarGeradorPdf = new GerarPDF();
        BarraDeCarregamento iniciarBarraDeCarregamento = new BarraDeCarregamento(inciarGeradorPdf);

        inciarGeradorPdf.start();
        iniciarBarraDeCarregamento.start();
    }
}

class GerarPDF extends Thread{
    @Override
    public void run(){
        try {
            System.out.println("Iniciar geração de PDF");
            Thread.sleep(5000);
        } catch (InterruptedException e){
            e.printStackTrace();
        }
        System.out.println("PDF gerado");
    }
}

class BarraDeCarregamento extends Thread{
    private final Thread inciarGeradorPdf;

    public BarraDeCarregamento(Thread inciarGeradorPdf) {
        this.inciarGeradorPdf = inciarGeradorPdf;
    }

    @Override
    public void run(){

        while (true){
            try {
                Thread.sleep(500);
                if (!inciarGeradorPdf.isAlive()){
                    break;
                }
                System.out.println("Loading...");
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
    }
}
```

Agora um exemplo da API 8 do Java, utilizando o ExecutorService:

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class FutureExemplo {
    //Esta instancia incica para o ExecutorService que inicie 3 Threads
    private static final ExecutorService pessoasParaExecutarAtividade = Executors.newFixedThreadPool(3);

    public static void main(String[] args) throws InterruptedException {
        Casa casa = new Casa(new Quarto());
        List<Future<String>> futuros =
        new CopyOnWriteArrayList<>(casa.obterAfazeresDaCasa().stream()
                .map(atividade -> pessoasParaExecutarAtividade.submit(() -> {
                        try {
                            return atividade.realizar();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                        return null;
                    })
                )
                .collect(Collectors.toList()));

        while (true){
            int numeroDeAtividadesNaoFinalizadas = 0;
            for (Future<?> futuro : futuros) {
                if (futuro.isDone()){
                    try {
                        System.out.println("Parabens voce terminou de "+futuro.get());
                        futuros.remove(futuro);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } catch (ExecutionException e) {
                        e.printStackTrace();
                    }
                }
                else {
                    numeroDeAtividadesNaoFinalizadas++;
                }
            }
            if (futuros.stream().allMatch(Future::isDone)){
                break;
            }
            System.out.println("Numero de atividades nao finalizadas :: "+numeroDeAtividadesNaoFinalizadas);
            Thread.sleep(500);
        }
        pessoasParaExecutarAtividade.shutdown();
    }
}

class Casa {
    private List<Comodo> comodos;

    // Os 3 pontos tem a mesma representação que um array
    Casa(Comodo... comodos) {
        this.comodos = Arrays.asList(comodos);
    }

    List<Atividade> obterAfazeresDaCasa() {
        return this.comodos.stream().map(Comodo::obterAfazeresDoComodo)
                .reduce(new ArrayList<Atividade>(), (pivo, atividades) -> {
                    pivo.addAll(atividades);
                    return pivo;
                });
    }
}

interface Atividade {
    String realizar() throws InterruptedException;
}

abstract class Comodo {
    abstract List<Atividade> obterAfazeresDoComodo();
}

class Quarto extends Comodo {
    @Override
    List<Atividade> obterAfazeresDoComodo() {
		
        /*
            As póximas linhas tem a mesma representação que:
            ArrayList<Object> objects = new ArrayList<>();
            object.add(this.getArrumarACama());
            object.add(this.varrerOQuarto());
            object.add(this.arrumarGuardaRoupa());
         */
        
        return Arrays.asList(
                this::arrumarACama,
                this::varretOQuarto,
                this::arrumarGuardaRoupa
        );
    }

    private String arrumarGuardaRoupa() throws InterruptedException {
        Thread.sleep(5000);
        String arrumar_o_guarda_roupa = "arrumar o guarda roupa";
        System.out.println(arrumar_o_guarda_roupa);
        return arrumar_o_guarda_roupa;
    }

    private String varretOQuarto() throws InterruptedException {
        Thread.sleep(7000);
        String varrer_o_quarto = "varrer o quarto";
        System.out.println(varrer_o_quarto);
        return varrer_o_quarto;
    }

    private String arrumarACama() throws InterruptedException {
        Thread.sleep(10000);
        String arrumar_a_cama = "Arrumar a cama";
        System.out.println(arrumar_a_cama);
        return arrumar_a_cama;
    }
}
```

## Por dentro da modularização do Java

### Jigsaw

Há muito tempo se diz sobre modularizar a plataforma Java. É um plano que começou desde antes do Java 7, foi uma possibilidade no Java 8 e por fim, para permitir mais tempo de desenvolvimento, revisão e testes, foi movido para o Java 9.

O projeto Jigsaw, como foi chamado, é composto por uma série de JEPs. Algumas delas inclusive já disponíveis no Java 8, como os conhecidos Compact Profiles. A ideia por trás do projeto não é só criar um sistema de módulos, que poderemos usar em nossos projetos, mas também aplicar em toda a plataforma e JDK em busca de melhor organização e desempenho. 

# :warning: *PRECISA SER CONCLUÍDO PELOS VÍDEOS RESTANTES*
