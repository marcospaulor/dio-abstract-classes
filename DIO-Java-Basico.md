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

- Primitivos

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

    

- Wrappers

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

    

- Não Primitivos

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

    

- Tipagem Forte e Estática

### Modificadores de acesso

### Interfaces

### Enums