# Java Básico

## O que é Java?

Java é uma linguagem de programação e plataforma computacional lançada em 1995 pela Sun Microsystems, por um time comandado por James Gosling. Anos depois foi adquirida pela Oracle.

Diferente de outras linguagens de programação, que são compiladas para código nativo, o Java é compilado para um bytecode que é interpretado por uma máquina virtual.

## O que é o compilador?

Um compulador é um programa que, a partir de um código fonte, cria um programa semanticamente equivalente, porém escrito em outra linguagem, código objeto. Um compilador traduz um programa de uma linguagem textual para uma linguagem de máquina, específica para um processador e sistema operacional.

O nome compilador é usado principalemente para os programas que traduzem o código fonte de uma linguagem de programa de alto nível para um linguagem de programação de baixo nível (por exemplo Assembly ou código de máquina).

## O que é a JVM? O que é uma VM?

Primeiramente um VM, Virtual Machine, é um software que simula uma máquina física e consegue executar vários programas, gerenciar processos, memória e arquivos. Tudo isso faz parte de uma plataforma com memória, processador e outros recusos totalmente virtuais, sem dependência do hardware.

O JVM é um máquina virtual que executa programas JAVA, executando os bytecodes em linguagem de máquina para cada sistema operacional.

Em linguagens compiladas diretamente para um sistema operacional SO específico, esse programa não irá executar em outro SO, havendo a necessidade de compilar uma versão do software para cada SO.

Com o Java, compilamos para a JVM, o bytecode será executado pela máquina virutal, e não diretamente pelo SO, assim, o software escrito em Java possui portabilidade para qualquer sistema operacional, porém cada JVM deve ser construída para um SO específico.

## O que é JRE?

JRE significa Java Runtime Environment, ou Ambiente de Execução do Java, é composto pela JAVA VIRTUAL MACHINE (JVM), bibliotecas e APIs da linguagem Java e outros componentes para suporte da plataforma Java.

Ele representa a parte responsável pela execução do software Java.

## O que é JDK?

Java Development Kit (JDK), Kit de Desenvolvimento Java, é um conjunto de utilitários que permitem criar software para a plataforma Java. É composto pelo compilador Java, bibliotecas da linguagem, ferramentas  e JRE.

## O que é Java SE?

Java Standard Edition(SE), é a distribuição mínima da plataforma de desenvolvimento de aplicações Java.

OpenJDK é a implementação de referência opensource da Plataforma Java, Java SE, que ainda é mantida pela Oracle.

## O que é Java EE?

Java Enterprise Edition, é uma extensão da Java SE que possui suporte a desenvolvimento de sistemas corporativos.

Além do mínimo da plataforma, o Java EE possui diversas especificações de partes da infra estrutura de aplicações, como acesso a banco de dados, mensageria, serviços web, parser de arquivos e outras.

Servidores de Aplicações Java EE, sabem seguir essas especificações e implementar os recursos para usuário.

Ex.: JBoss (RedHat), Weblogic (Oracle), WebSphere(IBM) e **Glassfih**.

## O que é Jakarta EE?

Com falta de investimento da Oracle no Java, ela cedeu todo o código, implementações e especificações do Java EE para o a Eclipse Foundation, mas como  nome Java EE é marca registrada, foi escolhido Jakarta EE.

Agora a evolução das especificações e padrões Java será feito sob o nome Jakarta EE, com compatibilidade com o Java EE.

## Característica da Linguagem Java

### Classes

- Main

  A classe Main resumidamente, será uma classe que executaria o programa.

  ```java
  package exemplo.projeto.main; //Pacote genérico
  
  public class Programa{
      //Esta é a classe main. Com assinatura String[] args.
      public static void main(String[] args){
          System.out.println("Executa Programa");
      }
  }
  ```

  

- Atributos

  O atributos de uma classe são basicamente variáveis em que podem ser acessadas de acordo com construtores(através de instancias) e métodos.

  ```java
  public class Pessoa{
      private int idade;
      protected String senha;
      public String nome; //Não há a necessidade de informar o public
  }
  ```

  

- Métodos
  - Retornos
  
    De acordo com o tipo da função o método irá retornar o mesmo tipo.
  
    ```java
    private String getSenha(){
        return senha; //retorna o atributo da classe Pessoa
    }
    ```
  
    
  
  - Parâmetros
  
    São valores em que o construtor e métodos possuem, onde geralmente há a passagem de valor.
  
    ```java
    //Estão entre parênteses name e sruname
    public String getNameAndSurname(String name, String surname){
        return System.out.println(name + " " + surname);
    }
    ```
  
    
  
  - Assinatura
  
    Tem correlação com o nome do método e os parâmetros.
    
    ```java
    //Está é assinatura do método acima
    getNameAndSurname(String,String);
    ```
    
    
  
- Construtores

  Método particular que define como instanciar a classe em sua criação.

  ```java
  public class Pessoa{
      private String login;
      protected String senha;
      String nome;
      
      //Construtor com dois parâmetros login e senha
      public Pessoa(final String login, final String senha){
          this.login = login;
          this.senha = senha;
      }
  }
  ```

  

### Tipos

- #### Primitivos

  Um tipo primitivo nunca pode ser nulo.

  - Inteiro

    Valor padrão: 0

    ```java
    int i = 2147483647;				//32 bits
    int i1 = -2147473648;
    //int i1 = -2147473649;			//To large
    ```

    

  - String

    Valor padrão: null

  - Char

    Valor padrão: '\u000'

    ```java
    char c;							//16 bits
    char c1 = 'A';
    char c2 = 15;
    //char c3 = 'AA';				//NOK
    //char c4 = -100;				//NOK
    ```

    

  - Short

    Valor padrão: 0

    ```java
    short s;					//16 bits
    short s1 = 32767;
    short s2 = -32768;
    ```

    

  - Byte

    Valor padrão: 0

    ```java
    byte b;						//8 bits
    byte b1 = 127;
    byte b2 = -128;
    //byte b3 = 129; 			//to large
    ```

    

  - Float

    Valor padrão: 0.0f

    ```java
    float f = 64f;			//32 bits
    float f2 = 65.0f;
    float f3 = -0.5f
    ```

    

  - Double

    Valor padrão: 0.0d

    ```java
    double d = 1024.99;		//64 bits
    double d2 = 20.2456;
    ```

    

  - Boolean

    Valor padrão: false

    ```java
    boolean bo = true;
    boolean bo2 = false;
    //boolean bo3 = "false";		//NOK
    //boolean bo4 = 'true';			//NOK
    ```

    

  - Long

    Valor padrão: 0L

    ```java
    long l = 9223372036854775807L;	//64 bits
    long l2 = -9223372036854775808L;
    //long l3 = -9223372036854775809L; // To large
    ```

    

- #### Wrappers

  São objetos que representam os primitivos. Geralmente representados com a primeiro letra maiúcula.

  ```java
  Byte b;
  Character c;
  Short s;
  Integer i;
  Long l;
  Float f;
  Double d;
  Boolean bo;
  ```

  

  - Auto-boxing

    Auto inicializa o objeto, com isso é possível utilizar valores **nulos**.

  - Unboxing

    É possível atribuir os wrappers aos tipos primitivos

    ```java
    int i = new Integer(3);
    int inteiro = Integer.valueOf(1024);
    boolean bo =  new Boolean(true);
    boolean boleano = Boolean.TRUE;
    ```

    

- #### Não Primitivos

  - Void

    ```java
    Void v;
    ```

    

  - String

    ```java
    String text = "Meu texto";
    ```

    

  - Number

    ```java
    Number numero = 100;
    ```

    

  - Object

    ```java
    Object o = new Object();
    ```

    

- #### Tipagem Forte e Estática

  - Estática

    Checagem de tipo em tempo de compilação

  - Forte

    Quando se atribui um tipo à aquela variável, o tipo nunca se altera para outro tipo 

  - Ps.: Tipagem Inferida, a partir do Java 10. Onde há a utilização do tipo **var**.

### Modificadores de acesso

- #### Public

  Pode ser acessada de qualquer lugar por qualquer entidade que possa visualizar a classe a que ela pertence.

- #### Private

  Os métodos e atributos da classe definidos como privados não podem ser acessadas ou usadas por nenhuma outra classe. Esses atributos e métodos também não podem ser visualizados pelas classes herdadas.

- #### Protected

  Torna o membro acessível às classes do mesmo pacote ou através de herança, seus membros herdados não são acessíveis a outras classes fora do pacote em que foram declarados.

- Default(Padrão)

  A classe e/ou seus membros são acessíveis somente por classes do mesmo pacote, na sua declaração não é definido nenhum tipo de modificador, sendo este identificado pelo computador.

- #### Abstract

  Esse modificador não é aplicado nas variáveis, apenas em classes e métodos. Uma classe abstrata não pode ser instanciada. Se houver alguma declaração de um método como abstract, a classe também deve ser marcada como abstract.

- #### Static

  É usado para a criação de uma variável que poderá ser acessada por todas as instâncias de objetos desta classe como uma variável comum, ou seja, a variável criada será a mesma em todas as instancias e quando seu conteúdo é modificado numa das instâncias, a modificação ocorre em todas as demais. E nas declarações de métodos ajudam no acesso direto à classe, portanto não é necessários instanciar um objetos para acessar o método.

- #### Final

  Quando é aplicado na classe, não permite estender, nos métodos impede que o mesmo seja sobrescrito(overriding) na subclasse, e no valores de variáveis não pode ser alterado depois que já tenha sido atribuído um valor.

### Interfaces

```java
public interface Display{
    ...
}
```



- Métodos Abstratos

  Devem ser implementados por todos;

  Novos métodos quebram as implementações;

  ```java
  public interface Display{
      String marca(); //método abstrato
      default void ligar(){
          System.out.println("Ligar tela");
      };
  }
  
  //Implementação
  
  public class Tela implements Display{
      @Override
      public String marca(){
          return "Samsung";
      }
  }
  ```

  

- Métodos Default

  São herdados a todos que implementam;

  Novos métodos não quebram as implementações;

  ```java
  public interface Display{
      String marca(); 
      
      // Método Default
      default void ligar(){
          System.out.println("Ligar tela");
      };
  }
  ```

  

- Herança Múltipla

  ```java
  public class Tela implements Display, Size{
      ...
  }
  ```

  

### Enums

- Basicamente é um dicionário de dados imutável.

- Não é permitido criar novas instâncias.

- O construtor é sempre declarado como private;

- Por convenção, por serem objetos constantes e imutáveis (static final), os nomes são em maiúsculos.

```java
public enum TipoVeiculo{
    
    TERRESTRE,
    AQUATICO,
    AEREO
    
}
```



### Strings

É uma sequencia de caracteres.

Pacote **java.lang**;

```java
//Classe exemplo
public class String{
    var nome = "Marcos";
    var sobreNome = "Rodrigues";
    //Tipos de concatenção de Strings
    final var nomeCompleto = nome + sobreNome;
    System.out.println("Nome: " + nome);
    System.out.println("Nome completo: " + nomeCompleto);
    
    //Exemplos de conteúdos dentro da classe String
    var string = new String("Minha string");
    
    System.out.println("Char na posição: " + string.charAt(5));
    System.out.println("Quantidade = " + string.length());
    System.out.println("Sem trim [" + string + "]");
    System.out.println("Com trim [" + string.trim() + "]");
    System.out.println("Lower: " + string.toLowerCase());
    System.out.println("Upper: " + string.toUpperCase());
    System.out.println("Contém M?" + string.contains("M"));
    System.out.println("Replace: " + string.replace("n","$"));
    System.out.println("Equals?" + string.equals("Minha string"));
    System.out.println("EqualsIgnoreCase?" + string.equalsIgnoreCase("minha String"));
    System.out.println("Substring(1,6)" + string.substring(1,6));
}
```

Outro exemplo mas dessa vez com o ***Format***.

```java
public class StringFormat{
    var nome = "Marcos";
    var sobreNome = "Rodrigues";
    final var nomeCompleto = nome + sobreNome;
    
    final var mensagem = String.format("O sobrenome do %s é o %s.", nome, sobreNome);
    System.out.println(mensagem);
    
    // No caso de valores numéricos
    System.out.println(String.format("Número %.2f", 1.2375d));
}
```

E também algumas funcionalidade do String Builder.

```java
var nome = "Marcos";

final var builder = new StringBuilder(nome);
System.out.println(builder.append("Paulo"));

final var reverse = builder.reverse();

final var insert = reverse.insert(0,"3").insert(reverse.length(), "#");
```

### Laços, Condicionais e Operadores

- **IF**

  ```java
  final var condicao = true;
  if(condicao){
      ...
  } else {
      ...
  }
  
  if(condicao)
      ...
      
  final var ternario = condicao ? "verdadeira" : "falsa";
  
  //Igualdades e desigualdades
  
  final var numero = 10;
  
  if(numero == 10) {
      System.out.println("O número é 10");
  } else {
      System.out.println("Não é 10");
  }
  
  if(numero != 10){
      System.out.println("Não é 10");
  } else {
      System.out.println("O número é 10");
  }
  
  final var letra = "B";
  
  if("A".equals(letra)){
      System.out.println("É a letra A");
  }
  
  if(!letra.equals("A")){
      System.out.println("Não é a letra A");
  }
  ```

  

- Operadores Matemáticos

  ```java
  var soma = 10 + 1;
  var sub = 5 - 2;
  var multi = 5 * 2;
  var div = 10 / 2;
  var resto = 8 % 2;
  ```

  

- Operadores Relacionais

  ```java
  final var numero = 6;
  
  if(numero > 20){
      System.out.println("Maior que 20");
  } else if(numero >= 10){
      System.out.println("Maior ou igual a 10");  
  } else if(numero <= 5){
      System.out.println("Menor ou igual a 5");
  } else {
      System.out.println("Nenhuma das anteriores");
  }
  ```

  

- Operadores Lógicos

  ```java
  final var numero = 2;
  final var letra = "A";
  
  //Sort Circuit
  if(numero < 5 && letra.equals("A")){
      System.out.println("Atendeu a condição");
  }
  
  if(numero < 5 || letra.equals("A")){
      System.out.println("Atendeu a condição");
  }
  
  if((10 - 5) > 5 && (5 - 3) > 1){
      System.out.println("Imprime");
  }
  
  
  ```

  

- Incremento

  ```java
  var numero = 1;
  
  ++numero; //incrementa e depois avalia a expressão
  numero++; //avalia a expressão depois incrementa
  ```

- For

  ```java
  for(int i = 0; i <= 10; i++){
      System.out.println("I = " + i);
  }
  
  //Looping infinito
  
  for( ; ; ){...Instrução}
  ```

  

- While

  ```java
  while(x< 1){
      System.out.println("Dentro do While");
      x++;
  }
  ```

  

- Do While

  ```java
  do{
      System.out.println("Dentro do Do/While");
  } while(y++ < 1);
  ```

### Convenções de Nomes

#### Nomes de Classes 

As classes, possuem sempre a primeira letra maiúscula. E em classes que possuem nomes compostos, os primeiras letras de cada palavra também são maiúsculas.

```java
class Classe{
    ...
}

class ClasseComposta{
    ...
}
```

#### Nomes de Métodos

Os métodos possuem nomes com todas as letra minúsculas. E se composto, a primeira palavra totalmente minúscula e as outras palavras sempre com primeira letra maiúscula.

```java
public static void metodo(){
    ...
}

public static void metodoComposto(){
    ...
}
```



#### Nome de Variáveis

Devem ser auto explicativas e não são inseridos números nos nomes das variáveis. Sempre minúscula.

```java
var numero = 10;
var nome = "Marcos";
var sobreNome = "Rodrigues";
```

### Plugins

Ver tutoriais sobre eles.

- #### Checkstyle Gradle Plugin

- #### PMD Grade Plugin

## Trabalhando com datas

### java.util.Date

A implementação do **java.util.Date** está na JDK desde sua versão 1.0. É de se esperar que algumas coisas não se mostrem tão interessantes nos dias atuais, dado a sua idade.

Documentação oficial: https://docs.oracle.com/javase/8/docs/api/java/util/Date.html

Construtores principais da classe:

```java
Date();

Date(int year, int month, int date); //Deprecated

Date(int year, int month, int date, int hrs, int min); // Deprecated

Date(int year, int month, int date, int hrs, int min, int sec); // Deprecated

Date(long date);

Date(String s); // Deprecated
```

- **Date( )**

  Este construtor vai alocar um objeto da classe Date e o **inicializará com o milissegundo mais próximo** do período da sua execução. 

  Exemplo:

  ```java
  import java.util.Date;
  
  public class Exemplo{
      public static void main(String[] args){
          
          Date novaData = new Date();
          System.out.println(novaData);
          
      }
  }
  ```

  

- **Date(long date)**

  Diferente do construtor anterior, esse construtor espera que você passe os milissegundos com base padrão de tempo (epoch) que usa como referência **1 de janeiro de 1970 00:00:00**.

  - O que é **Epoch**?

    É um padrão largamente aceito para representar uma data como um inteiro 32-bits a partir do início do **Unix Epoch.**

    

  O método **System.currentTimeMIllis( )**, método estático vai nos retornar o milissegundo mais próximo de sua execução com base no S.O.

  Exemplo:

  ```java
  import java.util.Date;
  
  public class Exemplo{
      public static void main(String[] args){
          long currentTimeMillis = System.currentTimeMillis();
       
          System.out.println(currentTimeMillis);
  		// 1563127311564 
          
          Date novaData = new Date(currentTimeMillis);
          
          System.out.println(novaData);
          //Sun Jul 14 15:01:51 BRT 2019
      }
  }
  ```



**Métodos Úteis:**

|   **Método**    | **Retorno** |                        **Descrição**                         |
| :-------------: | :---------: | :----------------------------------------------------------: |
|   after(Date)   |   boolean   | Checa se  o objeto Data de referência é posterior ao comparado. |
|  before(Date)   |   boolean   | Checa se o objeto Data de referência é atingida ao comparado. |
| compareTo(Date) |     int     |                  Compara dois objetos Data.                  |
|  equals(Date)   |   boolean   |               Checa se os objetos são iguais.                |
|   getTime( )    |    long     |               Retorna a data em milissegundos.               |
|  setTime(long)  |    void     |          Define uma data com base em milissegundos.          |
| from(Instante)  | static Date |           Define uma data com base  em um Instant.           |
|  toInstant( )   |   Instant   |           Retorna um Instant com base em um Date.            |



Exemplo do after before:

```java
import java.util.Date;

public class Exemplo{
    public static void main(String[] args){
        Date dataNoPassado = new Date(1513124807691L);
        //Tue Dec 12 22:26:47 BRST 2017
        
        Data dataNoFuturo = new Date(1613124807691L);
        //Fri Feb 12 08:13:27 BRST 2021
        
        /** Comparando se a dataNoPassado é posterior a dataNoFuturo*/
        boolean isAfter = dataNoPassado.after(dataNoFuturo);
        
        System.out.println(isAfter);
        //False
        
        /** Comparando se a dataNoPassado é anterior a dataNoFuturo*/
        boolean isBefore = dataNoPassado.before(dataNoFuturo);
        
        System.out.println(isBefore);
        //True
        
    }
}
```

Exemplo compareTo e equals:

```java
import java.util.Date;

public class Exemplo{
    public static void main(String[] args){
        Date dataNoPassado = new Date(1513124807691L);
        //Tue Dec 12 22:26:47 BRST 2017
        
        Data dataNoFuturo = new Date(1613124807691L);
        //Fri Feb 12 08:13:27 BRST 2021
        
        Data mesmaDataNoFuturo = new Date(1613124807691L);
        
        /** Comparando se a dataNoPassado é posterior a dataNoFuturo*/
        boolean isEquals = dataNoFuturo.after(mesmaDataNoFuturo);
        
        int compareCase1 = dataNoPassado.compareTo(dataNoFuturo); 
        int compareCase2 = dataNoFuturo.compareTo(dataNoPassado); 
        int compareCase3 = dataNoFuturo.compareTo(mesmaDataNoFuturo);
        
    }
}
```

Classe Instant

- Imutável e Thread safe;
- Modela um ponto instantâneo de uma linha do tempo;
- Indicado para gravar marcações temporais em eventos da sua aplicação;

### java.util.Calendar

É uma classe abstrata que provê métodos para converter data entre um instante específico. Possui alguns campos específicos  para manipulação como MONTH, YEAR, HOUR etc.

```java
import java.util.Calendar;

public class Exemplo{
    public static void main(String[] args){
        Calendar agora = Calendar.getInstance();
        
        System.out.println(agora);
    }
}
```

Manipulando datas

```java
import java.util.Calendar;

public class Exemplo{
    public static void main(String[] args){
        Calendar agora = Calendar.getInstance();
        
        System.out.println("A data corrente é:" + agora.getTime());
        
        agora.add(Calendar.DATE, -15);
        System.out.println("15 dias atrás:" + agora.getTime());
        
        agora.add(Calendar.MONTH, 4);
        System.out.println("4 meses depois: " + agora.getTime());
        
        agora.add(Calendar.YEAR, 2);
        System.out.println("2 anos depois: " + agora.getTime());
    }
}
```

Imprimindo **datas** e **horas**:

Aqui vão algumas maneira de se converter o resultado de um objeto **Calendar**.

```java
import java.util.Calendar;

public class Exemplo{
    public static void main(String[] args){
        Calendar agora = Calendar.getInstance();
        
        //Dom jul 14 20:58:11 BRT 2019
        System.out.printf("%tc\n",agora);
        
        //2019-07-14
        System.out.printf("%tF\n",agora);
        
        //07/14/19
        System.out.printf("%tD\n",agora);
        
        //08:58:11 PM
        System.out.printf("%tr\n",agora);
        
        //20:58:11
        System.out.printf("%tT\n",agora);
    }
}
```

### java.text.DateFormat

Nesse ponto em que estamos existem, basicamente, duas classes para formatação de datas. O **DateFormat** e o **SimpleDateFormat**. Ambos oferecem maneiras de formatar e parsear a saída das datas.

#### DateFormat

```java
import java.util.Date;
import java.text.DateFormat;

public class Exemplo{
    public static void main(String[] args){
        Date agora = new Date();
        
        String dateToStr = DateFormat.getInstance().format(agora);
        
        //14/07/19 22:40
        System.out.println(dateToStr);
        
        dateToStr = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.SHORT).format(agora);
        
        //14 de Julho de 2019 22:40
        System.out.println(dateToStr);
    }
}
```

#### SimpleDateFormat

Traz uma facilidade que é definir como padrão de formatação para a saída de data que você deseja.

```java
import java.util.Date;
import java.text.SimpleDateFormat;

public class Exemplo{
    public static void main(String[] args){
        Date agora = new Date();
        
        SimpleDateFormat formatter = new SimpleDateFormat("dd/MM/yyyy");
        
        String dataFormatada = formatter.format(agora);
        
        System.out.println(dataFormatada);
    }
}
```

### Datas no Java 8+

O trabalho com datas nas versões acima do java 8, são determinadas pelo pacote java.time com as seguintes classes **LocalDate, LocalTime e LocalDateTime**.

#### LocalDate

É uma classe imutável para representar uma data. Seu formato padrão é **yyyy-MM-dd**.

```java
import java.time.LocalDate;

public class Exemplo{
    public static void main (String[] args){
        
        LocalDate hoje = LocalDate.now();
        
        LocalDate ontem = hoje.minusDays(1);
        
        //2019-07-14
        System.out.println(hoje);
        
        //2019-07-13
        System.out.println(ontem);
    }
}
```

#### LocalTime

É uma classe imutável que representa um padrão de hora-minuto-segundo. Pode ser representado até o nível de nanosegundos. Sua utilização é similar ao **LocalDate**.

```java
import java.time.LocalTime;

public class Exemplo{
    public static void main (String[] args){
        
        LocalTime agora = LocalTime.now();
        
        LocalTime maisUmaHora = agora.plusHours(1);
        
        //23:53:58.421
        System.out.println(agora);
        
        //00:55:37.421
        System.out.println(maisUmaHora);
    }
}
```

#### LocalDateTime

Funciona como uma espécie de junção entre o LocalTime e o LocalDate. Também é uma classe imutável e você consegue trabalhar com dia e hora de uma vez só. Pode também trabalhar data e hora com precisão de nanosegundos.

```java
import java.time.LocalDateTime;

public class Exemplo{
    public static void main (String[] args){
        
        LocalDateTime agora = LocalDateTime.now();
        
        LocalDate futuro = agora.plusHours(1).plusDays(1).plusSeconds(12);
        
        //2019-07-15T00:02:16.076
        System.out.println(agora);
        
        //2019-07-17T01:02:28.076
        System.out.println(ontem);
    }
}
```

## Tratamento de Exceções

Requisitos básicos para aprender:

- Básico de Orientação a Objeto
- Básico de métodos encadeados
- Básico de algoritmos

### Exceptions

São todos os erros que ocorrem durante o processamento de um método que podem ser esperados ou não esperados. Como o termo já diz, "Exceptions" são exceções. Falhas que não devem ocorrer rotineiramente no fluxo de um sistema.

Exemplo de tratamento de exceção:

```java
public static void metodo(){
    try{
        new java.io.FileInputStream("arquivo.txt");
    }catch(java;io.FileNotFoundException e){
        System.out.println("Não foi possível abrir o arquivo para leitura");
    }
}
```

### Checked Exceptions

São exceções esperadas, cujo fluxo ou método de uma sistema foi preparado para receber. Um bom exemplo é uma exceção de negócio, onde se deseja informar um erro caso a exceção esperada ocorra.

Exemplo de checked exception:

```java
try{
    PreparedStatement stmt = con.prepareStatement(query);
    ...
} catch(SQLException e){
    throw new AcessoADadosException("Problema na criação do Statment", e);
}
```

### Unchecked Exceptions

São exceções não esperadas para o fluxo ou método de um sistema, um bom exemplo é a famosa NullPointException que ocorre quando se tenta acessar uma referência de memória vazia, ou recuperar uma instância que não existe, dentre outros motivos.

Exemplo de unchecked exception:

```java
try{
	CarroVo carro = new CarroVo();
	carro.getPlaca();
} catch(IntegrationException e){
    throw new BusinessException("Erro na criação do objeto", e);
}
```

#### Bloco Try catch

Este bloco sempre é utilizado quando no processo que será executado dentro de um método é esperado um erro, então cria-se um bloco "protegido" onde qualquer erro que ocorra dentro do trecho "try" é direcionado para o trecho "catch" e sofreráo devido tratamento de erro.

Exemplo de um bloco try/catch:

```
try{
    PreparedStatement stmt = con.prepareStatement(query);
    ...
} catch(SQLException e){
    throw new AcessoADadosException("Problema na criação do Statment", e);
}
```

### Finally

É um bloco de código que pode ou não ser utilizado junto ao try catch, este trecho de código sempre será executado independente se ocorrer erro ou não dentro do fluxo onde existe o try catch. Normalmente o finally é usado para liberar recursos ou para dar continuidade em um fluxo que deve ocorrer independente de erro.

Exemplo de bloco finally:

```java
try{
    PreparedStatement stmt = con.prepareStatement(query);
    ...
} catch(SQLException e){
    throw new AcessoADadosException("Problema na criação do Statment", e);
} finally{
    stmt.close();
}
```

### Throw e Throws

- **Throws**: é a assinatura do método que será retornado caso ocorra erro para o método que fez a chamada, dentro de um fluxo encadeado.
- **Throw**: é usado para lançar a exceção desejada, juntamente com a mensagem de erro, para o método que fez a chamada. 

Exemplo de throw e throws:

```java
public String recuperaIdUsuario(String query) throws AcessoADadosException{
    try{
        PreparedStatement stmt = con.prepareStatement(query);
        ...
    } catch(SQLException e){
        throw new AcessoADadosException("Problema na criação do Statment", e);
    } finally{
        stmt.close();
    }
}
```

